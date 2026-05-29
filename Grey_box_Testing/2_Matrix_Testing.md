# 2. Matrix Testing
**Fitur yang diuji:** Pencarian dan Filter Data Pendaftar (Dashboard Admin PPDB)

## 1. Definisikan Parameter dan Kondisi
Pada fitur pencarian pendaftar, kita memiliki tiga parameter utama untuk memfilter data:
* **Nama Pendaftar:** Valid (Huruf alfabet) / Tidak Valid (Mengandung angka/simbol)
* **Status Berkas:** Lengkap / Belum Lengkap
* **Jalur Pendaftaran:** Reguler / Pindahan

**Kondisi:** Kombinasi dari ketiga parameter di atas saat admin melakukan pencarian data siswa di tabel *dashboard*.

## 2. Membuat Tabel Matriks
Berikut adalah rancangan matriks kombinasi untuk skenario pengujian:

| ID Test | Nama Pendaftar | Status Berkas | Jalur Pendaftaran | Ekspektasi Hasil (Sistem PPDB) | Status (Lulus/Gagal) |
| :---: | :--- | :--- | :--- | :--- | :---: |
| TC-01 | Valid | Lengkap | Reguler | Menampilkan data pendaftar reguler berkas lengkap | [ ] |
| TC-02 | Valid | Belum Lengkap | Pindahan | Menampilkan data pendaftar pindahan berkas belum lengkap | [ ] |
| TC-03 | Valid | Lengkap | Pindahan | Menampilkan data pendaftar pindahan berkas lengkap | [ ] |
| TC-04 | Tidak Valid | Lengkap | Reguler | Menampilkan "Data tidak ditemukan" atau error validasi huruf | [ ] |
| TC-05 | Tidak Valid | Belum Lengkap | Pindahan | Menampilkan "Data tidak ditemukan" atau error validasi huruf | [ ] |

## 3. Menjalankan Test Case
*(Langkah ini dilakukan oleh tester dengan memasukkan kombinasi parameter di atas pada antarmuka admin PPDB, lalu mencatat hasilnya di kolom Status)*

## 4. Analisa Hasil Test
*(Bagian ini diisi jika ada kombinasi parameter yang membuat sistem crash atau gagal memfilter data dengan benar. Jika gagal, bug akan dicatat untuk diperbaiki)*
