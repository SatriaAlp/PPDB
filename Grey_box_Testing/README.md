# 🔲 Grey Box Testing — Sistem PPDB TKQ AS-SALAM

## 📌 Deskripsi
Folder ini berisi dokumen pengujian **Grey Box Testing** pada Sistem 
PPDB (Penerimaan Peserta Didik Baru) TKQ AS-SALAM.

Grey Box Testing merupakan **kombinasi White Box + Black Box Testing**.
Tester memiliki sebagian pengetahuan internal sistem (struktur database 
& alur modul), namun tetap menguji dari sisi antarmuka pengguna (UI),
lalu memverifikasi hasilnya langsung ke database MySQL.

---

## 👥 Tim Pengujian
| Nama | NIM | Peran |
|------|-----|-------|
| Diva Rosalinda | 20231310005 | Tester & Dokumentasi |
| Gita Nurcahyani | 20231310006 | Tester & Dokumentasi |
| Gustiar Rifaldi | 20231310031 | Tester & Dokumentasi |
| Satria Alparezi | 20231310017 | Tester & Dokumentasi |

---

## 🎯 Teknik Pengujian
| Teknik | Keterangan |
|--------|-----------|
| Integration Testing | Menguji integrasi antar modul & tabel database |
| Matrix Testing | Memetakan relasi antar modul dalam bentuk matriks |
| Regression Testing | Memastikan fitur lama tidak rusak setelah commit baru |
| Database Verification | Verifikasi hasil UI langsung ke tabel MySQL |

---

## 📂 Daftar Dokumen
| No | Nama File | Jenis Pengujian | Jumlah TC | Status |
|----|-----------|----------------|-----------|--------|
| 1 | `TestCase_GreyBox_Integrasi.pdf` | Integration Testing | 12 TC | ✅ Selesai |
| 2 | `TestCase_GreyBox_Regression.pdf` | Regression Testing | 12 TC | ✅ Selesai |

---

## 📊 Rekap Hasil Pengujian
| Dokumen | Total TC | Pass | Fail | Coverage |
|---------|----------|------|------|----------|
| Grey Box Integrasi | 12 | 12 | 0 | 100% |
| Grey Box Regression | 12 | 12 | 0 | 100% |
| **TOTAL** | **24** | **24** | **0** | **100%** |

---

## 🔍 Cakupan Pengujian

### 1. Integration Testing (`TestCase_GreyBox_Integrasi.pdf`)
Menguji integrasi antara UI dan database secara bersamaan:

| Skenario | Tabel yang Diverifikasi |
|----------|------------------------|
| Registrasi akun wali | `wali_siswa` |
| Pendaftaran siswa | `siswa` + `hasil_seleksi` |
| Seleksi otomatis umur | `hasil_seleksi` |
| Sanitasi nama file | `siswa` + `/uploads/` |
| Pembayaran | `pembayaran` + `tagihan` |
| Login & session | `wali_siswa` / `pegawai` |
| Logout | Session PHP |

### 2. Regression Testing (`TestCase_GreyBox_Regression.pdf`)
Memastikan 70 commit tidak merusak fitur yang sudah berjalan:

| Fitur yang Diuji Ulang | Status |
|------------------------|--------|
| Login Wali & Admin | ✅ Stabil |
| Pendaftaran & Upload File | ✅ Stabil |
| Seleksi Otomatis Umur | ✅ Stabil |
| Password Hashing (bcrypt) | ✅ Stabil |
| UNIQUE Constraint Username | ✅ Stabil |
| Foreign Key Antar Tabel | ✅ Stabil |
| JOIN Query Pembayaran | ✅ Stabil |
| Dashboard Multi-Profil Anak | ✅ Stabil |
| Nominal Tagihan dari Rincian Biaya | ✅ Stabil |
| Logout & Hapus Session | ✅ Stabil |

---

## 🗄️ Struktur Database yang Diuji
