---
title: "Rat In A Maze"
date: 2025-05-27
tags: [backtracking, algoritma, rekursi, maze solving, pathfinding]
categories: [pemrograman, algoritma dan struktur data]
---

## Definisi dan Prinsip Kerja
Rat in a Maze merupakan salah satu algorithm problem di mana seekor tikus (rat) harus keluar dari sebuah labirin (maze) dengan mengikuti jalur tertentu, dari titik awal ke titik tujuan. Labirin tersebut diwakili oleh sebuah matriks atau grid yang terdiri dari sel-sel yang bisa dilewati atau terhalang. Solusi untuk masalah ini dapat menggunakan algoritma backtracking, di mana tikus mencoba bergerak satuper satu dalam langkah-langkah dan mundur (backtrack) jika jalan yang dipilih tidak berhasil.

Prinsip Kerjanya: 
1. Tikus akan mencoba menemukan jalur dari posisi awal ke tujuan di dalam sebuah labirin berbentuk matriks 
2. Tikus akan mencoba satu langkah ke suatu arah (kanan, bawah, kiri, atau atas) 
3. Jika langkah tersebut valid (tidak keluar dari labirin dan tidak menabrak dinding), maka tikus lanjut ke sel tersebut 
4. Jika dari posisi baru tidak ada jalan ke tujuan, ia mundur (backtrack) ke posisi sebelumnya dan mencoba arah lain.
Arah pergerakan tikus adalah U (atas), D (bawah) , L (kiri) , R (kanan). Sel-sel matriks memiliki nilai:
- 1 berarti bisa dilewati (jalan)
- 0 berarti tidak bisa dilewati (tembok)

## Contoh Permasalahan
Seekor tikus yang ditempatkan di (0,0) dalam matriks persegi berorde N * N. Tikus harus mencapai tujuan di (N - 1, N - 1). Temukan semua kemungkinan jalur yang dapat diambil tikus untuk mencapai dari sumber ke tujuan. Dalam satu jalur, tidak ada sel yang dpat dikunjungi lebih dari satu kali. Nilai 0 pada sel dalam matriks menunjukkan bahwa sel tersebut terhalang dan tikus tidak dapat bergerak ke sana, sedangkan nilai 1 pada sel dalam matriks menunjukkan bahwa tikus dapat melewatinya.

Langkah 1: Coba gerakan ke arah
- Bawah (D) → ke (1, 0) = 1 ✅
- Kanan (R) → ke (0, 1) = 0❌

Langkah 2: Dari (1, 0)
Tandai (1, 0)
- Pilih arah:
    - Bawah (D) → (2, 0) = 1✅
    - Kanan (R) → (1, 1) = 1 ✅
Pilih salah satu : R

Langkah 3: Dari (1, 1)
- Pilih arah:
    - Bawah (D) → (2, 1) = 1 ✅

Langkah 4: Dari (2, 1)
- Pilih arah:
    - Bawah (D) → (3, 1) = 1 ✅

Langkah 5: Dari (3, 1)
- Pilih arah:
    - Kanan (R) → (3, 2) = 1 ✅

Langkah 6: Dari (3, 2)
- Pilih arah:
    - Kanan (R) → (3, 3) = 1 ✅

Sehingga didapatkan: 
<img src="/assets/image/image-2.png" alt="hasil" width="400">

Representasi arah: DRDDRR

## Implementasi Kode
``` c++
#include <iostream>
#include <vector>
#include <cstdlib>
#include <ctime>

using namespace std;

// Cek apakah posisi (x, y) valid
bool isSafe(int x, int y, const vector<vector<int> > &maze,
            const vector<vector<bool> > &visited, int n) {
    return (x >= 0 && x < n && y >= 0 && y < n &&
            maze[x][y] == 1 && !visited[x][y]);
}

// Cetak maze dengan tanda jalur P
void printMazeWithPath(const vector<vector<int> > &maze,
                       const vector<pair<int, int> > &path, int n) {
    vector<vector<char> > visual(n, vector<char>(n));

    for (int i = 0; i < n; ++i)
        for (int j = 0; j < n; ++j)
            visual[i][j] = (maze[i][j] == 1) ? '1' : '0';

    for (size_t i = 0; i < path.size(); ++i)
        visual[path[i].first][path[i].second] = 'P';  

    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            cout << visual[i][j] << " ";
        }
        cout << endl;
    }
}

// Rekursi Backtracking untuk cari semua jalur
void solveMazeUtil(const vector<vector<int> > &maze, int x, int y,
                   vector<vector<bool> > &visited,
                   vector<pair<int, int> > &path,
                   vector<vector<pair<int, int> > > &allPaths,
                   int n) {
    if (x == n - 1 && y == n - 1) {
        path.push_back({x, y});
        allPaths.push_back(path);
        path.pop_back();
        return;
    }

    visited[x][y] = true;
    path.push_back({x, y});

    int dx[] = {1, 0, -1, 0}; // bawah, kanan, atas, kiri
    int dy[] = {0, 1, 0, -1};

    for (int dir = 0; dir < 4; ++dir) {
        int newX = x + dx[dir];
        int newY = y + dy[dir];

        if (isSafe(newX, newY, maze, visited, n)) {
            solveMazeUtil(maze, newX, newY, visited, path, allPaths, n);
        }
    }

    path.pop_back();
    visited[x][y] = false;
}

// Tampilkan semua solusi + visualisasinya
void solveMaze(const vector<vector<int> > &maze, int n) {
    vector<vector<bool> > visited(n, vector<bool>(n, false));
    vector<pair<int, int> > path;
    vector<vector<pair<int, int> > > allPaths;

    solveMazeUtil(maze, 0, 0, visited, path, allPaths, n);

    if (allPaths.empty()) {
        cout << "\nTidak ada solusi ditemukan.\n";
    } else {
        cout << "\nTotal solusi ditemukan: " << allPaths.size() << endl;

        for (size_t i = 0; i < allPaths.size(); ++i) {
            cout << "\nSolusi ke-" << i + 1 << ":\n";
            for (size_t j = 0; j < allPaths[i].size(); ++j) {
                cout << "(" << allPaths[i][j].first << "," << allPaths[i][j].second << ") ";
            }
            cout << "\nVisualisasi jalur:\n";
            printMazeWithPath(maze, allPaths[i], n);
        }
    }
}

// Buat maze acak dengan 75% kemungkinan jalan
vector<vector<int> > generateRandomMaze(int n) {
    vector<vector<int> > maze(n, vector<int>(n));
    srand(time(0));

    for (int i = 0; i < n; ++i)
        for (int j = 0; j < n; ++j)
            maze[i][j] = (rand() % 100 < 75) ? 1 : 0;

    maze[0][0] = 1;
    maze[n - 1][n - 1] = 1;

    return maze;
}

int main() {
    int n;
    cout << "Masukkan ukuran maze (n x n): ";
    cin >> n;

    vector<vector<int> > maze = generateRandomMaze(n);

    cout << "\nMaze yang dihasilkan:\n";
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            cout << maze[i][j] << " ";
        }
        cout << endl;
    }

    solveMaze(maze, n);

    return 0;
}
```

## Kelebihan dan Kekurangan
Kelebihan:
1. Sederhana dan Mudah Diimplementasikan
2. Menemukan Semua Solusi
3. Fleksibel
4. Tidak Memerlukan Struktur Data Kompleks

Kekurangan:
1. Kurang efisien dalam Kasus Besar
2. Risiko Stack Overflow
3. Tidak Optimal
4. Mengulang Jalur yang Sama Jika Tidak Diatur

## Implementasi di Kehidupan Nyata
1. Robot Navigasi
2. Pencarian Jalur di GPS atau Navigasi
3. Simulasi dan Permainan
