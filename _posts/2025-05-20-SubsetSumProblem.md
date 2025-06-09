## Definisi dan Konsep
Subset Sum Problem adalah masalah klasik dalam ilmu komputer yang termasuk dalam kategori NP-Complete. Diberikan sebuah himpunan bilangan bulat dan sebuah nilai target, tugasnya adalah menentukan apakah ada subset dari himpunan tersebut yang jumlah elemennya sama dengan nilai target.

``` pseudocode
Input: arr = [1, 2, 3], target_sum = 3
Output: True
```
Penjelasan:
Terdapat subset {1, 2} yang jumlahnya 3.
set = 1     2     3
subsets = {1}, {1,2}, {1,2,3}
          {2}, {2,3}, {1,3}
          {3}
subset sums = {1, 3, 6, 2, 5, 4, 3}
                  |
                 True

``` pseudocode
Input: arr = {10, 20, 30, 40, 50}, sum = 25
Output: False
```
Penjelasan:
Tidak ada subset yang jumlahnya 25


Subset Sum Problem (SSP) termasuk dalam decision problem, yaitu jenis masalah yang hanya membutuhkan jawaban “ya” atau “tidak”. Inti dari masalah ini adalah mencari apakah mungkin memilih sejumlah angka dari sekumpulan bilangan bulat sehingga totalnya pas sama dengan angka target. Subset Sum Problem dalam implementasinya di dunia nyata bisa ditemukan dalam bidang kriptografi, pengelolaan keuangan, perencanaan sumber daya, bahkan kecerdasan buatan.

## Variasi Masalah
1. Bounded Subset Sum Problem
Setiap elemen dalam himpunan hanya dapat digunakan sekali untuk membentuk subset yang jumlahnya sama dengan target. Artinya, jika sebuah angka muncul sekali dalam himpunan, maka kita hanya bisa menggunakannya sekali saja dalam proses pencarian solusi. Contoh Kasus:
Set = {3, 34, 4, 12, 5, 2}, Target = 9
Apakah mungkin?

Ya. Subset {4, 5} menghasilkan total 9.
Kita tidak boleh menggunakan 4 atau 5 lebih dari sekali. Ini cocok untuk kasus di mana barang atau sumber daya hanya tersedia satu unit.

2. Partition Problem
Masalah membagi sebuah himpunan bilangan bulat menjadi dua subset yang memiliki jumlah total yang sama. Secara teknis, ini setara dengan mencari subset dengan jumlah sama dengan setengah dari total seluruh elemen himpunan. 
Contoh Kasus:
Set = {1, 5, 11, 5}
Total = 22 → Target subset = 11

Ya. Kita bisa buat dua subset:
{11} dan {1, 5, 5} → keduanya berjumlah 11
Masalah ini penting dalam manajemen sumber daya, seperti membagi beban server, tugas antar tim, atau membagi file secara seimbang.

3. Exact k Elements Subset Sum
Mencari subset yang jumlahnya sama dengan target dan terdiri dari tepat k elemen. Variasi ini menambahkan batasan tambahan yaitu jumlah elemen dalam subset harus tepat sebanyak k elemen.
Contoh Kasus:
Set = {1, 2, 3, 4, 5}, Target = 9, k = 2
Apakah mungkin?

Ya. Subset {4, 5} terdiri dari 2 elemen dan jumlahnya 9. Namun subset seperti {2, 3, 4} juga jumlahnya 9, tapi terdiri dari 3 elemen, tidak valid. Masalah ini cocok untuk memilih tim beranggotakan k orang dengan total nilai tertentu, atau memilih k item dengan total harga tepat.

4. Unbounded Subset Sum Problem
Setiap elemen boleh digunakan berulang kali untuk mencapai target. Ini berarti jika kita memiliki angka 3 dalam himpunan, maka kita bisa memakainya dua, tiga, atau bahkan lebih kali selama tidak melebihi target.
Contoh Kasus:
Set = {1, 3, 4}, Target = 6
Apakah mungkin?

Ya. Beberapa kemungkinan :
- 1 + 1 + 1 + 3 = 6
- 3 + 3 = 6
- 2 × 1 + 4 = 6

5. Multi-target Subset Sum Problem
Mencari subset yang memenuhi lebih dari satu kriteria, misalnya jumlah total dan batas berat. Dalam variasi ini, masalah subset sum menjadi lebih kompleks karena tidak hanya melibatkan satu target jumlah, tetapi lebih dari satu kriteria atau batasan yang harus dipenuhi secara bersamaan
Contoh Kasus:
Set barang:
- Barang A: harga = 40, berat = 1 kg
- Barang B: harga = 60, berat = 1.5 kg
- Barang C: harga = 30, berat = 0.5 kg
- Target: total harga ≤ 100 dan total berat ≤ 2 kg

Kombinasi Barang A + C → total harga 70, berat 1.5 kg →
valid
Tapi A + B → harga 100, berat 2.5 kg → tidak valid karena melebihi berat. Masalah ini sering muncul dalam e- commerce (checkout produk dengan batas ongkir) atau logistik pengirman.

6. Approximate Subset Sum
Tidak ada subset yang jumlahnya tepat sama dengan target, jadi dicari subset terbaik yang mendekati target, biasanya tidak boleh melebihi.
Contoh Kasus:
Set = {2, 5, 10, 14}, Target = 15
Apakah mungkin?

Tidak ada subset yang tepat 15. Tapi:
- {10, 2} = 12
- {5, 10} = 15 ✅ (tepat)
Kalau target = 16, dan tidak ada kombinasi pas, kita bisa ambil {14} atau {10, 5} = 15 → solusi terbaik.

## Pendekatan Subset Sum Problem
🔁 Pendekatan Rekursif (Recursive Approach)
Cek semua subset secara eksplisit.
1. Untuk setiap elemen:
    - Sertakan ATAU ❌ Abaikan.
2. Basis kasus:
    - Jika sum == 0 → ✅ True
    - Jika n == 0 && sum != 0 → ❌ False
3. Kompleksitas: O(2n)

❌ Tidak efisien untuk array besar.

🧠Dynamic Programming Approach
1. Memoization (Top-Down DP)
    - Kombinasi rekursi + penyimpanan hasil submasalah.
    - Gunakan struktur dp[n][sum] → cache hasil.
    - Kurangi pemanggilan ulang fungsi yang sama.
    - Efisien untuk input sedang, tetap butuh stack rekursi.
    - Kompleksitas Waktu: O(n × sum)
    - Kompleksitas Memori: O(n × sum)

2. Tabulation (Bottom-Up DP)
Iteratif → mulai dari kasus paling kecil.
    - Buat tabel dp[n+1][sum+1]
        dp[i][j] = True jika subset arr[0..i-1] bisa menghasilkan j.
    - Inisialisasi:
        dp[i][0] = True (karena subset kosong = 0)
        dp[0][j] = False (tidak bisa dapat sum ≠ 0 tanpa elemen)
    - Iterasi solusi dari bawah ke atas.

3. Optimasi Ruang pada Subset Sum (Space Optimization)
Dalam pendekatan tabulasi, kita hanya membutuhkan baris sebelumnya (i-1) untuk menghitung baris saat ini. Karena itu, kita bisa menghemat ruang dari O(n × sum) menjadi O(sum) dengan dua array 1D: prev dan curr.
- prev[j]: apakah jumlah j bisa dicapai dengan elemen sebelumnya.
- curr[j]: status jumlah j saat mempertimbangkan elemen saat ini.

Aturan pengisian:
- Jika j < arr[i]: curr[j] = prev[j]
- Jika j ≥ arr[i]: curr[j] = prev[j] or prev[j - arr[i]]
Setelah satu iterasi, salin curr ke prev.

4. Tabulation (Bottom-Up)
Tabel: Tabel DP untuk Subset Sum ({1, 2, 3}, target = 3)

| i/j | 0    | 1     | 2     | 3     |
|-----|------|-------|-------|-------|
| 0   | True | False | False | False |
| 1   | True | True  | False | False |
| 2   | True | True  | True  | True  |
| 3   | True | True  | True  | True  |
tabel DP berukuran (jumlah elemen + 1) x (target + 1).

i = 0 (tanpa elemen)
- Hanya dp[0][0] = True, karena subset kosong bisa membentuk 0.
i = 1 (elemen: [1])
- dp[1][0] = True (subset kosong)
- dp[1][1] = True (pakai angka 1)
- dp[1][2] = False, dp[1][3] = False
i = 2 (elemen: [1, 2])
- Tambah angka 2 ke subset:
    - dp[2][2] = True karena 2 bisa dibentuk (hanya pakai 2)
    - dp[2][3] = False → belum bisa dapat 3
i = 3 (elemen: [1, 2, 3])
- Sekarang bisa membentuk 3:
    - dp[3][3] = True karena 1 + 2 = 3

## Implementasi Kode
``` c++
#include <iostream>
#include <vector>
using namespace std;

void cariSubset(int arr[], int n, int index, int target, vector<int>& subset) {
    if (target == 0) {
        cout << "Subset ditemukan: ";
        for (int num : subset) cout << num << " ";
        cout << endl;
        return;
    }
    if (index ==  n || target < 0) return;

    // Ambil elemen arr[index] (boleh diambil berkali-kali, jadi index tetap)
    subset.push_back(arr[index]):
    cariSubset(arr, n, index + 1, target - arr[index], subset);
    subset.pop_back();

    // Skip elemen ini, lanjut ke elemen berikutnya
    cariSubset(arr, n, index + 1, target, subset);
}

int main() {
    int n, target;
    cout << "Masukkan jumlah elemen: ";
    cin >> n;

    int arr[100];
    cout << "Masukkan elemen: ";
    for (int i = 0; i < n; i++) cin >> arr[i];

    cout << "Masukkan target: ";
    cin >> target;

    vector<int> subset;
    cout << "Subset yang jumlahnya " << target << ":\n";
    cariSubset(arr, n, 0, target, subset);

    return 0;
}
```

## Permasalahan Subset Sum di Dunia Nyata
1. Kriptografi: Digunakan dalam sistem kriptografi berbasis ransel, di mana kesulitan menyelesaikan Permasalahan Subset Sum menjadi dasar keamanan kunci publik.
2. Alokasi Sumber Daya: Membantu memilih subset proyek atau item agar sesuai dengan anggaran atau target tertentu.
3. Genetika dan Bioinformatika: Digunakan untuk menganalisis kombinasi gen atau fragmen DNA dengan total ekspresi atau panjang tertentu.
4. Keuangan dan Investasi: Membantu menentukan apakah target investasi dapat dicapai dengan memilih kombinasi aset yang tepat.
5. Perancangan Permainan dan Teka-Teki: Muncul dalam permainan atau teka-teki yang melibatkan pencarian kombinasi angka sesuai skor target.