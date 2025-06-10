---
title: "Kahn’s Algorithm"
date: 2025-06-03
tags: [Kahn's Algorithm, topological sort, DAG, algoritma graf, dependensi tugas]
categories: [pemrograman, algoritma dan struktur data]
---

## Definisi dan Konsep
Kahn’s Algorithm adalah algoritma penyusunan topologi (topological sorting) yang digunakan untuk menentukan urutan dalam sebuah Directed Acyclic Graph (DAG) berdasarkan ketergantungan antar simpul.

Algoritma Kahn adalah pendekatan berbasis BFS untuk menemukan urutan node yang valid dalam Directed Acyclic Graph (DAG).

Urutan topologi DAG adalah urutan dimana untuk setiap tepi yang diarahkan u → v, u muncul sebelum v dalam urutan.

Kapan Algoritma Kahn dibutuhkan?
- Menjadwal tugas berdasarkan dependensi
- Mendeteksi siklus dalam grafik terarah
- Memproses dependensi dalam urutan yang benar

## Cara Kerja 
1. Gunakan struktur in-degree (jumlah sisi masuk) untuk tiap simpul
2. Tambahkan semua simpul dengan in-degree = 0 ke antrean (queue)
3. Proses antrean satu per satu
4. Jika semua simpul telah diproses, maka graf tidak memiliki siklus

## Contoh Kasus
1. Misalnya kita punya dependensi antar mata kuliah:

``` markdown
A -> C
B -> C
C -> D
```
- A dan B adalah prasyarat untuk C
- C adalah prasyarat untuk D

Urutan topologis yang valid: A B C D atau B A C D

2. Bayangkan kamu sedang mengelola proyek dengan 6 tugas (A sampai F), dan ada beberapa ketergantungan antar tugas:

```markdown
A -> D
F -> B
B -> D
F -> A
D -> C
```
Interpretasi Ketergantungan
- A harus selesai sebelum D
- F harus selesai sebelum A dan B
- B harus selesai sebelum D
- D harus selesai sebelum C

Urutan Topologis yang Valid

``` markdown
Salah satu urutan valid adalah:

F → A → B → D → C
F → B → A → D → C

(Penting: selama ketergantungan terpenuhi,
urutan bisa bervariasi)
```

## Implementasi Kode

``` c++
#include <iostream>
#include <unordered_map>
#include <vector>
#include <set>
#include <algorithm>
using namespace std;

unordered_map<char, vector<char>> graph;
unordered_map<char, int> in_degree;
set<char> vertices;

void allTopologicalSorts(vector<char> &res, vector<bool> &visited) {
    bool flag = false;
    for (char v : vertices) { 
        if (!visited[v] && in_degree[v] == 0) {
            // Pilih simpul v 
            visited[v] = true; 
            res.push_back(v);

            // Kurangi in-degree tetangga 
            for (char neighbor graph[v]) { 
                in_degree[neighbor]--; 
            }

            // Rekursi 
            allTopologicalSorts (res, visited);

            // Backtrack 
            visited[v] = false; 
            res.pop back(); 
            for (char neighbor: graph[v]) { 
                in_degree[neighbor]++;
            }
            flag = true;
        }
    }
}

int main() {
    int E;
    cout << "Masukkan jumlah edge (sisi): ";
    cin >> E;

    cout << "Masukkan sisi dalam format 'A B' (tanpa panah):" << endl;
    for (int i = 0; i < E; ++i) {
        char u, v;
        cin >> u >> v;
        graph[u].push_back(v);
        in_degree[v]++;
        vertices.insert(u);
        vertices.insert(v);
    }

    for (char v : vertices) {
        if (in_degree.find(v) == in_degree.end()) {
            in_degree[v] = 0;
        }
    }

    vector<char> res;
    unordered_map<char, bool> visited_map;
    for (char v: vertices) {
        visited_map[v] = false;
    }

    vector<bool> visited (256, false); // asumsi char
    allTopologicalSorts (res, visited);

    return 0;
}

```

## Kelebihan dan Kekurangan
Kelebihan:
1. Kompleksitas Waktu:
    O(V + E) sangat efisien.
2. Deteksi Siklus:
    Dapat mendeteksi siklus dalam graf berarah.
3. Masalah Dependency:
    Cocok untuk masalah dependency seperti mata kuliah, build system, atau project tasks.

Kekurangan:
1. Graf Siklus:
    Tidak bisa digunakan pada graf yang mengandung siklus.
2. Output:
    Bisa menghasilkan lebih dari satu urutan topologis yang valid.
3. Struktur Data
    Memerlukan struktur data tambahan (in-degree dan graph).