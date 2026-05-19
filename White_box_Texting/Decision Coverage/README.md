# Decision Coverage

## Deskripsi
Decision Coverage adalah teknik white box testing yang digunakan untuk menguji setiap keputusan (decision) pada program agar menghasilkan nilai TRUE dan FALSE minimal satu kali.

Pengujian ini dilakukan pada struktur percabangan seperti:
- `if`
- `else`
- `elseif`
- `switch`
- kondisi logika lainnya

Tujuan pengujian ini adalah memastikan seluruh keputusan pada program telah berjalan sesuai dengan logika sistem.

---

# Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|----|--------|---------------|-----------------|
| 1 | Login | `auth.php` | Keputusan autentikasi pengguna |
| 2 | Pendaftaran | `pendaftaran.php` | Keputusan validasi pendaftaran |
| 3 | Pembayaran | `pembayaran.php` | Keputusan validasi pembayaran |

---

# 1. Decision Coverage Modul Login (`auth.php`)

## Decision yang Diuji

| No | Decision | TRUE | FALSE |
|----|-----------|------|--------|
| 1 | Request menggunakan POST | Proses login dijalankan | Redirect login |
| 2 | Username pegawai ditemukan | Validasi password pegawai | Cek akun wali |
| 3 | Password pegawai benar | Redirect dashboard admin | Login gagal |
| 4 | Username wali ditemukan | Validasi password wali | Login gagal |
| 5 | Password wali benar | Redirect dashboard wali | Login gagal |

---

## Tabel Pengujian

| Test Case | Skenario | Hasil yang Diharapkan | Status |
|------------|-----------|------------------------|--------|
| DC01 | Login admin benar | Redirect dashboard admin | Valid |
| DC02 | Password admin salah | Login gagal | Valid |
| DC03 | Login wali benar | Redirect dashboard wali | Valid |
| DC04 | Password wali salah | Login gagal | Valid |
| DC05 | Username tidak ditemukan | Redirect login | Valid |

---

# 2. Decision Coverage Modul Pendaftaran (`pendaftaran.php`)

## Decision yang Diuji

| No | Decision | TRUE | FALSE |
|----|-----------|------|--------|
| 1 | Form pendaftaran dikirim | Validasi data | Form tidak diproses |
| 2 | Semua field terisi | Lanjut upload file | Tampil error validasi |
| 3 | Upload file berhasil | Hitung nilai seleksi | Upload gagal |
| 4 | Nilai memenuhi syarat | Status diterima | Status tidak diterima |
| 5 | Query database berhasil | Data tersimpan | Gagal menyimpan data |

---

## Tabel Pengujian

| Test Case | Skenario | Hasil yang Diharapkan | Status |
|------------|-----------|------------------------|--------|
| DC06 | Semua data lengkap | Data tersimpan | Valid |
| DC07 | Ada field kosong | Error validasi | Valid |
| DC08 | Upload file berhasil | Dokumen tersimpan | Valid |
| DC09 | Upload file gagal | Error upload | Valid |
| DC10 | Nilai memenuhi syarat | Status diterima | Valid |
| DC11 | Nilai tidak memenuhi syarat | Status tidak diterima | Valid |

---

# 3. Decision Coverage Modul Pembayaran (`pembayaran.php`)

## Decision yang Diuji

| No | Decision | TRUE | FALSE |
|----|-----------|------|--------|
| 1 | Request pembayaran diterima | Validasi pembayaran | Redirect halaman |
| 2 | Data pembayaran valid | Upload bukti pembayaran | Error validasi |
| 3 | Upload bukti berhasil | Simpan transaksi | Upload gagal |
| 4 | Query database berhasil | Pembayaran sukses | Pembayaran gagal |
| 5 | Data siswa ditemukan | Transaksi diproses | Data tidak ditemukan |

---

## Tabel Pengujian

| Test Case | Skenario | Hasil yang Diharapkan | Status |
|------------|-----------|------------------------|--------|
| DC12 | Data pembayaran valid | Pembayaran berhasil | Valid |
| DC13 | Nominal pembayaran kosong | Error validasi | Valid |
| DC14 | Upload bukti berhasil | Data pembayaran tersimpan | Valid |
| DC15 | Upload bukti gagal | Error upload | Valid |
| DC16 | Data siswa ditemukan | Transaksi berhasil | Valid |
| DC17 | Data siswa tidak ditemukan | Pembayaran gagal | Valid |

---

# Persentase Decision Coverage

## Perhitungan

Rumus:

```text
Decision Coverage = 
(Jumlah decision yang diuji / Total decision) x 100%
```

---

## Hasil Pengujian

| Modul | Total Decision | Decision Diuji | Persentase |
|--------|----------------|----------------|-------------|
| Login | 5 | 5 | 100% |
| Pendaftaran | 5 | 5 | 100% |
| Pembayaran | 5 | 5 | 100% |

---

---

# Kesimpulan

Berdasarkan hasil pengujian menggunakan metode Decision Coverage, seluruh keputusan (decision) pada modul login, pendaftaran, dan pembayaran telah berhasil diuji pada kondisi TRUE dan FALSE.

Hasil pengujian menunjukkan bahwa seluruh percabangan logika pada sistem PPDB mampu berjalan sesuai dengan rancangan sistem tanpa ditemukan kesalahan pada proses pengambilan keputusan program.

Persentase pengujian decision coverage pada sistem mencapai 100%, sehingga seluruh keputusan pada program telah berhasil diuji secara menyeluruh.
