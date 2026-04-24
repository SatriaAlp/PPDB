# White Box Testing — Sistem PPDB TKQ AS-SALAM

## Deskripsi
Folder ini berisi dokumen pengujian **White Box Testing** pada Sistem 
PPDB (Penerimaan Peserta Didik Baru) TKQ AS-SALAM.

White Box Testing dilakukan dengan menguji **struktur internal kode PHP** 
secara langsung, mencakup logika percabangan (branch), alur eksekusi 
(control flow), dan validasi input pada level kode.

---

##  Tim Pengujian
| Nama | NIM | Peran |
|------|-----|-------|
| Diva Rosalinda | 20231310005 | Tester & Dokumentasi |
| Gita Nurcahyani | 20231310006 | Tester & Dokumentasi |
| Gustiar Rifaldi | 20231310031 | Tester & Dokumentasi |
| Satria Alparezi | 20231310017 | Tester & Dokumentasi |

---

##  Teknik Pengujian
| Teknik | Keterangan |
|--------|-----------|
| Basis Path Testing | Mengidentifikasi semua jalur independen dalam kode |
| Branch Coverage | Memastikan setiap IF/ELSE dievaluasi true & false |
| Statement Coverage | Memastikan setiap baris kode tereksekusi |
| Condition Testing | Menguji setiap kondisi logika secara terpisah |
| Data Flow Testing | Menganalisis siklus variabel dari definisi ke penggunaan |

---

##  Daftar Dokumen
| No | Nama File | Modul yang Diuji | Jumlah TC | Status |
|----|-----------|-----------------|-----------|--------|
| 1 | `TestCase_WhiteBox_Login.pdf` | `controllers/auth.php` | 6 TC | ✅ Selesai |
| 2 | `TestCase_WhiteBox_Pendaftaran.pdf` | `controllers/pendaftaran.php` | 9 TC | ✅ Selesai |
| 3 | `TestCase_WhiteBox_RegisterAkun.pdf` | `controllers/register_akun.php` | 7 TC | ✅ Selesai |

---

##  Rekap Hasil Pengujian
| Dokumen | Total TC | Pass | Fail | Coverage |
|---------|----------|------|------|----------|
| White Box Login | 6 | 6 | 0 | 100% |
| White Box Pendaftaran | 9 | 9 | 0 | 100% |
| White Box Register Akun | 7 | 7 | 0 | 100% |
| **TOTAL** | **22** | **22** | **0** | **100%** |

---

##  Modul yang Diuji
### 1. `controllers/auth.php` — Modul Login
- Login sebagai Pegawai (Admin/Bendahara/Staf)
- Login sebagai Wali Siswa
- Penanganan login gagal & input kosong
- Cyclomatic Complexity: V(G) = 4

### 2. `controllers/pendaftaran.php` — Modul Pendaftaran Siswa
- Validasi session login wali
- Validasi required fields (nama, NIK, JK, umur, alamat)
- Validasi file upload (MIME type: JPG, PNG, PDF)
- Sanitasi nama file dengan regex
- Logika seleksi otomatis berdasarkan umur (>= 4 = Diterima)
- Cyclomatic Complexity: V(G) = 5

### 3. `controllers/register_akun.php` — Modul Registrasi Akun
- Validasi semua field wajib
- Pengecekan duplikasi username
- Verifikasi password hashing (bcrypt PASSWORD_DEFAULT)
- Cyclomatic Complexity: V(G) = 4

---

##  Teknologi yang Digunakan
- **Bahasa:** PHP Native
- **Database:** MySQL
- **Server:** XAMPP (Apache)
- **Metode Verifikasi:** var_dump($_SESSION), Header Location, 
  SQL Query langsung via phpMyAdmin

---

##  Informasi Pengujian
| Keterangan | Detail |
|------------|--------|
| Mata Kuliah | Software Quality |
| Dosen | Deni Suprihadi, S.T., M.Kom., MCE |
| Program Studi | Teknik Informatika |
| Universitas | Universitas Kebangsaan Republik Indonesia |
| Tanggal Pengujian | 24 April 2026 |
