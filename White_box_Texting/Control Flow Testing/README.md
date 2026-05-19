# Control Flow Testing

## Deskripsi
Control Flow Testing adalah teknik white box testing yang digunakan untuk menguji alur kontrol pada program berdasarkan struktur source code. Pengujian dilakukan dengan menganalisis node, edge, cyclomatic complexity, dan independent path pada setiap modul sistem.

Pengujian ini bertujuan untuk memastikan setiap jalur logika program dapat berjalan dengan baik sesuai rancangan sistem.

---

# Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|----|--------|---------------|-----------------|
| 1 | Login | `auth.php` | Autentikasi pengguna |
| 2 | Pendaftaran | `pendaftaran.php` | Validasi dan penyimpanan data siswa |
| 3 | Pembayaran | `pembayaran.php` | Validasi transaksi pembayaran |

---

# 1. Flowgraph Modul Login (`auth.php`)

## Node

| Node | Proses |
|------|---------|
| 1 | Start |
| 2 | Cek request POST |
| 3 | Input username dan password |
| 4 | Cek akun pegawai |
| 5 | Validasi password pegawai |
| 6 | Redirect dashboard admin |
| 7 | Cek akun wali |
| 8 | Validasi password wali |
| 9 | Redirect dashboard wali |
| 10 | Login gagal |
| 11 | Redirect login |
| 12 | End |

---

## Edge

| Edge | Jalur |
|------|--------|
| E1 | 1 → 2 |
| E2 | 2 → 3 |
| E3 | 2 → 11 |
| E4 | 3 → 4 |
| E5 | 4 → 5 |
| E6 | 4 → 7 |
| E7 | 5 → 6 |
| E8 | 5 → 10 |
| E9 | 7 → 8 |
| E10 | 7 → 10 |
| E11 | 8 → 9 |
| E12 | 8 → 10 |
| E13 | 10 → 11 |
| E14 | 6 → 12 |
| E15 | 9 → 12 |
| E16 | 11 → 12 |

---

## Cyclomatic Complexity

```text
V(G) = E - N + 2
V(G) = 16 - 12 + 2
V(G) = 6
```

---

## Independent Path

| Path | Jalur |
|------|--------|
| P1 | 1 → 2 → 3 → 4 → 5 → 6 → 12 |
| P2 | 1 → 2 → 3 → 4 → 5 → 10 → 11 → 12 |
| P3 | 1 → 2 → 3 → 4 → 7 → 8 → 9 → 12 |
| P4 | 1 → 2 → 3 → 4 → 7 → 8 → 10 → 11 → 12 |
| P5 | 1 → 2 → 3 → 4 → 7 → 10 → 11 → 12 |
| P6 | 1 → 2 → 11 → 12 |

---

# 2. Flowgraph Modul Pendaftaran (`pendaftaran.php`)

## Node

| Node | Proses |
|------|---------|
| 1 | Start |
| 2 | Form pendaftaran dikirim |
| 3 | Validasi field input |
| 4 | Field lengkap |
| 5 | Upload file dokumen |
| 6 | Upload berhasil |
| 7 | Hitung nilai seleksi |
| 8 | Nilai memenuhi syarat |
| 9 | Simpan data ke database |
| 10 | Status diterima |
| 11 | Status tidak diterima |
| 12 | Tampilkan error |
| 13 | Redirect hasil |
| 14 | End |

---

## Edge

| Edge | Jalur |
|------|--------|
| E1 | 1 → 2 |
| E2 | 2 → 3 |
| E3 | 2 → 14 |
| E4 | 3 → 4 |
| E5 | 3 → 12 |
| E6 | 4 → 5 |
| E7 | 5 → 6 |
| E8 | 5 → 12 |
| E9 | 6 → 7 |
| E10 | 7 → 8 |
| E11 | 8 → 9 |
| E12 | 8 → 11 |
| E13 | 9 → 10 |
| E14 | 10 → 13 |
| E15 | 11 → 13 |
| E16 | 12 → 13 |
| E17 | 13 → 14 |

---

## Cyclomatic Complexity

```text
V(G) = E - N + 2
V(G) = 17 - 14 + 2
V(G) = 5
```

---

## Independent Path

| Path | Jalur |
|------|--------|
| P1 | 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 → 10 → 13 → 14 |
| P2 | 1 → 2 → 3 → 12 → 13 → 14 |
| P3 | 1 → 2 → 3 → 4 → 5 → 12 → 13 → 14 |
| P4 | 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 11 → 13 → 14 |
| P5 | 1 → 14 |

---

# 3. Flowgraph Modul Pembayaran (`pembayaran.php`)

## Node

| Node | Proses |
|------|---------|
| 1 | Start |
| 2 | Request pembayaran diterima |
| 3 | Validasi data pembayaran |
| 4 | Data valid |
| 5 | Upload bukti pembayaran |
| 6 | Upload berhasil |
| 7 | Simpan transaksi |
| 8 | Query database berhasil |
| 9 | Redirect pembayaran sukses |
| 10 | Tampilkan error |
| 11 | Redirect gagal |
| 12 | End |

---

## Edge

| Edge | Jalur |
|------|--------|
| E1 | 1 → 2 |
| E2 | 2 → 3 |
| E3 | 2 → 12 |
| E4 | 3 → 4 |
| E5 | 3 → 10 |
| E6 | 4 → 5 |
| E7 | 5 → 6 |
| E8 | 5 → 10 |
| E9 | 6 → 7 |
| E10 | 7 → 8 |
| E11 | 8 → 9 |
| E12 | 8 → 11 |
| E13 | 9 → 12 |
| E14 | 10 → 11 |
| E15 | 11 → 12 |

---

## Cyclomatic Complexity

```text
V(G) = E - N + 2
V(G) = 15 - 12 + 2
V(G) = 5
```

---

## Independent Path

| Path | Jalur |
|------|--------|
| P1 | 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 → 12 |
| P2 | 1 → 2 → 3 → 10 → 11 → 12 |
| P3 | 1 → 2 → 3 → 4 → 5 → 10 → 11 → 12 |
| P4 | 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 11 → 12 |
| P5 | 1 → 12 |

---

# Tabel Pengujian Control Flow

| No | Modul | Path | Skenario Pengujian | Hasil | Status |
|----|--------|------|--------------------|--------|--------|
| 1 | Login | P1 | Login admin berhasil | Redirect dashboard admin | Valid |
| 2 | Login | P2 | Password admin salah | Login gagal | Valid |
| 3 | Login | P3 | Login wali berhasil | Redirect dashboard wali | Valid |
| 4 | Login | P4 | Password wali salah | Login gagal | Valid |
| 5 | Pendaftaran | P1 | Pendaftaran berhasil | Data tersimpan | Valid |
| 6 | Pendaftaran | P2 | Field kosong | Error validasi | Valid |
| 7 | Pendaftaran | P3 | Upload file gagal | Error upload | Valid |
| 8 | Pendaftaran | P4 | Nilai tidak memenuhi syarat | Status tidak diterima | Valid |
| 9 | Pembayaran | P1 | Pembayaran berhasil | Data pembayaran tersimpan | Valid |
| 10 | Pembayaran | P2 | Data pembayaran tidak valid | Error pembayaran | Valid |
| 11 | Pembayaran | P3 | Upload bukti gagal | Error upload | Valid |
| 12 | Pembayaran | P4 | Query database gagal | Transaksi gagal | Valid |



---

# Kesimpulan

Berdasarkan hasil pengujian menggunakan metode Control Flow Testing, seluruh jalur independen (independent path) pada modul login, pendaftaran, dan pembayaran telah berhasil diuji. Setiap proses pada sistem PPDB mampu berjalan sesuai dengan alur logika program yang telah dirancang.

Nilai Cyclomatic Complexity pada setiap modul menunjukkan bahwa tingkat kompleksitas sistem masih dapat dikontrol dan seluruh jalur program dapat diuji dengan baik menggunakan metode basis path testing.
