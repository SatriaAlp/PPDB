# Pengujian 3: Regression Testing
**Skenario:** Penambahan fitur baru (Export to Excel/CSV di tabel pendaftar admin).

**Tujuan:**
Memastikan setelah fitur "Export" ditambah, fitur lama (CRUD pendaftar) gak jadi error atau nge-bug.

### Tahapan Regresi
1. **Cek fitur lama:** Tes ulang fitur tambah, edit, dan hapus pendaftar di admin. Pastikan fungsinya masih aman.
2. **Cek fitur baru:** Klik tombol Export, cek file CSV yang didownload apakah isinya sinkron dengan yang ada di tabel database.
3. **Cek efek samping:** Pastikan UI/tabel gak berantakan gara-gara nambah tombol baru.

### Hasil Uji
| Fitur | Action | Ekspektasi | Hasil Aktual | Status |
|---|---|---|---|---|
| CRUD | Tambah data siswa | Masuk ke database & muncul di tabel | Data masuk tanpa ada field yang null | **Lulus** |
| CRUD | Hapus data siswa | Data beneran hilang dari tabel | Data terhapus bersih dari database | **Lulus** |
| Export | Klik "Export CSV" | File terdownload, format rapi | File `pendaftar.csv` berhasil diunduh | **Lulus** |
| UI | Buka halaman pendaftar | Layout tetap responsif, tombol bisa diklik | Posisi tombol export pas di kanan atas tabel | **Lulus** |
