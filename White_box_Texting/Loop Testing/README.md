# Loop Testing

## Deskripsi
Loop Testing adalah teknik white box testing yang digunakan untuk menguji struktur perulangan (loop) pada program. Pengujian ini bertujuan untuk memastikan proses perulangan berjalan dengan benar dan tidak menyebabkan:
- infinite loop,
- kesalahan iterasi,
- kesalahan validasi data,
- maupun kegagalan proses penyimpanan data.

Pada modul `pendaftaran.php`, proses loop digunakan pada:
- validasi data form,
- pengecekan field input,
- proses upload dokumen,
- serta proses seleksi data siswa.

---

# Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|----|--------|---------------|-----------------|
| 1 | Pendaftaran | `pendaftaran.php` | Perulangan validasi dan pemrosesan data siswa |

---

# Jenis Loop yang Digunakan

| Jenis Loop | Fungsi |
|-------------|---------|
| `foreach` | Digunakan untuk membaca data field form |
| `while` | Digunakan pada proses query database |
| Iterasi validasi | Digunakan untuk pengecekan data input |
| Iterasi upload | Digunakan untuk memproses file dokumen |

---

# Skenario Loop Testing

## 1. Zero Iteration

### Deskripsi
Perulangan tidak dijalankan karena form pendaftaran kosong atau data tidak dikirim.

### Kondisi
- User membuka halaman tanpa mengirim form.

### Hasil yang Diharapkan
- Sistem tidak memproses data.
- Tidak terjadi error pada sistem.

---

## 2. One Iteration

### Deskripsi
Perulangan dijalankan satu kali karena hanya terdapat satu data input yang diproses.

### Kondisi
- User mengisi satu data pendaftaran.

### Hasil yang Diharapkan
- Data berhasil divalidasi.
- Sistem melanjutkan proses pendaftaran.

---

## 3. Multiple Iteration

### Deskripsi
Perulangan dijalankan lebih dari satu kali untuk memproses beberapa field dan dokumen.

### Kondisi
- User mengisi seluruh field form.
- Upload beberapa dokumen dilakukan.

### Hasil yang Diharapkan
- Seluruh data berhasil dibaca.
- Validasi berjalan dengan baik.
- Tidak ada data yang terlewat.

---

## 4. Maximum Iteration

### Deskripsi
Perulangan diuji dengan jumlah data maksimum.

### Kondisi
- Sistem menerima banyak data input dan dokumen.

### Hasil yang Diharapkan
- Sistem tetap stabil.
- Tidak terjadi infinite loop.
- Seluruh data tetap diproses dengan baik.

---

# Tabel Loop Testing

| Test Case | Jenis Iterasi | Skenario | Hasil yang Diharapkan | Status |
|------------|----------------|-----------|------------------------|--------|
| LT01 | Zero Iteration | Form tidak dikirim | Sistem tidak memproses data | Valid |
| LT02 | One Iteration | Satu data siswa diproses | Pendaftaran berhasil | Valid |
| LT03 | Multiple Iteration | Banyak field dan dokumen diproses | Data tervalidasi seluruhnya | Valid |
| LT04 | Maximum Iteration | Data pendaftaran sangat banyak | Sistem tetap stabil | Valid |

---

# Alur Pengujian Loop

| No | Proses |
|----|---------|
| 1 | User mengisi form pendaftaran |
| 2 | Sistem membaca seluruh field input |
| 3 | Loop melakukan validasi data |
| 4 | Sistem memproses upload dokumen |
| 5 | Sistem menghitung nilai seleksi |
| 6 | Sistem menentukan status diterima |
| 7 | Data disimpan ke database |
| 8 | Sistem menampilkan hasil pendaftaran |

---


---

# Kesimpulan

Berdasarkan hasil pengujian menggunakan metode Loop Testing pada modul `pendaftaran.php`, seluruh proses perulangan telah berjalan sesuai dengan logika program yang dirancang.

Pengujian zero iteration, one iteration, multiple iteration, dan maximum iteration menunjukkan bahwa sistem mampu menangani proses validasi data, upload dokumen, serta penyimpanan data pendaftaran dengan baik tanpa terjadi infinite loop maupun kesalahan iterasi.

Dengan demikian, proses loop pada modul pendaftaran dinyatakan berjalan dengan baik dan stabil.
