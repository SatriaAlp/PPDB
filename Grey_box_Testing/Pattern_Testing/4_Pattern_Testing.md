# Pengujian 4: Pattern Testing (Exploratory)
**Fokus:** Mencari bug dengan cara eksplorasi sistem PPDB tanpa script test yang terlalu kaku.

### 1. Uji Fungsional Dasar
* [x] Membuka alur form pendaftaran dari awal sampai akhir. **Hasil:** Data masuk ke DB local/production dengan mulus.
* [x] Login admin dan mengubah status pendaftaran anak dari "Pending" jadi "Diterima". **Hasil:** Status terupdate secara *real-time* di tabel admin.
* [x] Hapus satu data testing pendaftar. **Hasil:** Data terhapus dan tidak merusak relasi tabel data orang tua.

### 2. Nyari Bug (Edge Cases / Skenario Aneh)
* [x] Coba masukkan nama anak menggunakan emoji atau simbol aneh. **Hasil:** Sistem berhasil memfilter input dan memunculkan error "Nama hanya boleh berisi huruf".
* [x] NIK sengaja dikosongkan atau diisi huruf, lalu klik submit. **Hasil:** Frontend langsung memblokir aksi klik dengan border merah pada form NIK (Validasi HTML5 & JS jalan).
* [x] Coba daftar dua kali pakai NIK yang sama persis. **Hasil:** Sistem menampilkan pesan error "NIK sudah terdaftar", mencegah duplikasi data siswa.

### 3. Performa & Stabilitas
* [x] Spam klik tombol "Daftar" pas form lagi proses loading submit. **Hasil:** Sempat terjadi duplikasi data di database pada percobaan pertama. Masalah langsung diatasi dengan menambahkan fungsi *disable button* setelah klik pertama di frontend.
* [x] Buka web pendaftaran lewat browser HP (Mobile view). **Hasil:** Responsif, form menyesuaikan ukuran layar dan tombol tidak ada yang bertumpuk.

### 4. User Experience (UX)
* [x] Cek bahasa notifikasi error saat salah isi form. **Hasil:** Bahasanya santun dan mudah dipahami oleh orang tua calon siswa.
* [x] Memastikan kontras warna tombol utama. **Hasil:** Tombol daftar menggunakan warna yang kontras sehingga mudah ditemukan oleh pendaftar.
