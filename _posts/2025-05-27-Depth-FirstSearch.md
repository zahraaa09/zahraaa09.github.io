---
title: "Depth-First Search (DFS)"
date: 2025-05-27
tags: [DFS, algoritma graf, traversal graf, stack, pencarian kedalaman]
categories: [pemrograman, algoritma dan struktur data]
---

## Pengertian dan Prinsip Utama
Depth-first search (dfs) adalah algoritma pencarian atau penelusuran pada struktur data graf atau pohon yang bekerja dengan menjelajahi satu cabang sedalam mungkin sebelum mundur (backtrack) dan melanjutkan ke cabang berikutnya.

Prinsip Utama DFS, yaitu:
1. Masukkan simpul (node) akar ke dalam stack
2. Ambil node dari stack teratas, lalu cek apakah node tersebut merupakan solusi?
    - jika node merupakan solusi, pencarian selesai dan hasil dikembalikan
    - jika node bukan solusi, masukkan seluruh node anak ke dalam stack
3. Jika stack kosong, dan setiap node sudah dicek. pencarian berakhir
4. Jika stack tidak kosong, ulangi pencarian mulai langkah ke-2

## Contoh Kasus
Jika penelusuran dilakukan menggunakan Depth-First Search (DFS) dari simpul awal 1, tuliskan salah satu kemungkinan urutan kunjungan simpul!

Kemungkinan DFS (Urutan Eksplorasi Berbeda):
1. 1 -> 2 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10
2. 1 -> 2 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10 -> 4
3. 1 -> 2 -> 5 -> 6 -> 9 -> 10 -> 7 -> 8 -> 4

Jika penelusuran dilakukan menggunakan Depth-First Search (DFS) dari simpul awal 1, dengan akhir 10 tuliskan kemungkinan urutan kunjungan simpul!

Kemungkinan DFS (Urutan Ekplorasi Berbeda):
1 , 2, 4, 6, 9, 10

## Implementasi Kode 
``` c++
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

void DFS(int start, vector<vector<int>>& graph, vector<bool>& visited) {
    stack<int> s;
    s.push(start);
    
    while (!s.empty()) {
        int node = s.top();
        s.pop();
        
        if (!visited[node]) {
            cout << node << " ";
            visited[node] = true;
        }

        for (int neighbor : graph[node]) {
            if (!visited[neighbor]) {
                s.push(neighbor);
            }
        }
    }
}

int main() {
    int n = 6;
    vector<vector<int>> graph(n);
    
    graph[0].push_back(1);
    graph[0].push_back(2);
    graph[1].push_back(0);
    graph[1].push_back(3);
    graph[1].push_back(4);
    graph[2].push_back(0);
    graph[2].push_back(5);
    graph[3].push_back(1);
    graph[4].push_back(1);
    graph[5].push_back(2);
    vector<bool> visited(n, false);
    
    cout << "DFS traversal starting from node 2: ";
    DFS(1, graph, visited);
    cout << endl;

    return 0;
}
```

## Kelebihan dan Kekurangan
Kelebihan:
1. Penggunaan memori lebih efisien
2. Mudah diimplementasikan
3. Cocok untuk menemukan solusi kedalaman maksimal
4. Digunakan dalam banyak algoritma penting

Kekurangan:
1. Tidak menjamin solusi yang terbaik
2. Bisa masuk ke infinite loop (pada graf biklik)
3. Kurang efisien di graf luas tapi dangkal
4. Tidak cocok untuk semua masalah