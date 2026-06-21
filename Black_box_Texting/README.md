# Black Box Testing — Sistem PPDB TKQ AS-SALAM

## Deskripsi
Repository ini berisi dokumentasi pengujian **Black Box Testing** pada Sistem PPDB (Penerimaan Peserta Didik Baru) TKQ AS-SALAM.

Black Box Testing dilakukan dari sisi **user interface (UI)** tanpa melihat kode internal. Fokus pengujian meliputi:
- Fungsi sistem
- Output yang dihasilkan
- Alur penggunaan (user experience)

Role yang diuji:
- Wali Siswa
- Admin
- Bendahara

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

| Teknik | Deskripsi |
|--------|----------|
| Equivalence Partitioning | Membagi input ke kelas valid & tidak valid |
| Boundary Value Analysis | Menguji nilai batas minimum & maksimum |
| Decision Table Testing | Menguji kombinasi kondisi dan hasil |
| Use Case Testing | Menguji alur penggunaan berdasarkan role |
| State Transition Testing | Menguji perubahan state sistem (login, logout, dll) |

---

##  Daftar Test Case

| No | File | Modul | Test Case | Status |
|----|------|-------|------------|--------|
| 1 | Login_RegisterAkun | Login & Register | 11 TC | Selesai |
| 2 | Pendaftaran | Form Siswa | 12 TC | Selesai |
| 3 | Pembayaran_Dashboard | Payment & Dashboard | 12 TC | Selesai |

---

##  Rekap Hasil Pengujian

| Modul | Total TC | Pass | Fail | Coverage |
|------|----------|------|------|----------|
| Login & Register | 11 | 11 | 0 | 100% |
| Pendaftaran Siswa | 12 | 12 | 0 | 100% |
| Pembayaran & Dashboard | 12 | 12 | 0 | 100% |
| **TOTAL** | **35** | **35** | **0** | **100%** |

---

##  Use Case Testing
Pengujian dilakukan berdasarkan skenario berikut:
- Wali Siswa: registrasi → login → daftar siswa → pembayaran → logout
- Admin: login → verifikasi data → edit/hapus data → logout
- Bendahara: login → cek pembayaran → validasi transaksi → logout
- Validasi akses berdasarkan role (authorization)

---

##  State Transition Testing
Pengujian perubahan state sistem:
- Guest → Login Success → Dashboard → Logout → Guest
- Guest → Login Failed → Retry Login
- Login gagal berulang → akun terkunci (jika fitur tersedia)
- Akses halaman tanpa login → redirect ke login
- Session handling untuk setiap role

---

##  Halaman yang Diuji

###  Login & Register
- Valid / invalid login
- Register akun baru
- Validasi input kosong
- Username duplikat

###  Form Pendaftaran Siswa
- Input umur valid (>= 4 tahun)
- Validasi file upload (.jpg, .png, .pdf)
- Dropdown & required field validation

###  Pembayaran & Dashboard
- Pembayaran valid / invalid
- Filter tagihan belum lunas
- Dashboard per role
- Logout system

---

##  Tools & Environment
- Browser: Chrome / Firefox
- Server: XAMPP (localhost)
- Method: Manual UI Testing

---

##  Informasi
- Mata Kuliah: Software Quality
- Dosen: Deni Suprihadi, S.T., M.Kom., MCE
- Program Studi: Teknik Informatika
- Universitas: Universitas Kebangsaan Republik Indonesia
- Tanggal Pengujian: 24 April 2026

---

##  Struktur Folder (Rekomendasi GitHub)
