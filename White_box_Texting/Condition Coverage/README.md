# Condition Coverage

## Deskripsi
Condition Coverage adalah teknik white box testing yang digunakan untuk memastikan setiap kondisi logika pada program telah diuji dalam dua kemungkinan hasil, yaitu true dan false. Pengujian ini dilakukan untuk mengetahui apakah setiap percabangan pada sistem berjalan sesuai dengan logika yang telah dirancang.

---

# Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|----|--------|---------------|-----------------|
| 1 | Login | `auth.php` | Validasi username, password, dan role pengguna |
| 2 | Pendaftaran | `pendaftaran.php` | Validasi data pendaftaran dan upload dokumen |
| 3 | Pembayaran | `pembayaran.php` | Validasi pembayaran dan penyimpanan transaksi |

---

# Tabel Condition Coverage

| No | Modul | Kondisi yang Diuji | Kondisi True | Kondisi False | Test Case | Status |
|----|--------|-------------------|---------------|----------------|------------|--------|
| 1 | Login | Request menggunakan POST | Data login diproses | Redirect ke login | TC01 | Valid |
| 2 | Login | Username pegawai ditemukan | Masuk validasi password pegawai | Cek akun wali | TC02 | Valid |
| 3 | Login | Password pegawai benar | Redirect dashboard admin | Login gagal | TC03 | Valid |
| 4 | Login | Username wali ditemukan | Validasi password wali | Login gagal | TC04 | Valid |
| 5 | Login | Password wali benar | Redirect dashboard wali | Login gagal | TC05 | Valid |
| 6 | Pendaftaran | Form dikirim | Proses validasi data | Form tidak diproses | TC06 | Valid |
| 7 | Pendaftaran | Semua field wajib terisi | Data diproses | Tampil pesan error | TC07 | Valid |
| 8 | Pendaftaran | File upload berhasil | Data disimpan | Gagal upload file | TC08 | Valid |
| 9 | Pendaftaran | Nilai memenuhi syarat | Status diterima | Status tidak diterima | TC09 | Valid |
| 10 | Pembayaran | Request POST diterima | Proses pembayaran | Redirect halaman | TC10 | Valid |
| 11 | Pembayaran | Nominal pembayaran valid | Simpan transaksi | Tampil error pembayaran | TC11 | Valid |
| 12 | Pembayaran | Bukti pembayaran diupload | Data pembayaran tersimpan | Upload gagal | TC12 | Valid |
| 13 | Pembayaran | Query database berhasil | Pembayaran sukses | Transaksi gagal | TC13 | Valid |
| 14 | Pembayaran | Data siswa ditemukan | Proses pembayaran dilanjutkan | Error data tidak ditemukan | TC14 | Valid |
| 15 | Pembayaran | Status pembayaran berhasil | Redirect sukses | Redirect gagal | TC15 | Valid |

---


# Kesimpulan

Berdasarkan hasil pengujian menggunakan metode Condition Coverage pada modul login, pendaftaran, dan pembayaran, seluruh kondisi logika pada sistem telah diuji pada kondisi true dan false. Hasil pengujian menunjukkan bahwa sistem PPDB mampu menjalankan proses autentikasi, pendaftaran, serta pembayaran sesuai dengan alur yang diharapkan tanpa ditemukan kesalahan logika pada kondisi yang diuji.

Dengan demikian, pengujian Condition Coverage pada sistem PPDB dinyatakan berhasil dan seluruh modul utama sistem dapat berjalan dengan baik.
