# 1. Orthogonal Array Testing (OAT)
**Fitur yang diuji:** Formulir Pendaftaran Siswa Baru (PPDB TKQ AS-SALAM)

## A. Identifikasi Variabel (Faktor dan Level)
Berdasarkan kebutuhan pendaftaran, terdapat 3 faktor utama yang mempengaruhi keberhasilan pendaftaran siswa, masing-masing dengan 3 level pengujian:
1. **Usia Pendaftar:** < 4 Tahun, 4-6 Tahun, > 6 Tahun
2. **Kelengkapan Dokumen:** Lengkap, Sebagian, Kosong
3. **Jalur Pendaftaran:** Reguler, Pindahan, Jalur Khusus

**Jumlah Kasus Uji:** Berdasarkan pemetaan Orthogonal Array L9(3^3), kita hanya memerlukan 9 kasus uji untuk mencakup seluruh kombinasi kritis.

## B. Tabel Skenario Uji (OAT)

| Kasus Uji # | Usia Pendaftar | Kelengkapan Dokumen | Jalur Pendaftaran | Ekspektasi Hasil (Sistem PPDB) | Status |
| :---: | :--- | :--- | :--- | :--- | :---: |
| 1 | < 4 Tahun | Lengkap | Reguler | Ditolak (Usia belum mencukupi) | [ ] |
| 2 | < 4 Tahun | Sebagian | Pindahan | Ditolak (Usia & Dokumen tidak valid) | [ ] |
| 3 | < 4 Tahun | Kosong | Jalur Khusus | Ditolak (Validasi form gagal) | [ ] |
| 4 | 4-6 Tahun | Lengkap | Pindahan | Diterima (Lanjut ke proses seleksi/pembayaran) | [ ] |
| 5 | 4-6 Tahun | Sebagian | Jalur Khusus | Pending (Notifikasi lengkapi dokumen) | [ ] |
| 6 | 4-6 Tahun | Kosong | Reguler | Ditolak (Validasi form gagal) | [ ] |
| 7 | > 6 Tahun | Lengkap | Jalur Khusus | Diterima (Review manual oleh admin) | [ ] |
| 8 | > 6 Tahun | Sebagian | Reguler | Pending (Notifikasi lengkapi dokumen) | [ ] |
| 9 | > 6 Tahun | Kosong | Pindahan | Ditolak (Validasi form gagal) | [ ] |

## C. Kesimpulan Pengujian OAT
*(Bagian ini diisi setelah kamu menjalankan 9 pengujian di atas pada aplikasi web PPDB)*
