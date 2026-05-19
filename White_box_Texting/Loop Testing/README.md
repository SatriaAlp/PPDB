# Loop Testing

## Deskripsi
Loop Testing adalah teknik white box testing yang digunakan untuk menguji struktur perulangan (loop) pada program. Pengujian dilakukan untuk memastikan proses perulangan berjalan dengan benar dan tidak menyebabkan:
- infinite loop,
- kesalahan iterasi,
- ataupun proses yang tidak sesuai logika program.

Pada modul login (`auth.php`), loop digunakan pada proses pengecekan data pengguna dan validasi autentikasi.

---

# Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|----|--------|---------------|-----------------|
| 1 | Login | `auth.php` | Perulangan proses validasi data pengguna |

---

# Jenis Loop yang Digunakan

| Jenis Loop | Fungsi |
|-------------|---------|
| `foreach` | Digunakan untuk membaca data hasil query pengguna |
| `while` | Digunakan dalam proses pengambilan data database |
| Iterasi validasi | Digunakan untuk pengecekan data login |

---

# Skenario Loop Testing

## 1. Zero Iteration

### Deskripsi
Perulangan tidak dijalankan karena data pengguna tidak ditemukan.

### Kondisi
- Username tidak tersedia di database.

### Hasil yang Diharapkan
- Sistem menampilkan login gagal.
- Loop tidak dijalankan.

---

## 2. One Iteration

### Deskripsi
Perulangan dijalankan satu kali karena hanya ada satu data pengguna yang ditemukan.

### Kondisi
- Username ditemukan satu data.

### Hasil yang Diharapkan
- Sistem memvalidasi password.
- Login berhasil jika password benar.

---

## 3. Multiple Iteration

### Deskripsi
Perulangan dijalankan lebih dari satu kali untuk membaca data pengguna.

### Kondisi
- Terdapat lebih dari satu data hasil query.

### Hasil yang Diharapkan
- Sistem membaca seluruh data.
- Validasi dilakukan tanpa error.

---

## 4. Maximum Iteration

### Deskripsi
Perulangan diuji pada jumlah data maksimum.

### Kondisi
- Database memiliki banyak data pengguna.

### Hasil yang Diharapkan
- Sistem tetap berjalan stabil.
- Tidak terjadi infinite loop.
- Proses login tetap berhasil.

---

# Tabel Loop Testing

| Test Case | Jenis Iterasi | Skenario | Hasil yang Diharapkan | Status |
|------------|----------------|-----------|------------------------|--------|
| LT01 | Zero Iteration | Username tidak ditemukan | Login gagal | Valid |
| LT02 | One Iteration | Satu akun ditemukan | Login berhasil | Valid |
| LT03 | Multiple Iteration | Banyak data pengguna | Data terbaca seluruhnya | Valid |
| LT04 | Maximum Iteration | Data pengguna sangat banyak | Sistem tetap stabil | Valid |

---

# Alur Pengujian Loop

| No | Proses |
|----|---------|
| 1 | Input username dan password |
| 2 | Sistem melakukan query database |
| 3 | Loop membaca data pengguna |
| 4 | Validasi password dilakukan |
| 5 | Sistem menentukan status login |
| 6 | Redirect dashboard atau login gagal |

---


---

# Kesimpulan

Berdasarkan hasil pengujian menggunakan metode Loop Testing pada modul login (`auth.php`), seluruh proses perulangan telah berjalan sesuai dengan logika program yang dirancang.

Pengujian zero iteration, one iteration, multiple iteration, dan maximum iteration menunjukkan bahwa sistem mampu menangani proses validasi pengguna dengan baik tanpa terjadi infinite loop maupun kesalahan iterasi.

Dengan demikian, proses loop pada modul login dinyatakan berjalan dengan baik dan stabil.
