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
| MT-1 | Valid | Lengkap | Reguler | Muncul data siswa reguler yg berkasnya lengkap | **Lulus** |
| MT-2 | Valid | Belum | Pindahan | Muncul data siswa pindahan yg berkasnya belum lengkap | **Lulus** |
| MT-3 | Valid | Lengkap | Pindahan | Muncul data siswa pindahan yg berkasnya lengkap | **Lulus** |
| MT-4 | Invalid | Lengkap | Reguler | Tabel kosong / Muncul "Data tidak ditemukan" | **Gagal (Bug #01)** |
| MT-5 | Invalid | Belum | Pindahan | Tabel kosong / Muncul "Data tidak ditemukan" | **Lulus** |

### Analisa Hasil Test & Temuan Bug
* **Bug #01 (Skenario MT-4):** Ketika input pencarian nama dimasukkan karakter simbol (contoh: `Anas%';--`), query SQL di backend sempat mengalami *error internal server (500)* karena masalah *escaping character*. 
* **Tindakan:** Masalah ini sudah difiksasi di sisi backend dengan menerapkan *query binding* / *prepared statements* agar aman dari SQL Injection. Setelah ditest ulang, status berubah menjadi **Lulus**.
