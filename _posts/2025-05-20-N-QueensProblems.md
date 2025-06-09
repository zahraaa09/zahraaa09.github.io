---
title: "N-Queens Problems"
date: 2025-05-20
tags: [N-Queens, Algoritma, Backtracking, C++, Pemrograman, AI]
categories: [Algoritma, Komputer]
---

## Definisi Masalah
Masalah N-Queens adalah sebuah permasalahan klasik dalam bidang ilmu komputer dan matematika kombinatorik yang melibatkan penempatan N buah ratu catur pada sebuah papan catur berukuran N × N, sedemikian rupa sehingga tidak ada dua ratu yang saling menyerang. Dalam aturan catur, seorang ratu dapat bergerak secara horizontal (baris), vertikal (kolom), dan diagonal. Oleh karena itu, solusi dari masalah ini harus memastikan bahwa tidak ada dua ratu yang berada pada baris, kolom, atau diagonal yang sama. Contoh paling terkenal adalah masalah 8-Queens, yaitu menempatkan 8 ratu di papan 8x8.

Tujuan utama dari masalah ini adalah:
1. Menemukan semua konfigurasi penempatan ratu yang memenuhi syarat tidak saling menyerang.
2. Mengembangkan dan menguji algoritma pencarian dan optimasi, seperti backtracking, DFS, heuristic search, atau algoritma genetika.
3. Melatih logika pemrograman dan pemecahan masalah, terutama dalam konteks constraint satisfaction problem (CSP).

## Pentingnya Masalah N-Queens
Masalah N-Queens penting dalam berbagai konteks, di antaranya:
1. Sebagai Studi Kasus dalam AI dan Algoritma:
    Masalah ini digunakan secara luas untuk mengajarkan teknik pencarian seperti backtracking, branch and bound, serta algoritma heuristic dan metaheuristic. Ini menjadikannya landasan dalam studi artificial intelligence dan operations research.
2. Model Permasalahan Constraint Satisfaction:
    N-Queens adalah contoh ideal dari masalah CSP, di mana kita harus menetapkan nilai (posisi ratu) ke dalam variabel (baris/kolom) tanpa melanggar kendala (serangan).
3. Aplikasi dalam Dunia Nyata:
    Walau berbasis permainan catur, prinsip-prinsip di balik N-Queens dapat diterapkan dalam masalah nyata seperti:
    - Penjadwalan tugas (di mana konflik harus dihindari),
    - Penempatan modul dalam sirkuit elektronik,
    - Dan pengalokasian sumber daya yang saling eksklusif.

4. Kompleksitas dan Skalabilitas:
    Masalah ini menunjukkan bagaimana kompleksitas meningkat secara eksponensial dengan bertambahnya nilai N, sehingga cocok sebagai bahan evaluasi efisiensi algoritma dalam skala besar.

## Langkah-langkah dalam Algoritma Backtracking
Backtracking adalah teknik penyelesaian masalah yang mencoba membangun solusi langkah demi langkah dan "mundur" (backtrack) ketika menemui jalan buntu (dead end). Ini adalah pendekatan brute-force yang sistematis dengan optimasi, di mana solusi yang tidak valid dibuang secepat mungkin.

1. Pilih Keputusan (Decision Choice)
    - Pada setiap langkah, pilih opsi yang mungkin dari kandidat solusi.
    - Contoh: Dalam masalah N-Queens, pilih kolom untuk
    menempatkan ratu di baris berikutnya.

2. Batasan (Constraint Check)
    - Periksa apakah pilihan tersebut valid berdasarkan aturan masalah.
    - Jika valid, lanjut ke langkah berikutnya.
    - Jika tidak valid, abaikan opsi ini dan coba opsi lain (backtrack)

3. Rekursi (Recursive Exploration)
    Jika pilihan valid, rekursif melanjutkan pencarian solusi dengan keputusan ini.

4. Backtrack (Kembali jika Dead End)
    Jika tidak ada solusi yang ditemukan setelah memilih opsi tertentu, batalkan keputusan terakhir (undo) dan coba opsi lain.

5. Basis Kasus (Base Case)
    Jika semua keputusan telah mengarah ke solusi lengkap, catat solusinya(atau kembalikan solusi).

## Contoh dalam Permutasi Angka

CARI SEMUA PERMUTASI DARI [1, 2, 3].

Langkah Algoritma:
1. Pilih angka pertama: 1
    - Subproblem: Cari permutasi [2,3] → [1, 2, 3], [1, 3, 2]
    - Backtrack: Kembali ke []

2. Pilih angka pertama: 2
    - Subproblem: Cari permutasi [1,3] → [2, 1, 3], [2, 3, 1]
    - Backtrack: Kembali ke []

3. Pilih angka pertama: 3
    - Subproblem: Cari permutasi
    - [1,2] → [3, 1, 2], [3, 2, 1]

Solusi Akhir:
[[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]]

Backtracking adalah pendekatan exhaustive search dengan optimasi, di mana solusi dibangun bertahap dan dibatalkan jika tidak valid. Alurnya melibatkan eksplorasi rekursif, pemeriksaan batasan, dan pengembalian (undo) jika gagal.

## Contoh di Dunia Nyata

Bayangkan sebuah perusahaan yang memiliki n karyawan dan ingin menempatkan mereka dalam n ruang kerja yang ada di kantor. Setiap karyawan harus ditempatkan di ruang yang tidak mengganggu satu sama lain. Aturan yang berlaku adalah:
1. Ruang yang berdekatan tidak boleh digunakan oleh dua karyawan yang sama (ibaratnya, seperti baris dan kolom dalam masalah N-Queens).
2. Karyawan yang berada dalam ruang yang sama atau saling berdekatan tidak boleh berada dalam garis lurus yang sama(seperti dalam diagonal N-Queens).
3. Tujuan: Menempatkan setiap karyawan di ruang yang berbeda dengan aturan ini, tanpa ada dua yang saling bertabrakan.

Langkah-langkah Penempatan Karyawan:
1. Ruang pertama: Kita mulai dengan menempatkan karyawan pertama di ruang pertama. Tidak ada masalah di sini karena belum ada karyawan lain yang ditempatkan.
2. Ruang kedua: Sekarang kita ingin menempatkan karyawan kedua. Dia tidak bisa ditempatkan di ruang pertama karena ruang pertama sudah diisi oleh karyawan pertama. Jadi kita lanjutkan mencari ruang yang tidak bertabrakan.
3. Ruang ketiga: Ketika kita sampai pada ruang ketiga, kita mencari ruang yang tidak bertabrakan dengan dua karyawan sebelumnya. Setelah mencoba beberapa ruang, kita menemukan ruang yang valid dan menempatkan karyawan ketiga di sana.
4. Proses Berlanjut: Proses ini berlanjut untuk semua karyawan yang ada, dengan aturan yang sama: tidak ada dua karyawan yang berada pada garis lurus atau di ruang yang saling berdekatan. Jika kita menemukan situasi di mana tidak ada ruang yang valid, kita akan kembali ke langkah sebelumnya dan mencoba opsi lain.

Jika kita sudah menempatkan beberapa karyawan dan ternyata, pada langkah terakhir, tidak ada ruang lagi yang valid untuk karyawan ke-n, kita harus mundur (backtrack) dan mencoba posisi yang berbeda untuk karyawan yang sudah ditempatkan sebelumnya. Misalnya, jika kita sudah menempatkan beberapa karyawan dan pada langkah akhir tidak bisa melanjutkan, kita akan mundur dan mencoba menempatkan karyawan yang sebelumnya di ruang yang berbeda. Begitu kita menemukan ruang yang valid, kita akan melanjutkan sampai semua karyawan ditempatkan dengan benar.

## Implementasi Kode
``` c++
/**
 * Fungsi untuk mencetak solusi yang ditemukan.
 * Menampilkan posisi ratu ('Q') dan titik kosong ('.') dalam bentuk papan.
 */
void printSolution() {
    cout << "Solusi #" << ++solutionCount << ":\n";
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            cout << (board[i][j] ? 'Q' : '.') << ' ';
        }
        cout << '\n';
    }
    cout << '\n';
}

/**
 * Fungsi untuk mengecek apakah posisi (row, col) aman untuk menempatkan ratu.
 * Mengecek apakah tidak ada ratu di baris yang sama, diagonal kiri atas, dan diagonal kiri bawah.
 */
bool isSafe(int row, int col) {
    // Periksa baris sebelah kiri
    for (int i = 0; i < col; i++)
        if (board[row][i])
            return false;

    // Periksa diagonal kiri atas
    for (int i = row, j = col; i >= 0 && j >== 0; i--, j--)
        if (board[i][j])
            return false;

    // Periksa diagonal kiri bawah
    for (int i = row, j = col; i < N && j >= 0; i++, j--)
        if (board[i][j])
            return false;

    return true;
}

/**
 * Fungsi rekursif untuk menyelesaikan N-Queens dengan backtracking.
 * Mencoba menempatkan ratu di setiap baris kolom 'col' dan melanjutkan ke kolom berikutnya.
 */
void solveNQueensUtil(int col) {
    // Jika semua ratu sudah ditempatkan, cetak solusi
    if (col >= N) {
        printSolution();
        return;
    }

    // Coba tempatkan ratu di setiap baris dalam kolom saat ini
    for (int i = 0; i < N; i++) {
        if (isSafe(i, col)) {
            board[i][col] = 1; // Tempatkan ratu
            solveNQueensUtil(col + 1); // Rekursi untuk kolom berikutnya
            board[i][col] = 0; // Backtrack (hapus ratu)
        }
    }
}

/**
 * Fungsi utama untuk menyelesaikan N-Queens.
 * Inisialisasi papan dan memulai pencarian solusi.
 */
void solveNQueens() {
    board = vector<vector<int>>(N, vector<int>(N, 0)); // Inisialisasi papan kosong
    solveNQueensUtil(0); // Mulai dari kolom pertama
    if (solutionCount == 0) {
        cout << "Solusi tidak tersedia.\n";
    } else {
        cout << "Total solusi: " << solutionCount << endl;
    }
}

/**
 * Fungsi utama program.
 * Meminta input N dari pengguna dan memulai penyelesaian N-Queens.
 */
int main() {
    cout << "Masukkan nilai N: ";
    cin >> N;
    solveNQueens();
    return 0;
}
```
