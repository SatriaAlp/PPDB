# Endurance Testing

## Deskripsi

Endurance Testing adalah model black box testing yang dilakukan dengan menjalankan kasus uji secara berulang dalam jumlah tertentu. Pada Sistem PPDB TKQ AS-SALAM, model ini dapat digunakan karena sistem memiliki fitur upload foto siswa, upload akta kelahiran, upload kartu keluarga, pendaftaran siswa, login, logout, dan pembayaran.

Pengujian ini dibuat karena pada sistem terdapat data gambar atau file, yaitu foto siswa serta dokumen akta dan kartu keluarga. Dashboard wali juga menampilkan foto siswa dan link dokumen yang telah diunggah.

---

## Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|---|---|---|---|
| 1 | Login dan Logout | `views/login.php`, `controllers/auth.php`, `controllers/logout.php` | Pengujian session secara berulang |
| 2 | Pendaftaran Siswa | `views/register.php`, `controllers/pendaftaran.php` | Input data siswa dan upload dokumen berulang |
| 3 | Dashboard Wali | `views/dashboard_wali.php` | Menampilkan foto siswa, akta, KK, status, dan riwayat |
| 4 | Pembayaran | `views/form_pembayaran.php` | Proses pembayaran berulang |
| 5 | Upload Dokumen | `uploads/foto/`, `uploads/akta/`, `uploads/kk/` | Penyimpanan file gambar dan dokumen |

---

## Tabel Endurance Testing

| No | Modul | Pengujian Berulang | Jumlah Pengulangan | Expected Output | Actual Output | Test Case | Status |
|---|---|---|---|---|---|---|---|
| 1 | Login dan Logout | Login dan logout akun wali secara berulang | 20 kali | Session tetap normal dan tidak error | Sesuai expected output | TC01 | Valid |
| 2 | Pendaftaran Siswa | Input data siswa lengkap secara berulang menggunakan akun berbeda | 10 kali | Semua data siswa berhasil tersimpan | Sesuai expected output | TC02 | Valid |
| 3 | Upload Foto Siswa | Upload foto siswa `.jpg/.png` secara berulang | 10 kali | Foto tersimpan dan tampil di dashboard wali | Sesuai expected output | TC03 | Valid |
| 4 | Upload Akta | Upload akta kelahiran `.pdf/.jpg/.png` secara berulang | 10 kali | File tersimpan dan link akta dapat dibuka | Sesuai expected output | TC04 | Valid |
| 5 | Upload Kartu Keluarga | Upload KK `.pdf/.jpg/.png` secara berulang | 10 kali | File tersimpan dan link KK dapat dibuka | Sesuai expected output | TC05 | Valid |
| 6 | Pembayaran | Input pembayaran tagihan secara berulang | 10 kali | Riwayat pembayaran bertambah dan tersimpan | Sesuai expected output | TC06 | Valid |
| 7 | Dashboard Wali | Membuka dashboard wali berulang setelah data tersimpan | 20 kali | Data anak, foto, dokumen, status, dan riwayat tetap tampil | Sesuai expected output | TC07 | Valid |

---

## Kesimpulan

Endurance Testing dapat diterapkan pada Sistem PPDB TKQ AS-SALAM karena sistem memiliki fitur upload gambar dan dokumen. Fokus pengujian adalah memastikan sistem tetap stabil ketika proses login, pendaftaran, upload file, pembayaran, dan pembukaan dashboard dilakukan berulang kali.

