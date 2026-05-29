# 3. Regression Testing
[cite_start]**Skenario Uji:** Menambah Fitur Baru (Export Data Pendaftar) pada Dashboard Admin[cite: 146, 154].

## A. Deskripsi Kasus
[cite_start]Pengembang baru saja menambahkan fitur tombol "Export to CSV" agar admin dapat mengunduh seluruh data pendaftar[cite: 156, 158, 190]. 
[cite_start]**Tujuan Pengujian:** Memastikan bahwa fungsionalitas dasar aplikasi PPDB (seperti menambah, mengedit, dan menghapus data siswa) masih berfungsi dengan baik dan tidak terganggu setelah fitur *export* ini ditambahkan ke dalam sistem[cite: 159, 160, 161].

## B. Langkah Pengujian (Regression Suite)
[cite_start]Berdasarkan standar pengujian, berikut adalah langkah-langkah regresinya[cite: 162]:

1. **Uji Ulang Fungsionalitas Dasar:**
   * [cite_start]Jalankan kembali test case fungsionalitas dasar aplikasi (Tambah Siswa, Edit Status, Hapus Siswa)[cite: 163].
   * [cite_start]Pastikan semua test case dasar tersebut lulus dengan sukses tanpa ada *error* baru[cite: 164].
2. **Uji Fitur Baru (Export):**
   * [cite_start]Uji fitur baru impor/ekspor data buku secara menyeluruh untuk memastikan fungsionalitasnya bekerja dengan benar[cite: 165, 166]. (Klik tombol Export, periksa apakah file CSV terunduh, dan buka file untuk memastikan datanya sesuai).
3. **Pemeriksaan Dampak (Impact Analysis):**
   * [cite_start]Periksa apakah fitur baru ekspor data tidak menyebabkan masalah (bug) pada antarmuka tabel pendaftar atau fungsi pencarian yang sudah ada[cite: 167].

## C. Hasil Eksekusi Regresi
| Modul yang Diuji | Tindakan | Ekspektasi | Status (Lulus/Gagal) | Catatan |
| :--- | :--- | :--- | :---: | :--- |
| CRUD Pendaftar | Tambah data pendaftar baru | Data berhasil tersimpan ke database | [ ] | |
| CRUD Pendaftar | Hapus data pendaftar | Data berhasil terhapus dari tabel | [ ] | |
| Fitur Export | Klik tombol "Export to CSV" | File CSV berhasil diunduh dan format rapi | [ ] | |
| UI/UX | Cek tampilan tabel data | Tabel tidak berantakan setelah ada tombol baru | [ ] | |
