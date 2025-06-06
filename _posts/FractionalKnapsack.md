## Definisi
Fractional Knapsack adalah sebuah permasalahan optimisasi dalam bidang algoritma dan struktur data, di mana tujuannya adalah untuk memaksimalkan nilai total barang yang dimasukkan ke dalam sebuah knapsack (tas) dengan kapasitas tertentu, dengan kemungkinan mengambil sebagian (fraksi) dari barang.


## Karakteristik
Setiap barang memiliki berat (weight) dan nilai (value). Kapasitas tas adalah terbatas. Barang boleh dipotong atau diambil sebagian (misalnya 0.5 bagian dari barang A). Masalah ini dapat diselesaikan secara greedy karena tidak memerlukan pencarian kombinasi semua kemungkinan seperti pada 0/1 Knapsack.


## Strategi Penyelesaian
Gunakan pendekatan Greedy Algorithm:
1. Hitung value per unit weight untuk setiap item: value/weight.
2. Urutkan item berdasarkan nilai tersebut secara menurun.
3. Ambil sebanyak mungkin dari item dengan rasio tertinggi, hingga tas penuh.
4. Jika tidak bisa mengambil seluruh item karena kapasitas tersisa, ambil sebagian dari item terakhir.

## Kompleksitas Waktu
O(n log n) untuk mengurutkan item berdasarkan rasio value/weight.
O(n) untuk memasukkan item ke dalam tas.

## Aplikasi
1. Penjadwalan tugas dengan sumber daya terbatas
2. Investasi dana ke beberapa proyek 
3. Pengalokasian bandwidth di jaringan 
4. Optimisasi logistik


## Algoritma Greedy
Algoritma Greedy adalah sebuah pendekatan atau strategi dalam merancang algoritma yang membuat pilihan yang tampak terbaik pada saat itu (pilihan optimal lokal) dengan harapan bahwa pilihan tersebut akan mengarah pada solusi optimal global.
Adapun Karakteristik Utamanya:
1. Pilihan Lokal Optimal
Di setiap langkah, algoritma memilih opsi yang paling menguntungkan atau "greedy" saat itu.
2. Tidak Melihat ke Depan
Keputusan dibuat berdasarkan informasi yang tersedia saat ini saja, tanpa mempertimbangkan sub-masalah yang akan muncul setelah keputusan tersebut dibuat.
3. Sederhana dan Cepat
Algoritma greedy seringkali sangat sederhana untuk diimplementasikan dan memiliki kompleksitas waktu yang rendah dibandingkan pendekatan lain seperti pemrograman dinamis.

Algoritma greedy sangat efektif dan sering digunakan untuk masalah-masalah tertentu di mana pilihan optimal lokal memang mengarah ke solusi optimal global. Kelemahan utama algoritma greedy adalah tidak selalu menghasilkan solusi optimal global untuk semua jenis masalah. Ada masalah di mana pilihan terbaik saat ini justru menghalangi tercapainya solusi terbaik secara keseluruhan.

## Permasalahan
A. Diketahui ada 4 item dengan data berikut:
--------------------------------
| Item | Nilai (Value) | Berat |
--------------------------------
| A    | 50            | 10    |
| B    | 60            | 20    |
| C    | 140           | 40    |
| D    | 60            | 30    |
--------------------------------
Diketahui: Kapasitas tas (W) = 50
Pertanyaan: Berapa nilai maksimum yang bisa dibawa dalam tas?

Langkah Manual:
1. Hitung rasio value/weight
    A = 5.0
    B = 3.0
    C = 3.5
    D = 2.0

2. Urutkan
    A (5.0), C (3.5), B (3.0), D (2.0)

3. Isi tas berdasarkan kapasitas
    Ambil A (10kg, nilai 50) -> sisa 40
    Ambil C (40kg, nilai 140) -> sisa 0
    B dan D tidak diambil

# Total nilai maksimum = 50 + 140 = 190


B. Pendaki punya tas berkapasitas 50kg, di basecamp tersedia:
| Barang  | Berat(kg) | Nilai (pentingnya) |
--------------------------------------------
| Makanan | 10        | 60                 |
| Selimut | 20        | 100                |
| Kamera  | 30        | 120                |

Solusi:
1. Hitung value/weight
    Makanan: 60/10 = 6
    Selimut: 100/20 = 5
    Kamera: 120/30 = 4

2. Urutkan dan pilih
    Ambil semua makanan (10kg) -> Nilai = 60
    Ambil semua selimut (20kg) -> Nilai = 100
    Sisa Kapasitas = 20kg -> Ambil 2/3 kamera -> Nilai = 120 x 20/30 = 80

3. Total nilai: 60 + 100 + 80 = 240

C. Pemulung bisa bawa 15kg logam. Di tempat sampah ada:
| Logam     | Berat | Nilai Jual |
--------------------------------
| Tembaga   |   5   |    100     |
| Aluminium | 10    |    60      |
| Besi      | 20    |    80      |

Solusi:
1. Hitung value/weight:
    Tembaga: 100/5 = 20
    Aluminium: 60/10 = 6
    Besi: 80/20 = 4

2. Urutan
    Tembaga ->  Aluminium -> Besi

3. Pilih
    Tembaga (5kg) -> Nilai = 100
    Aluminium (10kg) -> Nilai = 60
    Tas penuh

4. Total Nilai
    100 + 60 = 160

## Implementasi Kode
Jika kamu bisa membawa 30kg barang, barang priotitas adalah:
| Barang     | Berat | Nilai Penting |
--------------------------------------
| Laptop     | 10    | 300           |
| Buku Paket | 20    | 200           |
| Baju       | 30    | 180           |

``` c++
// Fungsi comparator untuk mengurutkan berdasarkan rasio terbesar
bool compare (Item a, Item b) {
    return a.ratio() > b.ratio();
}

int main() {
    double capacity = 30.0; // kapasitas maksimal kurir
    vector<Item> items = {
        {"Laptop", 10, 300},
        {"Buku Paket", 20, 200},
        {"Baju", 30, 180}
    };

    // Urutkan berdasarkan rasion value/weight tertinggi
    sort(items.begin(), items.end(), compare);

    double totalValue = 0.0;
    double totalWeight = 0.0;

    cout << "Barang yang dipiih:\n";
    for (const auto& item : items) {
        if (capacity == 0) break;

        if (item.weight <= capacity) {
            // Ambil seluruh barang
            totalValue += item.value;
            capacity -= item.weight;
            cout << "-" << item.name << " (berat: " << item.weight << " kg, nilai: " << item.value << ")\n";
        } else {
            // Ambil sebagian barang (fractional)
            double fraction = capacity / item.weight;
            totalValue += capacity * fraction;
            cout << "-" << item.name << " (berat : " << capacity << " kg dari " << item.weight << " kg, nilai:  " << item.value * fraction << ")\n";
            capacity = 0;
        }
    }

    cout << "\nTotal nilai yang dibawa: " << totalValue << endl;

    return 0;
}
```