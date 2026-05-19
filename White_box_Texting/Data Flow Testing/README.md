# Data Flow Testing

## Deskripsi
Data Flow Testing adalah teknik white box testing yang digunakan untuk menguji aliran data pada program, mulai dari proses pendefinisian variabel (define), penggunaan variabel (use), hingga penghapusan variabel (kill).

Pengujian ini bertujuan untuk memastikan setiap variabel pada sistem digunakan secara benar dan tidak terjadi:
- variabel tidak terdefinisi,
- variabel tidak digunakan,
- kesalahan aliran data,
- atau penggunaan data yang tidak valid.

---

# Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|----|--------|---------------|-----------------|
| 1 | Login | `auth.php` | Aliran data autentikasi pengguna |
| 2 | Pendaftaran | `pendaftaran.php` | Aliran data pendaftaran siswa |
| 3 | Pembayaran | `pembayaran.php` | Aliran data transaksi pembayaran |

---

# 1. Data Flow Testing Modul Login (`auth.php`)

## Variabel yang Digunakan

| Variabel | Define | Use | Keterangan |
|-----------|--------|-----|-------------|
| `$username` | Input form login | Validasi akun | Menyimpan username pengguna |
| `$password` | Input form login | Validasi password | Menyimpan password pengguna |
| `$pegawai` | Query database | Cek data pegawai | Menyimpan data pegawai |
| `$wali` | Query database | Cek data wali | Menyimpan data wali |
| `$_SESSION` | Setelah login berhasil | Redirect dashboard | Menyimpan session login |

---

## Alur Data

| No | Alur Data |
|----|------------|
| 1 | Input username dan password |
| 2 | Data dikirim ke proses login |
| 3 | Sistem memvalidasi data pengguna |
| 4 | Data pegawai/wali diambil dari database |
| 5 | Session dibuat |
| 6 | Redirect dashboard |

---

## Hasil Pengujian

| Test Case | Skenario | Hasil |
|------------|-----------|--------|
| DF01 | Username valid | Data berhasil diproses |
| DF02 | Password valid | Login berhasil |
| DF03 | Username tidak ditemukan | Login gagal |
| DF04 | Password salah | Login gagal |
| DF05 | Session berhasil dibuat | Redirect dashboard berhasil |

---

# 2. Data Flow Testing Modul Pendaftaran (`pendaftaran.php`)

## Variabel yang Digunakan

| Variabel | Define | Use | Keterangan |
|-----------|--------|-----|-------------|
| `$nama` | Input form | Simpan database | Nama calon siswa |
| `$nisn` | Input form | Validasi data | Nomor induk siswa |
| `$alamat` | Input form | Simpan database | Alamat siswa |
| `$nilai` | Input form | Seleksi penerimaan | Nilai seleksi |
| `$file` | Upload file | Validasi upload | Dokumen pendaftaran |
| `$status` | Hasil seleksi | Tampilkan hasil | Status diterima/tidak |

---

## Alur Data

| No | Alur Data |
|----|------------|
| 1 | Input data pendaftaran |
| 2 | Validasi field form |
| 3 | Upload dokumen |
| 4 | Hitung nilai seleksi |
| 5 | Menentukan status diterima |
| 6 | Menyimpan data ke database |
| 7 | Menampilkan hasil pendaftaran |

---

## Hasil Pengujian

| Test Case | Skenario | Hasil |
|------------|-----------|--------|
| DF06 | Semua field lengkap | Data tersimpan |
| DF07 | Ada field kosong | Validasi gagal |
| DF08 | Upload file berhasil | Dokumen tersimpan |
| DF09 | Upload file gagal | Error upload |
| DF10 | Nilai memenuhi syarat | Status diterima |
| DF11 | Nilai tidak memenuhi syarat | Status tidak diterima |

---

# 3. Data Flow Testing Modul Pembayaran (`pembayaran.php`)

## Variabel yang Digunakan

| Variabel | Define | Use | Keterangan |
|-----------|--------|-----|-------------|
| `$id_siswa` | Input pembayaran | Query database | Identitas siswa |
| `$jumlah_bayar` | Input pembayaran | Validasi pembayaran | Nominal pembayaran |
| `$bukti` | Upload file | Simpan pembayaran | Bukti transfer |
| `$tanggal` | Generate sistem | Simpan transaksi | Tanggal pembayaran |
| `$status` | Hasil transaksi | Tampilkan pembayaran | Status pembayaran |

---

## Alur Data

| No | Alur Data |
|----|------------|
| 1 | Input data pembayaran |
| 2 | Validasi nominal pembayaran |
| 3 | Upload bukti pembayaran |
| 4 | Simpan transaksi pembayaran |
| 5 | Menampilkan status pembayaran |

---

## Hasil Pengujian

| Test Case | Skenario | Hasil |
|------------|-----------|--------|
| DF12 | Nominal pembayaran valid | Pembayaran berhasil |
| DF13 | Nominal kosong | Validasi gagal |
| DF14 | Upload bukti berhasil | Data pembayaran tersimpan |
| DF15 | Upload bukti gagal | Error upload |
| DF16 | Data siswa ditemukan | Transaksi berhasil |
| DF17 | Data siswa tidak ditemukan | Transaksi gagal |

---

---

# Kesimpulan

Berdasarkan hasil pengujian menggunakan metode Data Flow Testing, seluruh variabel pada modul login, pendaftaran, dan pembayaran telah berhasil diuji mulai dari proses define, use, hingga output data.

Hasil pengujian menunjukkan bahwa aliran data pada sistem PPDB berjalan dengan baik dan tidak ditemukan kesalahan penggunaan variabel, data yang tidak terdefinisi, maupun kesalahan aliran data pada proses autentikasi, pendaftaran, dan pembayaran.
