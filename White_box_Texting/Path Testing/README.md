# Path Testing

## Deskripsi
Path Testing adalah teknik white box testing yang digunakan untuk menguji seluruh jalur independen (independent path) pada program. Pengujian dilakukan untuk memastikan setiap kemungkinan jalur eksekusi pada sistem dapat berjalan dengan benar sesuai logika program.

Pada modul `pendaftaran.php`, path testing dilakukan pada proses:
- validasi form,
- upload dokumen,
- seleksi nilai,
- penyimpanan data,
- dan penentuan status penerimaan siswa.

---

# Modul yang Diuji

| No | Modul | File Program | Fokus Pengujian |
|----|--------|---------------|-----------------|
| 1 | Pendaftaran | `pendaftaran.php` | Jalur proses pendaftaran siswa |

---

# Flowgraph Modul Pendaftaran

## Node

| Node | Proses |
|------|---------|
| 1 | Start |
| 2 | Form pendaftaran dikirim |
| 3 | Validasi field input |
| 4 | Field lengkap |
| 5 | Upload dokumen |
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

# Edge

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

# Cyclomatic Complexity

Rumus:

```text
V(G) = E - N + 2
```

Keterangan:
- E = Jumlah Edge
- N = Jumlah Node

Perhitungan:

```text
V(G) = 17 - 14 + 2
V(G) = 5
```

Jadi nilai Cyclomatic Complexity pada modul pendaftaran adalah:

```text
V(G) = 5
```

Artinya terdapat 5 jalur independen yang harus diuji.

---

# Independent Path

## Path 1 – Pendaftaran Berhasil

```text
1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 → 10 → 13 → 14
```

Keterangan:
- Semua data valid
- Upload berhasil
- Nilai memenuhi syarat
- Data tersimpan

---

## Path 2 – Validasi Gagal

```text
1 → 2 → 3 → 12 → 13 → 14
```

Keterangan:
- Ada field kosong
- Sistem menampilkan error validasi

---

## Path 3 – Upload Dokumen Gagal

```text
1 → 2 → 3 → 4 → 5 → 12 → 13 → 14
```

Keterangan:
- Data valid
- Upload dokumen gagal
- Sistem menampilkan error upload

---

## Path 4 – Tidak Lulus Seleksi

```text
1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 11 → 13 → 14
```

Keterangan:
- Data valid
- Upload berhasil
- Nilai tidak memenuhi syarat

---

## Path 5 – Form Tidak Dikirim

```text
1 → 14
```

Keterangan:
- User membuka halaman tanpa submit form

---

# Tabel Path Testing

| Test Case | Path | Skenario | Hasil yang Diharapkan | Status |
|------------|------|-----------|------------------------|--------|
| PT01 | P1 | Semua data valid | Pendaftaran berhasil | Valid |
| PT02 | P2 | Ada field kosong | Error validasi | Valid |
| PT03 | P3 | Upload dokumen gagal | Error upload | Valid |
| PT04 | P4 | Nilai tidak memenuhi syarat | Status tidak diterima | Valid |
| PT05 | P5 | Form tidak dikirim | Sistem tidak memproses data | Valid |

---


---

# Kesimpulan

Berdasarkan hasil pengujian menggunakan metode Path Testing pada modul `pendaftaran.php`, seluruh jalur independen (independent path) telah berhasil diuji.

Hasil pengujian menunjukkan bahwa setiap jalur proses pada sistem pendaftaran mampu berjalan sesuai dengan logika program yang dirancang, baik pada kondisi normal maupun kondisi error.

Nilai Cyclomatic Complexity sebesar 5 menunjukkan bahwa modul pendaftaran memiliki tingkat kompleksitas yang masih dapat dikontrol dan seluruh jalur program dapat diuji dengan baik menggunakan metode path testing.
