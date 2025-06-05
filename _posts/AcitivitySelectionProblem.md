*Pendahuluan dan Definisi Masalah*
Activity selection problem merupakan masalah optimasi klasik dalam ilmu komputer. Kita diberikan sejumlah aktivitas yang masing-masing didefinisikan dengan waktu mulai dan waktu selesai. Dua aktivitas dikatakan kompatibel jika mereka tidak tumpang tindih secara waktu, artinya salah satu aktivitas selesai sebelum aktivitas lainnya dimulai.

*Konsep Dasar Algoritma Greedy*
Algoritma greedy adalah strategi pemecahan masalah optimasi yang bekerja dengan membuat pilihan yang tampak paling baik pada  setiap langkah, dengan harapan rangkaian pilihan ini akan mengarah pada solusi  yang optimal secara keseluruhan. Algoritma ini bersifat serakah karena langsung mengambil pilihan terbaik saat itu tanpa mempertimbangkan konsekuensi di masa depan.

Dalam konteks activity selection problem, algoritma greedy  secara efektif diterapkan dengan memilih aktivitas yang memiliki waktu selesai paling awal di setiap langkah.
Pemilihan yang optimal ini didasarkan pada gagasan bahwa dengan menyelesaikan suatu aktivitas lebih awal, kita memaksimalkan sisa waktu yang tersedia untuk memilih aktivitas-aktivitas lain yang tidak bertabrakan. Strategi greedy ini terbukti menghasilkan solusi dengan jumlah aktivitas maksimal yang dapat dipilih tanpa adanya konflik waktu.

*Algoritma Activity Selection Problem*
Algoritma Activity Selection Problem menggunakan pendekatan greedy dengan memilik aktiviitas berdasarkan waktu selesai (finish time). Ide kuncinya adalah dengan memilih aktivitas yang selesai paling awal, kita memaksimalkan waktu tersisa untuk aktivitas lainnya.
1.	Urutkan semua aktivitas berdasarkan waktu selesai  (finish time)
2.	Pilih aktivitas pertama (aktivitasa dengan waktu selesai paling awal)
3.	Untuk aktivitas berikutnya, pilih jika waktu mulainya lebih besar atau sama dengan waktu selesai aktivitas yang dipilih sebelumnya.


*Problem and Solution*
-------------------------------------------
| Aktivitas |	Mulai (s)	| Selesai (f) |
|-----------|---------------|-------------|
|A1	        |      1        |      4      |
|A2         |      3        |      5      |
|A3         |      0        |      6      |
|A4	        |      5        |      7      |
|A5	        |      8        |      9      |
|A6	        |      5        |      9      |
-------------------------------------------

Langkah Solusinya:
1.	Urutkan berdasarkan waktu selesai
Berdasarkan waktu selesainya, kita dapat mengurutkannya A1, A2, A3, A4, A5, A6.
2.	Pilih aktivitas yang selesai paling awal, yaitu A1.
3.	Iterasi:
a.	A2, A3: Tumpah tindih karena A2 selesai detik ke 5 sementara A3 dimulai pada detik ke 0.
b.	A4: Kompatibel, pada aktivitas A1 selesai pada detik ke 4 sementara aktivitas A4 dimulai pada detik ke 5.
c.	A5: Kompatibel, pada aktivitas A1 selesai pada detik ke 4, aktivita A4 selesai pada detik 7, dan aktivitas A5 dimulai  pada detik 8.
d.	A6: Tumpang tindih karena aktivitas A5 selesai pada detik ke 9, sementara aktivitas A6 dimulai pada detik ke 5.

Sehingga, dapat kita simpulkan untuk solusi optimalnya yaitu A1, A4, dan A5.

*Implementasi*
''' c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

struct Activity {
    int start, finish;
    int index;
}

bool activityCompare(Activity s1, Activity s2) {
    return (s1.finish < s2.finish);
}

void printMaxActivities(vector<Activity>& arr, int n) {
    sort(arr.begin(). arr.end(). activityCompare);

    cout << "Aktivitas yang terpilih: ";

    int i = 0;
    cout << "A" << arr[i].index << " ";

    for (int j = 1; j < n; j++) {
        if (arr[j].start >= arr[i].finish) {
            cout << "A" << arr[j].index << " ";
            i = j;
        }
    }
    cout << endl;
}
int main() {
    vector <Activity> arr = {
        {1, 4, 1}, // A1
        {3, 5, 2}, // A2
        {0, 6, 3}, // A3
        {5, 7, 4}, // A4
        {8, 9, 5}, // A5
        {5, 9, 6}  // A6
    };

    int n = arr.size();
    printMaxActivities(arr, n);

    return 0;
}
'''

Output:
Aktivitas yang terpilih: A1 A4 A5

*Analisis Kompleksitas*
Kompleksitas waktu:
1.	Pengurutan aktivitas berdasarkan waktu selesai, O(n log n)
2.	Pemilihan aktivitas, O(n log n)
3.	Total kompleksitas waktu, O(n log n)
Langkah pertama dalam algoritma ini adalah mengurutkan aktivitas berdasrkan waktu selesai. Menggunakan algoritma pengurutan yang efisien Quich Sort atau Merge Sort membutuhkan waktu O(n log n) untuk n aktivitas.
Komplektsitas Ruang:
1.	Menyimpan aktivitas, O(n)
2.	Tidak memerlukan ruang tambahan yang siginifikan selain untuk menyimpan input dan output.
Algoritma memerlukan ruang O(n) untuk menyimpan n aktivitas dalam array atau vektor. Selain itu, kita memerlukan ruang tambahan untuk menyimpan hasil (subset aktivitas yang dipilih) yang dalam kasus terburuk juga O(n). Operasi pengurutan mungkin memerlukan ruang tambahan O(n log n) atau O(n), tergantung pada implementasi algoritma pengurutan yang digunakan.

*Aplikasi Dunia Nyata*
Penjadwalan dan Fasilitas: jadwal ruang kelas, meeting, lab, olahraga
Sistem Operasi: jadwal proses CPU, alokasi memori
Logistik: jadwal pengiriman dan rute kendaraan
Telekomunikasi: alokasi bandwidth dan jadwal transmisi data