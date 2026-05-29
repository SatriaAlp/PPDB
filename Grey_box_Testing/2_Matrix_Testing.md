# Pengujian 2: Matrix Testing
**Modul:** Filter Pencarian Data Calon Siswa (Halaman Admin)

Pengujian ini untuk memastikan filter pencarian di tabel admin berjalan lancar saat dipakai kombinasi.
Parameter yang mau diuji:
1. Input Nama: Valid (Alfabet) / Invalid (Angka/Simbol)
2. Status Berkas: Lengkap / Belum
3. Jalur: Reguler / Pindahan

### Matriks Uji Coba
| ID | Input Nama | Status Berkas | Jalur | Ekspektasi Output | Status |
|---|---|---|---|---|---|
| MT-1 | Valid | Lengkap | Reguler | Muncul data siswa reguler yg berkasnya lengkap | - |
| MT-2 | Valid | Belum | Pindahan | Muncul data siswa pindahan yg berkasnya belum lengkap | - |
| MT-3 | Valid | Lengkap | Pindahan | Muncul data siswa pindahan yg berkasnya lengkap | - |
| MT-4 | Invalid | Lengkap | Reguler | Tabel kosong / Muncul "Data tidak ditemukan" | - |
| MT-5 | Invalid | Belum | Pindahan | Tabel kosong / Muncul "Data tidak ditemukan" | - |
