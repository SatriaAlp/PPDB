# 4. Pattern Testing (Exploratory Testing)
**Pendekatan:** Eksplorasi sistem PPDB TKQ AS-SALAM secara kreatif untuk mengidentifikasi bug pada skenario yang mungkin terlewat oleh pengujian terstruktur.

## A. Menguji Fungsional Dasar
Fokus pada alur utama yang paling sering digunakan oleh pendaftar dan admin.
* [ ] Membuka halaman utama form pendaftaran PPDB dan memastikan UI dirender sempurna.
* [ ] Mencoba mengisi seluruh form pendaftaran dengan data valid dan memastikan data tersimpan ke database.
* [ ] Membuka dashboard Admin, mengedit data pendaftar (misal: mengubah status menjadi "Diterima"), lalu menyimpan perubahan.
* [ ] Menghapus salah satu data uji pendaftar dari tabel admin dan memastikan data benar-benar hilang dari sistem.

## B. Menguji Batasan & Skenario Tidak Terduga (Edge Cases)
Memberikan input ekstrem atau aneh untuk melihat apakah sistem memiliki validasi keamanan yang baik.
* [ ] Mengisi kolom "Nama Lengkap" dengan ribuan karakter untuk mengecek batas maksimal input (Varchar limit).
* [ ] Memasukkan angka atau simbol (seperti `@#$%`) pada kolom yang seharusnya hanya berisi huruf (misal: Nama Orang Tua).
* [ ] Mengosongkan isian wajib (seperti NIK atau Tanggal Lahir) lalu memaksa klik tombol "Daftar".
* [ ] Mencoba mendaftarkan siswa dengan NIK yang sama persis dengan siswa yang sudah terdaftar sebelumnya (Cek duplikasi).

## C. Menguji Performa dan Stabilitas
Melihat bagaimana aplikasi PPDB menangani beban kerja.
* [ ] Melakukan *refresh* (F5) berkali-kali secara cepat pada saat proses *submit* form pendaftaran sedang loading.
* [ ] Menambahkan puluhan data pendaftar secara berurutan dalam waktu singkat untuk melihat apakah server *lag*.
* [ ] Membuka sistem admin di berbagai web browser berbeda (Chrome, Firefox, Safari, Edge) untuk mengecek komptabilitas.

## D. Menguji Kegunaan dan Pengalaman Pengguna (UX)
Fokus pada kemudahan penggunaan sistem, baik bagi pendaftar maupun admin.
* [ ] Mengecek apakah pesan *error* (jika form salah isi) mudah dipahami oleh orang tua wali murid.
* [ ] Memastikan warna tombol utama (misal: tombol "Simpan" atau "Daftar") cukup kontras dan mudah dilihat.
* [ ] Menyimulasikan pendaftaran melalui perangkat *mobile* (HP) untuk memastikan website responsif dan tidak terpotong.
