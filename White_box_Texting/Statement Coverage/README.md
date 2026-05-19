# Statement Coverage

## Deskripsi
Statement Coverage adalah teknik white box testing yang digunakan untuk memastikan seluruh statement atau baris program pada sistem telah dieksekusi minimal satu kali selama proses pengujian.

Pengujian ini bertujuan untuk mengetahui apakah seluruh perintah dalam program dapat dijalankan dengan baik tanpa menghasilkan error.

Pada modul `pendaftaran.php`, statement coverage dilakukan pada proses:
- validasi data,
- upload dokumen,
- proses seleksi,
- penyimpanan data,
- dan penentuan hasil pendaftaran.

---

# Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|----|--------|---------------|-----------------|
| 1 | Pendaftaran | `pendaftaran.php` | Eksekusi seluruh statement program |

---

# Statement yang Diuji

| No | Statement Program | Fungsi |
|----|-------------------|---------|
| 1 | Input data form | Mengambil data pendaftaran |
| 2 | Validasi field | Mengecek kelengkapan data |
| 3 | Validasi upload file | Mengecek dokumen pendaftaran |
| 4 | Upload dokumen | Menyimpan file ke server |
| 5 | Perhitungan nilai | Menghitung hasil seleksi |
| 6 | Penentuan status | Menentukan diterima/tidak |
| 7 | Simpan database | Menyimpan data siswa |
| 8 | Redirect hasil | Menampilkan hasil pendaftaran |
| 9 | Tampilkan error | Menampilkan pesan kesalahan |

---

# Skenario Pengujian

## 1. Data Pendaftaran Valid

### Kondisi
- Semua field diisi lengkap
- Upload dokumen berhasil
- Nilai memenuhi syarat

### Statement yang Dieksekusi
- Input data
- Validasi field
- Upload file
- Hitung nilai
- Simpan database
- Redirect hasil

### Hasil yang Diharapkan
- Data berhasil disimpan
- Status diterima

---

## 2. Field Kosong

### Kondisi
- Ada data yang belum diisi

### Statement yang Dieksekusi
- Input data
- Validasi field
- Tampilkan error

### Hasil yang Diharapkan
- Sistem menampilkan error validasi

---

## 3. Upload Dokumen Gagal

### Kondisi
- File tidak berhasil diupload

### Statement yang Dieksekusi
- Input data
- Validasi field
- Validasi upload
- Tampilkan error

### Hasil yang Diharapkan
- Sistem menampilkan error upload

---

## 4. Tidak Lulus Seleksi

### Kondisi
- Nilai tidak memenuhi syarat

### Statement yang Dieksekusi
- Input data
- Validasi field
- Upload file
- Hitung nilai
- Penentuan status

### Hasil yang Diharapkan
- Status tidak diterima

---

# Tabel Statement Coverage

| Test Case | Statement yang Diuji | Hasil yang Diharapkan | Status |
|------------|----------------------|------------------------|--------|
| SC01 | Input data form | Data berhasil dibaca | Valid |
| SC02 | Validasi field | Validasi berjalan | Valid |
| SC03 | Validasi upload file | File tervalidasi | Valid |
| SC04 | Upload dokumen | File berhasil diupload | Valid |
| SC05 | Perhitungan nilai | Nilai berhasil dihitung | Valid |
| SC06 | Penentuan status | Status diterima/tidak diterima | Valid |
| SC07 | Simpan database | Data berhasil tersimpan | Valid |
| SC08 | Redirect hasil | Halaman hasil tampil | Valid |
| SC09 | Tampilkan error | Error tampil dengan benar | Valid |

---

# Persentase Statement Coverage

## Rumus

```text
Statement Coverage =
(Jumlah statement yang dieksekusi / Total statement) x 100%
```

---

## Perhitungan

```text
Statement dieksekusi = 9
Total statement = 9
```

```text
Statement Coverage = (9 / 9) x 100%
Statement Coverage = 100%
```



---

# Kesimpulan

Berdasarkan hasil pengujian menggunakan metode Statement Coverage pada modul `pendaftaran.php`, seluruh statement atau baris program telah berhasil dieksekusi minimal satu kali selama proses pengujian.

Hasil pengujian menunjukkan bahwa seluruh proses pada sistem pendaftaran berjalan sesuai dengan logika program yang dirancang tanpa ditemukan statement yang gagal dijalankan.

Persentase statement coverage pada modul pendaftaran mencapai 100%, sehingga seluruh statement program telah berhasil diuji secara menyeluruh.
