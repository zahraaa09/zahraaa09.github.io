---
layout: post
title: "Breadth-First Search (BFS)"
date: 2025-05-27
tags: [BFS, algoritma graf, pencarian jalur, antrian, traversal graf]
categories: [pemrograman, algoritma dan struktur data]
---

## Pengertian dan Konsep Dasar
Breadth-First Search (BFS) adalah metode untuk menjelajahi graph atau pohon dengan menelusuri simpul-simpul berdasarkan jaraknya dari titik awal. Secara sederhana, BFS akan mengeksplorasi semua simpul yang paling dekat terlebih dahulu, baru kemudian beralih ke simpul yang lebih jauh. Jadi pendekatannya menyebar ke seluruh arah secara merata dari pusat.

Sebagai ilustrasi, bayangkan kita sedang mencari ruang kelas di sebuah gedung kampus berlantai 3. Kita pasti akan memeriksa seluruh ruangan dari lantai pertama sebelum lanjut ke lantai atas. Itulah cara kerja BFS: menjelajah secara mendatar.

BFS banyak digunakan dalam berbagai aplikasi, mulai dari pencarian rute tercepat dalam game, penelusuran jaringan sosial, hingga pencarian jalur optimal dalam sistem navigasi dan peta digital.

Konsep Dasar dari BFS, yaitu:
1. BFS menggunakan struktur queue (antrian).
2. Mulai dari simpul awal → kunjungi semua tetangga → lanjut ke tetangga dari tetangga.
3. Bersifat level-order traversal (per lapisan).

## Langkah-langkah Algoritma BFS
1. Tentukan simpul awal (start node) 
2. Masukkan simpul (node) ke dalam antrian (queue)
3. Ambil simpul dari queue terdepan, tandai bahwa simpul telah dikunjungi, dan cek apakah merupakan solusi/tujuan
4. Selama antrian tidak kosong atau simpul aktif bukan merupakan tujuan, lakukan:
    - Ulangi proses pencarian mulai langkah ke-2 sampai ke-3
    - Keluarkan simpul dari antrian (dequeue)
    - Untuk setiap tetangga dari simpul (jika ada):
        - Kunjungi semua tetangga yang belum dikunjungi lalu tandai sebagai dikunjungi
        - Tambahkan ke antrian (enqueue)
Ulangi sampai simpul tujuan ditemukan atau queue sudah kosong.

## Cara Kerja BFS
<img src="/assets/image/image.png" alt="bfs" width="400">

| Queue      | Visited   | Simpul Aktif |
|------------|-----------|--------------|
| S          | S         | S            |
| A, B       | SA        | A            |
| B, C, D    | SAB       | B            |
| C, D, E, F | SABC      | C            |
| D, E, F    | SABCD     | D            |  
| E, F       | SABCDE    | E            |
| F, H, G    | SABCDEF   | F            |
| H, G       | SABCDEFH  | H            |
| G          | SABCDEFHG | G            |

## Implementasi Kode
``` c++
using namespace std;

// Inisialisasi graf dengan adjacency list
unordered_map<char, vector<char>> graf;

// Menyimpan simpul yang sudah dikunjungi
unordered_map<char, bool> sudahDikunjungi;

// Menyimpan jalur: simpul_sekarang -> simpul_sebelumnya
unordered_map<char, char> parent;

void bsf(char start, char goal) {
    queue<char> q;
    q.push(start);
    sudahDikunjungi[start] = true;
    parent[start] = '-'; // Titik awal tidak punya parent

    while (!q.empty()) {
        char sekarang = q.front();
        q.pop();
        cout << "Kunjungi node: " << sekarang << endl;

        // Jika goal ditemukan, langsung hentikan
        if (sekarang == goal) break;

        for (char tetangga : graf[sekarang]) {
            if (!sudahDikunjungi[tetangga]) {
                q.push(tetangga);
                sudahDikunjungi[tetangga] = true;
                parent[tetangga] = sekarang;
            }
        }
    }

    // Cetak jalur terpendek dari goal ke start
    vector<char> jalur;
    char current = goal;
    while (current != '-') {
        jalur.push_back(current);
        current = parent[current];
    }

    cout << "\n=== HASIL ===" << endl;
    cout << "Start Node: " << start << endl;
    cout << "Goal Node: " << goal << endl;
    cout << "Jalur Terpendek: ";
    for (int i = jalur.size() - 1; i >= 0; i--) {
        cout << jalur[i];
        if (i != 0) cout << " -> ";
    }
    cout << endl;
}
```

## Aplikasi di Kehidupan Nyata
1. BFS dalam Labirin
Digunakan untuk mencari jalan terpendek dari titik awal ke tujuan.
- Contoh: Game Pac-Man menghitung rute terpendek untuk mengejar pemain.
- Cara kerja: Mengeksplorasi semua jalur level demi level (tetangga terdekat dulu) hingga menemukan exit.

2. BFS di Media Sosial
Platform seperti Facebook atau LinkedIn menggunakan BFS untuk menemukan teman atau koneksi dalam jarak tertentu (misal: "Orang yang mungkin Anda kenal").
- Cara kerja: Menelusuri teman langsung (level 1), lalu temannya teman (level 2), dst.

3. BFS dalam Jaringan Komputer
Memetakan semua perangkat (PC, server, router) dalam jaringan.
Cara Kerja:
- Mulai dari router utama, telusuri perangkat yang terhubung per level:
    - Level 1: Switch langsung terhubung ke router.
    - Level 2: PC/server yang terhubung ke switch
    tersebut.

4. BFS dalam Trasportasi & Nafigasi (Google Maps, Grab, Gojek)
BFS digunakan untuk menemukan rute terpendek dari titik A ke B dengan asumsi semua edge memiliki bobot yang sama (misal: jumlah jalan, bukan jarak).
- Contoh: Mencari jalur dengan paling sedikit persimpangan.

## Kelebihan dan Kekurangan
Kelebihan : Menjamin ditemukannya solusi yang paling baik (omplit dan optimal).

Kekurangan : Membutuhkan memori dan waktu yang cukup banyak.