# Comparison Testing

## Deskripsi

Comparison Testing adalah model black box testing yang digunakan untuk membandingkan hasil keluaran pada beberapa bagian sistem. Pada Sistem PPDB TKQ AS-SALAM, model ini digunakan untuk memastikan data yang diinput oleh wali siswa sama dengan data yang ditampilkan pada dashboard wali dan dashboard admin.

---

## Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|---|---|---|---|
| 1 | Pendaftaran Siswa | `views/register.php` | Input data siswa dan dokumen |
| 2 | Dashboard Wali | `views/dashboard_wali.php` | Menampilkan data anak, status, tagihan, dan riwayat pembayaran |
| 3 | Dashboard Admin | `views/dashboard_admin.php` | Menampilkan data pendaftaran dan data siswa |
| 4 | Pembayaran | `views/form_pembayaran.php` | Input data pembayaran |
| 5 | Riwayat Pembayaran | `views/dashboard_wali.php` | Menampilkan data pembayaran wali |

---

## Tabel Comparison Testing

| No | Data yang Dibandingkan | Sumber Data 1 | Sumber Data 2 | Expected Output | Actual Output | Test Case | Status |
|---|---|---|---|---|---|---|---|
| 1 | Nama siswa | Form pendaftaran siswa | Dashboard wali | Nama siswa tampil sama | Sesuai expected output | TC01 | Valid |
| 2 | NIK siswa | Form pendaftaran siswa | Dashboard wali | NIK siswa tampil sama | Sesuai expected output | TC02 | Valid |
| 3 | Umur siswa | Form pendaftaran siswa | Dashboard wali | Umur siswa tampil sama | Sesuai expected output | TC03 | Valid |
| 4 | Status seleksi | Proses pendaftaran | Dashboard wali | Status seleksi tampil sesuai umur siswa | Sesuai expected output | TC04 | Valid |
| 5 | File akta dan KK | Upload dokumen | Link dokumen di dashboard wali | File dapat dibuka sesuai dokumen yang diunggah | Sesuai expected output | TC05 | Valid |
| 6 | Nominal pembayaran | Form pembayaran | Riwayat pembayaran | Nominal pembayaran tampil sama | Sesuai expected output | TC06 | Valid |
| 7 | Metode pembayaran | Form pembayaran | Riwayat pembayaran | Metode pembayaran tampil sama | Sesuai expected output | TC07 | Valid |

---

## Kesimpulan

Comparison Testing memastikan bahwa data yang dimasukkan melalui form tidak berubah ketika ditampilkan pada halaman lain. Pengujian ini penting karena Sistem PPDB memiliki beberapa tampilan yang menggunakan data yang sama, seperti data siswa, status seleksi, dokumen, dan pembayaran.

