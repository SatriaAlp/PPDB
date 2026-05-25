# Decision Table Testing

## Deskripsi

Decision Table Testing adalah model black box testing yang digunakan untuk menguji kombinasi beberapa kondisi dan aksi. Pada Sistem PPDB TKQ AS-SALAM, model ini cocok digunakan pada proses login dan proses seleksi otomatis siswa, karena sistem memberikan output berdasarkan beberapa kondisi input.

---

## Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|---|---|---|---|
| 1 | Login | `controllers/auth.php` | Validasi username, password, dan role pengguna |
| 2 | Pendaftaran | `controllers/pendaftaran.php` | Penentuan status seleksi berdasarkan umur siswa |
| 3 | Dashboard | `views/dashboard_wali.php` | Menampilkan status pendaftaran dan riwayat |

---

## Tabel Decision Table Login

| Kondisi / Aksi | TC01 | TC02 | TC03 | TC04 |
|---|---|---|---|---|
| Username pegawai ditemukan | Ya | Tidak | Tidak | Tidak |
| Password pegawai benar | Ya | Tidak | Tidak | Tidak |
| Username wali ditemukan | Tidak | Ya | Tidak | Tidak |
| Password wali benar | Tidak | Ya | Tidak | Tidak |
| Username/password salah | Tidak | Tidak | Ya | Tidak |
| Field login kosong | Tidak | Tidak | Tidak | Ya |
| Redirect ke dashboard admin | Ya | Tidak | Tidak | Tidak |
| Redirect ke dashboard wali | Tidak | Ya | Tidak | Tidak |
| Redirect kembali ke login | Tidak | Tidak | Ya | Ya |
| Pesan error login tampil | Tidak | Tidak | Ya | Ya |

---

## Tabel Decision Table Seleksi Siswa

| Kondisi / Aksi | TC05 | TC06 | TC07 |
|---|---|---|---|
| Data siswa lengkap | Ya | Ya | Ya |
| Umur siswa kurang dari 4 tahun | Ya | Tidak | Tidak |
| Umur siswa sama dengan 4 tahun | Tidak | Ya | Tidak |
| Umur siswa lebih dari 4 tahun | Tidak | Tidak | Ya |
| Status `Tidak Diterima` | Ya | Tidak | Tidak |
| Status `Diterima` | Tidak | Ya | Ya |
| Keterangan `Umur tidak memenuhi syarat` | Ya | Tidak | Tidak |
| Keterangan `Usia memenuhi syarat` | Tidak | Ya | Ya |

---

## Kesimpulan

Decision Table Testing menunjukkan bahwa sistem memiliki beberapa keputusan utama, yaitu keputusan saat login berdasarkan role pengguna dan keputusan status seleksi siswa berdasarkan umur.

