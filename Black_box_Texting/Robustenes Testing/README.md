# Robustness Testing

## Deskripsi

Robustness Testing adalah model black box testing yang digunakan untuk menguji ketahanan sistem ketika menerima input yang tidak normal atau berada di luar spesifikasi. Pada Sistem PPDB TKQ AS-SALAM, pengujian ini dilakukan pada fitur login, registrasi akun, pendaftaran siswa, upload dokumen, dan pembayaran.

---

## Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|---|---|---|---|
| 1 | Login | `views/login.php` dan `controllers/auth.php` | Ketahanan sistem terhadap username/password tidak normal |
| 2 | Registrasi Akun | `views/register_akun.php` dan `controllers/register_akun.php` | Validasi input akun wali |
| 3 | Pendaftaran Siswa | `views/register.php` dan `controllers/pendaftaran.php` | Validasi umur dan dokumen tidak normal |
| 4 | Pembayaran | `views/form_pembayaran.php` | Validasi nominal dan metode pembayaran |

---

## Tabel Robustness Testing

| No | Modul | Input Tidak Normal | Expected Output | Actual Output | Test Case | Status |
|---|---|---|---|---|---|---|
| 1 | Login | Username dan password diisi karakter sangat panjang | Sistem tidak error dan login ditolak | Sesuai expected output | TC01 | Valid |
| 2 | Login | Username diisi simbol acak seperti `@@@@@` | Sistem menampilkan pesan login gagal | Sesuai expected output | TC02 | Valid |
| 3 | Registrasi Akun | Nama wali diisi script `<script>alert(1)</script>` | Sistem tidak menjalankan script dan data tidak merusak tampilan | Sesuai expected output | TC03 | Valid |
| 4 | Pendaftaran Siswa | Umur siswa diisi `-1` | Sistem tidak crash dan data tidak seharusnya diterima sebagai data valid | Sesuai expected output | TC04 | Valid |
| 5 | Pendaftaran Siswa | NIK siswa diisi huruf | Sistem menolak atau tidak memproses data sebagai NIK valid | Sesuai expected output | TC05 | Valid |
| 6 | Upload Dokumen | Upload file selain ketentuan, misalnya `.exe` | Sistem menolak file yang tidak sesuai format | Sesuai expected output | TC06 | Valid |
| 7 | Pembayaran | Nominal pembayaran diisi huruf `abcde` | Sistem menampilkan pesan nominal pembayaran tidak valid | Sesuai expected output | TC07 | Valid |
| 8 | Pembayaran | Nominal pembayaran diisi nilai negatif | Sistem tidak seharusnya menerima nominal negatif | Sesuai expected output | TC08 | Valid |

---

## Kesimpulan

Robustness Testing memastikan sistem tetap stabil dan tidak mengalami error ketika pengguna memasukkan data yang tidak sesuai. Pengujian ini penting untuk menjaga keamanan dan keandalan Sistem PPDB.

