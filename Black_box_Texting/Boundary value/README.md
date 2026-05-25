# Boundary Value Analysis

## Deskripsi

Boundary Value Analysis adalah model black box testing yang digunakan untuk menguji nilai batas dari suatu input. Pada Sistem PPDB TKQ AS-SALAM, model ini digunakan untuk menguji batas umur siswa pada proses pendaftaran, karena sistem menentukan status seleksi otomatis berdasarkan umur siswa.

---

## Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|---|---|---|---|
| 1 | Pendaftaran Siswa | `views/register.php` | Validasi input umur siswa dan dokumen pendaftaran |
| 2 | Proses Pendaftaran | `controllers/pendaftaran.php` | Penentuan status seleksi otomatis berdasarkan umur |
| 3 | Dashboard Wali | `views/dashboard_wali.php` | Menampilkan hasil status pendaftaran siswa |

---

## Tabel Boundary Value Analysis

| No | Modul | Kondisi yang Diuji | Data Uji | Expected Output | Actual Output | Test Case | Status |
|---|---|---|---|---|---|---|---|
| 1 | Pendaftaran | Umur siswa berada di bawah batas minimum | Umur = 3 tahun | Data tersimpan dan status menjadi `Tidak Diterima` | Sesuai expected output | TC01 | Valid |
| 2 | Pendaftaran | Umur siswa tepat pada batas minimum | Umur = 4 tahun | Data tersimpan dan status menjadi `Diterima` | Sesuai expected output | TC02 | Valid |
| 3 | Pendaftaran | Umur siswa di atas batas minimum | Umur = 5 tahun | Data tersimpan dan status menjadi `Diterima` | Sesuai expected output | TC03 | Valid |
| 4 | Pendaftaran | Umur siswa sangat kecil | Umur = 1 tahun | Data diproses dan status menjadi `Tidak Diterima` | Sesuai expected output | TC04 | Valid |
| 5 | Pendaftaran | Umur siswa jauh di atas batas minimum | Umur = 6 tahun | Data diproses dan status menjadi `Diterima` | Sesuai expected output | TC05 | Valid |

---

## Kesimpulan

Pengujian Boundary Value Analysis pada Sistem PPDB berfokus pada batas umur siswa. Berdasarkan skenario uji, batas utama sistem adalah umur 4 tahun. Jika umur siswa kurang dari 4 tahun maka status menjadi `Tidak Diterima`, sedangkan umur 4 tahun atau lebih akan menghasilkan status `Diterima`.

