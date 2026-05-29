# Pengujian 1: Orthogonal Array Testing (OAT)
**Modul:** Form Pendaftaran Siswa Baru (PPDB TKQ AS-SALAM)

Skenario ini menggunakan OAT untuk menguji form pendaftaran dengan kombinasi input yang berbeda.
Berdasarkan kebutuhan sistem, kita uji 3 variabel utama:
- Usia: < 4 Tahun, 4-6 Tahun, > 6 Tahun
- Dokumen: Lengkap, Kurang, Kosong
- Jalur: Reguler, Pindahan, Khusus

Karena ada 3 faktor dan 3 level, array yang terbentuk adalah L9 (butuh 9 test case).

### Tabel Test Case OAT
| No | Usia | Dokumen | Jalur | Ekspektasi | Hasil |
|---|---|---|---|---|---|
| 1 | < 4 Tahun | Lengkap | Reguler | Ditolak (Usia tidak cukup) | - |
| 2 | < 4 Tahun | Kurang | Pindahan | Ditolak | - |
| 3 | < 4 Tahun | Kosong | Khusus | Form error / minta isi dokumen | - |
| 4 | 4-6 Tahun | Lengkap | Pindahan | Lanjut ke pembayaran | - |
| 5 | 4-6 Tahun | Kurang | Khusus | Pending (tunggu dokumen) | - |
| 6 | 4-6 Tahun | Kosong | Reguler | Form error | - |
| 7 | > 6 Tahun | Lengkap | Khusus | Diterima | - |
| 8 | > 6 Tahun | Kurang | Reguler | Pending (tunggu dokumen) | - |
| 9 | > 6 Tahun | Kosong | Pindahan | Form error | - |
