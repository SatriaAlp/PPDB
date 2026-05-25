# Equivalence Partitioning

## Deskripsi

Equivalence Partitioning adalah model black box testing yang membagi data masukan ke dalam beberapa kelas, yaitu kelas data valid dan kelas data tidak valid. Pada Sistem PPDB TKQ AS-SALAM, pengujian ini digunakan pada form registrasi akun wali, form pendaftaran siswa, upload dokumen, login, dan pembayaran.

---

## Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|---|---|---|---|
| 1 | Registrasi Akun Wali | `views/register_akun.php` | Validasi data akun wali |
| 2 | Login | `views/login.php` | Validasi username dan password |
| 3 | Pendaftaran Siswa | `views/register.php` | Validasi data siswa dan upload dokumen |
| 4 | Pembayaran | `views/form_pembayaran.php` | Validasi tagihan dan nominal pembayaran |

---

## Tabel Equivalence Partitioning

| No | Modul | Kelas Data | Data Uji | Expected Output | Actual Output | Test Case | Status |
|---|---|---|---|---|---|---|---|
| 1 | Registrasi Akun Wali | Valid | Semua field wali diisi lengkap | Akun berhasil dibuat dan diarahkan ke halaman login | Sesuai expected output | TC01 | Valid |
| 2 | Registrasi Akun Wali | Tidak Valid | Username yang sudah digunakan | Sistem menampilkan pesan username sudah dipakai | Sesuai expected output | TC02 | Valid |
| 3 | Login | Valid | Username dan password benar | Sistem masuk ke dashboard sesuai role pengguna | Sesuai expected output | TC03 | Valid |
| 4 | Login | Tidak Valid | Username atau password salah | Sistem menampilkan pesan login gagal | Sesuai expected output | TC04 | Valid |
| 5 | Pendaftaran Siswa | Valid | Data siswa lengkap dan dokumen sesuai format | Data siswa berhasil tersimpan | Sesuai expected output | TC05 | Valid |
| 6 | Pendaftaran Siswa | Tidak Valid | Field wajib dikosongkan | Sistem menolak atau tidak memproses data kosong | Sesuai expected output | TC06 | Valid |
| 7 | Upload Dokumen | Valid | Foto `.jpg/.png`, Akta `.pdf/.jpg/.png`, KK `.pdf/.jpg/.png` | File berhasil diunggah | Sesuai expected output | TC07 | Valid |
| 8 | Pembayaran | Tidak Valid | Nominal diisi huruf | Sistem menampilkan pesan nominal tidak valid | Sesuai expected output | TC08 | Valid |

---

## Kesimpulan

Pengujian Equivalence Partitioning membantu memastikan bahwa sistem dapat membedakan input valid dan tidak valid pada fitur utama PPDB, seperti registrasi akun, login, pendaftaran siswa, upload dokumen, dan pembayaran.

