# Sample Testing

## Deskripsi

Sample Testing adalah model black box testing yang dilakukan dengan mengambil beberapa contoh data dari kelompok input tertentu. Pada Sistem PPDB TKQ AS-SALAM, sampel data diambil dari data wali siswa, data siswa, dokumen pendaftaran, dan pembayaran.

---

## Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|---|---|---|---|
| 1 | Registrasi Akun Wali | `views/register_akun.php` | Sampel data wali |
| 2 | Pendaftaran Siswa | `views/register.php` | Sampel data siswa |
| 3 | Upload Dokumen | `views/register.php` | Sampel file foto, akta, dan KK |
| 4 | Pembayaran | `views/form_pembayaran.php` | Sampel nominal dan metode pembayaran |

---

## Tabel Sample Testing

| No | Modul | Sampel Data | Expected Output | Actual Output | Test Case | Status |
|---|---|---|---|---|---|---|
| 1 | Registrasi Akun Wali | Nama: Ahmad, NIK: 3201010101010001, JK: Laki-laki, username: ahmad01 | Akun wali berhasil dibuat | Sesuai expected output | TC01 | Valid |
| 2 | Registrasi Akun Wali | Nama: Siti, NIK: 3201010101010002, JK: Perempuan, username: siti01 | Akun wali berhasil dibuat | Sesuai expected output | TC02 | Valid |
| 3 | Pendaftaran Siswa | Nama: Andi, NIK: 3201010101011001, umur: 4 tahun | Data siswa tersimpan dan status `Diterima` | Sesuai expected output | TC03 | Valid |
| 4 | Pendaftaran Siswa | Nama: Budi, NIK: 3201010101011002, umur: 3 tahun | Data siswa tersimpan dan status `Tidak Diterima` | Sesuai expected output | TC04 | Valid |
| 5 | Upload Dokumen | Foto: `siswa.png`, Akta: `akta.pdf`, KK: `kk.pdf` | File berhasil diunggah dan dapat dilihat | Sesuai expected output | TC05 | Valid |
| 6 | Pembayaran | Nominal: 500000, metode: Transfer Bank | Pembayaran berhasil tersimpan | Sesuai expected output | TC06 | Valid |
| 7 | Pembayaran | Nominal: 250000, metode: Tunai | Pembayaran berhasil tersimpan | Sesuai expected output | TC07 | Valid |

---

## Kesimpulan

Sample Testing menunjukkan bahwa sistem dapat memproses beberapa contoh data yang mewakili input utama pada PPDB, mulai dari akun wali, data siswa, dokumen, sampai pembayaran.

