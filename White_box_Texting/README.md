# White Box Testing — Sistem PPDB TKQ AS-SALAM

## Deskripsi
Folder ini berisi dokumentasi pengujian **White Box Testing** pada Sistem PPDB TKQ AS-SALAM. Pengujian dilakukan dengan menganalisis struktur internal kode program, khususnya pada bagian controller yang menangani proses login, pendaftaran siswa, dan registrasi akun wali siswa.

White Box Testing pada sistem ini berfokus pada logika percabangan, alur eksekusi program, aliran data variabel, serta statement penting yang terdapat pada kode PHP.

---

## Tim Pengujian

| Nama | NIM | Peran |
|---|---|---|
| Diva Rosalinda | 20231310005 | Tester & Dokumentasi |
| Gita Nurcahyani | 20231310006 | Tester & Dokumentasi |
| Gustiar Rifaldi | 20231310031 | Tester & Dokumentasi |
| Satria Alparezi | 20231310017 | Tester & Dokumentasi |

---
## Struktur Folder White Box Testing

| No | Folder | Isi Dokumentasi |
|---|---|---|
| 1 | `Condition Coverage` | Dokumentasi pengujian kondisi true dan false |
| 2 | `Control Flow Testing` | Dokumentasi alur kontrol program |
| 3 | `Data Flow Testing` | Dokumentasi aliran variabel dalam kode |
| 4 | `Decision Coverage` | Dokumentasi pengujian percabangan keputusan |
| 5 | `Loop Testing` | Dokumentasi identifikasi dan pengujian loop |
| 6 | `Path Testing` | Dokumentasi jalur independen dan cyclomatic complexity |
| 7 | `Statement Coverage` | Dokumentasi statement yang diuji |
| 8 | `Whitebox_test_PPDB` | Tempat penyimpanan dokumen hasil pengujian white box |

---


## Modul yang Diuji

| No | Modul | File Program | Fungsi Utama |
|---|---|---|---|
| 1 | Login | `ppdb/controllers/auth.php` | Memproses login pegawai dan wali siswa |
| 2 | Pendaftaran Siswa | `ppdb/controllers/pendaftaran.php` | Memproses pendaftaran siswa baru dan seleksi umur |
| 3 | Registrasi Akun Wali | `ppdb/controllers/register_akun.php` | Memproses pembuatan akun wali siswa |

---

## Ringkasan Logika Kode yang Diuji

### 1. `auth.php` — Modul Login
Modul login menangani proses autentikasi pengguna berdasarkan username dan password. Pada kode ini, sistem melakukan pengecekan terhadap dua jenis pengguna, yaitu pegawai dan wali siswa.

Alur utama:
1. Sistem menerima input `username` dan `password`.
2. Sistem mengecek akun pegawai menggunakan `getByUsernamePegawai($username)`.
3. Jika akun pegawai ditemukan dan `password_verify()` bernilai benar, sistem membuat session pegawai.
4. Pegawai diarahkan ke `dashboard_admin.php`.
5. Jika bukan pegawai, sistem mengecek akun wali siswa menggunakan `getByUsername($username)`.
6. Jika akun wali ditemukan dan password sesuai, sistem membuat session wali.
7. Wali diarahkan ke `dashboard_wali.php`.
8. Jika seluruh proses autentikasi gagal, sistem mengarahkan kembali ke halaman login dengan parameter `login_error=1`.

Session yang digunakan:
- `$_SESSION['login_pegawai']`
- `$_SESSION['user']`
- `$_SESSION['login_wali']`
- `$_SESSION['id_wali']`
- `$_SESSION['nama_wali']`

---

### 2. `pendaftaran.php` — Modul Pendaftaran Siswa
Modul pendaftaran digunakan untuk menyimpan data siswa baru berdasarkan input dari form pendaftaran wali siswa. Data yang diproses meliputi data identitas siswa, data wali, dan berkas pendaftaran.

Alur utama:
1. Sistem mengambil `id_wali`.
2. Sistem menerima input data siswa dari `$_POST`.
3. Sistem mengambil data:
   - `nama_siswa`
   - `nik_siswa`
   - `jenis_kelamin_siswa`
   - `umur_siswa`
   - `alamat_siswa`
4. Sistem memproses nama file:
   - `foto_siswa`
   - `kk_siswa`
   - `akta_kelahiran_siswa`
5. Sistem menyimpan data siswa menggunakan `$siswaModel->register($data_siswa)`.
6. Sistem menentukan status seleksi berdasarkan umur siswa:
   - Jika `umur_siswa >= 4`, status menjadi `Diterima`.
   - Jika `umur_siswa < 4`, status menjadi `Tidak Diterima`.
7. Sistem membuat keterangan seleksi:
   - `Usia memenuhi syarat`
   - `Umur tidak memenuhi syarat`
8. Sistem menyimpan hasil seleksi menggunakan `$hasilSeleksiModel->insert()`.
9. Sistem mengarahkan kembali ke `dashboard_wali.php?register_success=1`.

---

### 3. `register_akun.php` — Modul Registrasi Akun Wali
Modul registrasi akun digunakan untuk membuat akun wali siswa. Pada kode ini, sistem melakukan pengecekan duplikasi username sebelum akun disimpan.

Alur utama:
1. Sistem menerima input data wali dari form registrasi.
2. Sistem menerima data:
   - `nama_wali`
   - `nik_wali`
   - `jenis_kelamin_wali`
   - `alamat_wali`
   - `username_login`
   - `password_login`
3. Sistem mengecek apakah username sudah digunakan menggunakan `getByUsername($username_login)`.
4. Jika username sudah ada, sistem mengarahkan kembali ke halaman register dengan pesan error.
5. Jika username belum digunakan, sistem menyusun array `$data_wali`.
6. Field `hubungan_wali` diisi dengan nilai `null`.
7. Sistem menyimpan akun wali menggunakan `$waliSiswaModel->register($data_wali)`.
8. Setelah akun berhasil dibuat, sistem mengarahkan pengguna ke halaman login dengan parameter `akun_created=1`.
9. Jika request tidak sesuai, sistem mengarahkan kembali ke halaman register.

---

## Teknik White Box Testing yang Digunakan

| No | Teknik Pengujian | Fokus Pengujian | Keterangan |
|---|---|---|---|
| 1 | Condition Coverage | Kondisi logika | Menguji kondisi seperti password sesuai/tidak sesuai, username ada/tidak ada, dan umur memenuhi/tidak memenuhi |
| 2 | Control Flow Testing | Alur eksekusi program | Menguji alur dari input, proses validasi, penyimpanan data, hingga redirect |
| 3 | Data Flow Testing | Aliran variabel | Menguji penggunaan variabel seperti `$username`, `$password`, `$data_siswa`, `$status`, dan `$data_wali` |
| 4 | Decision Coverage | Percabangan keputusan | Menguji hasil true dan false dari percabangan `if/else` dan operator ternary |
| 5 | Loop Testing | Perulangan atau proses berulang | Mengidentifikasi apakah terdapat loop atau pola proses berulang pada kode |
| 6 | Path Testing | Jalur independen | Menguji jalur login pegawai, login wali, login gagal, pendaftaran diterima, pendaftaran tidak diterima, dan register gagal/berhasil |
| 7 | Statement Coverage | Pernyataan kode | Memastikan statement penting pada controller dijalankan minimal satu kali |

---

## Rencana Test Case Berdasarkan Kode

### Modul Login — `auth.php`

| No | Skenario | Kondisi Kode yang Diuji | Expected Result | Status |
|---|---|---|---|---|
| 1 | Login sebagai pegawai dengan data valid | `$pegawai && password_verify(...)` bernilai true | Masuk ke `dashboard_admin.php` | Belum diuji |
| 2 | Login sebagai wali dengan data valid | `$wali && password_verify(...)` bernilai true | Masuk ke `dashboard_wali.php` | Belum diuji |
| 3 | Login dengan password salah | `password_verify(...)` bernilai false | Kembali ke login dengan `login_error=1` | Belum diuji |
| 4 | Login dengan username tidak terdaftar | Data pegawai dan wali tidak ditemukan | Kembali ke login dengan `login_error=1` | Belum diuji |
| 5 | Akses login tanpa request valid | Blok request tidak terpenuhi | Kembali ke halaman login | Belum diuji |

---

### Modul Pendaftaran — `pendaftaran.php`

| No | Skenario | Kondisi Kode yang Diuji | Expected Result | Status |
|---|---|---|---|---|
| 1 | Pendaftaran dengan umur siswa 4 tahun atau lebih | `$_POST['umur_siswa'] >= 4` bernilai true | Status `Diterima` | Belum diuji |
| 2 | Pendaftaran dengan umur siswa kurang dari 4 tahun | `$_POST['umur_siswa'] >= 4` bernilai false | Status `Tidak Diterima` | Belum diuji |
| 3 | Data siswa berhasil disimpan | `$siswaModel->register($data_siswa)` dijalankan | Data siswa tersimpan | Belum diuji |
| 4 | Hasil seleksi berhasil disimpan | `$hasilSeleksiModel->insert(...)` dijalankan | Hasil seleksi tersimpan | Belum diuji |
| 5 | Redirect setelah pendaftaran berhasil | `header('Location: ../views/dashboard_wali.php?register_success=1')` dijalankan | Kembali ke dashboard wali | Belum diuji |

---

### Modul Register Akun — `register_akun.php`

| No | Skenario | Kondisi Kode yang Diuji | Expected Result | Status |
|---|---|---|---|---|
| 1 | Registrasi dengan username baru | `$existingUser` bernilai false | Akun wali berhasil dibuat | Belum diuji |
| 2 | Registrasi dengan username yang sudah ada | `$existingUser` bernilai true | Kembali ke register dengan pesan error | Belum diuji |
| 3 | Password diproses sebelum disimpan | `$password_login` masuk ke `$data_wali` | Password tersimpan pada data akun | Belum diuji |
| 4 | Data wali disusun ke array | `$data_wali` dibuat | Data siap disimpan | Belum diuji |
| 5 | Request registrasi tidak valid | Blok request tidak terpenuhi | Kembali ke halaman register | Belum diuji |

---

## Variabel Penting yang Dianalisis

| No | Variabel | Modul | Fungsi |
|---|---|---|---|
| 1 | `$username` | Login | Menyimpan username dari input login |
| 2 | `$password` | Login | Menyimpan password dari input login |
| 3 | `$pegawai` | Login | Menyimpan hasil pencarian akun pegawai |
| 4 | `$wali` | Login | Menyimpan hasil pencarian akun wali siswa |
| 5 | `$id_wali` | Pendaftaran | Menghubungkan data siswa dengan wali siswa |
| 6 | `$data_siswa` | Pendaftaran | Menyimpan kumpulan data siswa sebelum dikirim ke model |
| 7 | `$id_siswa` | Pendaftaran | Menyimpan ID siswa hasil proses register |
| 8 | `$status` | Pendaftaran | Menyimpan hasil seleksi berdasarkan umur siswa |
| 9 | `$keterangan` | Pendaftaran | Menyimpan keterangan hasil seleksi |
| 10 | `$existingUser` | Register Akun | Menyimpan hasil pengecekan username |
| 11 | `$data_wali` | Register Akun | Menyimpan kumpulan data wali sebelum dikirim ke model |

---

## Status Dokumentasi

| Dokumen | Status |
|---|---|
| Condition Coverage | Belum diisi |
| Control Flow Testing | Belum diisi |
| Data Flow Testing | Belum diisi |
| Decision Coverage | Belum diisi |
| Loop Testing | Belum diisi |
| Path Testing | Belum diisi |
| Statement Coverage | Belum diisi |
| Dokumen Test Case PDF | Belum dilengkapi / menyesuaikan hasil pengujian |

---

## Teknologi yang Digunakan

| Keterangan | Detail |
|---|---|
| Bahasa Pemrograman | PHP Native |
| Database | MySQL |
| Server Lokal | XAMPP / Apache |
| Database Management | phpMyAdmin |
| Metode Verifikasi | Session, redirect header, query database, dan pengecekan hasil input |

---

## Informasi Pengujian

| Keterangan | Detail |
|---|---|
| Mata Kuliah | Software Quality |
| Dosen | Deni Suprihadi, S.T., M.Kom., MCE |
| Program Studi | Teknik Informatika |
| Universitas | Universitas Kebangsaan Republik Indonesia |
| Tanggal Pengujian | Belum ditentukan |

---

## Kesimpulan Sementara
Dokumentasi White Box Testing ini disusun berdasarkan struktur kode pada controller sistem PPDB TKQ AS-SALAM. Pengujian akan difokuskan pada modul login, pendaftaran siswa, dan registrasi akun wali siswa. Setiap teknik pengujian akan dilengkapi secara bertahap berdasarkan hasil analisis kode dan pelaksanaan test case.
