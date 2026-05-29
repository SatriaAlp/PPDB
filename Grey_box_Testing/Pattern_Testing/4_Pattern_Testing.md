# Pengujian 4: Pattern Testing (Exploratory)
**Fokus:** Mencari bug dengan cara eksplorasi sistem PPDB tanpa script test yang terlalu kaku.

### 1. Uji Fungsional Dasar
- Coba isi form pendaftaran dari awal sampai akhir, pastiin masuk ke database.
- Login admin, coba ubah status pendaftaran anak dari "Pending" jadi "Diterima".
- Hapus satu data testing, pastiin datanya gak nyangkut di relasi tabel lain.

### 2. Nyari Bug (Edge Cases / Skenario Aneh)
- Coba masukin nama pakai emoji atau simbol (misal: `Budi @#$`).
- NIK sengaja dikosongin atau diisi huruf, terus coba paksa klik submit form.
- Coba daftar pakai NIK yang udah pernah didaftarin (seharusnya dicegah sistem supaya gak duplikat).

### 3. Performa & Stabilitas
- Spam klik tombol "Daftar" pas form lagi loading, buat ngecek datanya ke-input dobel atau nggak.
- Buka web admin lewat HP, cek tabel datanya kepotong atau masih bisa digeser (responsif).

### 4. User Experience (UX)
- Cek notifikasi error pas form ada yang salah diisi. Bahasanya gampang dimengerti gak sama orang tua wali?
- Pastiin warna tombol utama kelihatan jelas dan gak nyaru sama background form.
