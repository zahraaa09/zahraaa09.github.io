## Pengertian dan Konsep Dasar
Huffman Coding adalah algoritma kompresi data lossless yang dikembanhkan oleh David A. Huffman pada tahun 1952. Huffman Coding digunakan untuk mengurangi ukuran data dengan cara mengganti simbol sering muncul dengan kode bit lebih pendek. Umumnya digunakan dalam format kompresi seperti ZIP, JPEG, dan MP3.

Huffman Coding bekerja berdasarkan:
1. Berdasarkan frekuensi karakter dalam data.
2. Karakter dengan frekuensi tinggi → kode pendek.
3. Karakter dengan frekuensi rendah → kode panjang.
4. Representasi data menggunakan pohon biner.

## Proses Huffman Coding
1. Hitung frekuensi tiap karakter dalam data.
2. Buat simpul untuk setiap karakter.
3. Gabungkan dua simpul dengan frekuensi terkecil.
4. Ulangi hingga terbentuk satu pohon Huffman.
5. Tentukan kode biner untuk tiap karakter (0: kiri, 1: kanan).

## Contoh Permasalahan
String = “ABBCCCDDDD”
Frekuensi:
    A = 1
    B = 2
    C = 3
    D = 4

Bangun pohon Huffman berdasarkan frekuensi.
Hasil kode mungkin:
    D = 0, C = 10, B = 110, A = 111
   
Output terkompresi: lebih pendek dari representasi asli.

## Simulasi
1.  PESAN - BCCABBDDAECCBBAEDDCC
    
    PANJANG = 20

Pada Komponen Elektronik, alfabet dikirim melalui kode ASCII. Kode ASCII untuk huruf kapital A adalah 65, dan kita membutuhkan 8 bit biner untuk mengonversi 65.
- Untuk 1  huruf, kita membutuhkan 8 bit
- Untuk 20 huruf, kita membutuhkan 8 x 20 = 100 bit

| Huruf | Kode ASCII |
|-------|------------|
| A     | 65         |
| B     | 66         |
| C     | 67         |
| D     | 68         |


2. PESAN - BCCABBDDAECCBBAEDDCC

Langkah pertama, urutkan jumlah kemunculan huruf dari yang terkecil ke yang terbesar, kemudian ambil dua yang paling kecil dan gabungkan keduanya. Sekarang, node akar untuk huruf E dan A adalah 5.

| Huruf | Jumlah |
|-------|--------|
| A     | 3      |
| B     | 5      |


3. PESAN - BCCABBDDAECCBBAEDDCC

| Huruf | Jumlah | Huffman Code |
|-------|--------|--------------|
| A     | 3      | 1            |
| B     | 5      | 10           |
| C     | 6      | 11           |
| D     | 4      | 1            |
| E     | 2      | 0            |

Total = 45 bit

Awalnya kita membutuhkan 160 bit, namun sekarang kita hanya membutuhkan 45 bit. Dengan demikian, kita telah mengompresi biaya dan ukuran data.

## Implementasi Kode
```  pseudocode
Huffman(C)
    n = |C|
    Q = C
    for i = 1 to n - 1
        allocate new node z
        z.left = x = Extract-Min(Q)
        z.right = y = Extract-Min(Q)
        insert(Q, z)
    return Extract-Min(Q) // returns the root
```

Kompleksitas Waktu:
O(n log n)

(N = Jumlah Karakter Unik)

## Kelebihan dan Kekurangan
Kelebihan:

✅ Lossless: tidak ada data yang hilang.

✅ Efisien untuk data dengan distribusi karakter tidak merata.

✅ Digunakan luas di sistem kompresi file.

Kekurangan:

❌ Kurang optimal jika frekuensi karakter merata.

❌ Memerlukan tabel kode untuk dekompresi.


