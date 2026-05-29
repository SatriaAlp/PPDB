# Pengujian 1: Orthogonal Array Testing (OAT)
**Modul:** Form Pendaftaran Siswa Baru (PPDB TKQ AS-SALAM)

Skenario ini menggunakan OAT untuk menguji form pendaftaran dengan kombinasi input yang berbeda.
Berdasarkan kebutuhan sistem, kita uji 3 variabel utama:
- Usia: < 4 Tahun, 4-6 Tahun, > 6 Tahun
- Dokumen: Lengkap, Kurang, Kosong
- Jalur: Reguler, Pindahan, Khusus

Karena ada 3 faktor dan 3 level, array yang terbentuk adalah L9 (butuh 9 test case).

### Tabel Test Case OAT
| No | Usia | Dokumen | Jalur | Ekspektasi | Hasil Aktual / Status |
|---|---|---|---|---|---|
| 1 | < 4 Tahun | Lengkap | Reguler | Ditolak (Usia tidak cukup) | **Lulus** (Muncul alert validasi umur) |
| 2 | < 4 Tahun | Kurang | Pindahan | Ditolak | **Lulus** (Sistem memblokir submit) |
| 3 | < 4 Tahun | Kosong | Khusus | Form error / minta isi dokumen | **Lulus** (Validasi frontend jalan) |
| 4 | 4-6 Tahun | Lengkap | Pindahan | Lanjut ke pembayaran | **Lulus** (Redirect ke halaman invoice) |
| 5 | 4-6 Tahun | Kurang | Khusus | Pending (tunggu dokumen) | **Lulus** (Data masuk DB dengan status 'Pending') |
| 6 | 4-6 Tahun | Kosong | Reguler | Form error | **Lulus** (Muncul notifikasi berkas wajib diisi) |
| 7 | > 6 Tahun | Lengkap | Khusus | Diterima | **Lulus** (Data masuk DB dengan status 'Diterima') |
| 8 | > 6 Tahun | Kurang | Reguler | Pending (tunggu dokumen) | **Lulus** (Status pending & muncul log di admin) |
| 9 | > 6 Tahun | Kosong | Pindahan | Form error | **Lulus** (Ditolak oleh sistem) |

### Kesimpulan Pengujian OAT
Semua kombinasi input dari L9 array berhasil dihandle oleh sistem validasi pendaftaran PPDB. Tidak ditemukan adanya data bocor atau lolos dari filter umur/berkas.
