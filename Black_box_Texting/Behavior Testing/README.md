# Behavior Testing

## Deskripsi

Behavior Testing adalah model black box testing yang berfokus pada perilaku sistem dari sudut pandang pengguna. Pada Sistem PPDB TKQ AS-SALAM, model ini digunakan untuk menguji alur penggunaan sistem oleh wali siswa, admin, bendahara, dan kepala sekolah.

---

## Modul yang Diuji

| No | Aktor | Modul | Fokus Pengujian |
|---|---|---|---|
| 1 | Wali Siswa | Registrasi akun | Membuat akun wali |
| 2 | Wali Siswa | Login | Masuk ke dashboard wali |
| 3 | Wali Siswa | Pendaftaran siswa | Mengisi data anak dan upload dokumen |
| 4 | Wali Siswa | Pembayaran | Melakukan pembayaran tagihan |
| 5 | Admin | Data pendaftaran | Melihat dan mengelola data pendaftaran |
| 6 | Bendahara | Pembayaran | Melihat dan memverifikasi pembayaran |
| 7 | Kepala Sekolah | Laporan | Melihat laporan pendaftaran dan pembayaran |

---

## Tabel Behavior Testing

| No | Alur Perilaku Pengguna | Expected Output | Actual Output | Test Case | Status |
|---|---|---|---|---|---|
| 1 | Wali membuka halaman registrasi akun | Form daftar akun wali tampil | Sesuai expected output | TC01 | Valid |
| 2 | Wali mengisi data akun dan klik buat akun | Akun berhasil dibuat dan diarahkan ke login | Sesuai expected output | TC02 | Valid |
| 3 | Wali login dengan username dan password benar | Sistem masuk ke dashboard wali | Sesuai expected output | TC03 | Valid |
| 4 | Wali memilih menu pendaftaran | Form pendaftaran anak tampil | Sesuai expected output | TC04 | Valid |
| 5 | Wali mengisi data siswa dan upload dokumen | Data anak tersimpan dan status seleksi tampil | Sesuai expected output | TC05 | Valid |
| 6 | Wali memilih menu pembayaran | Form pembayaran tagihan tampil | Sesuai expected output | TC06 | Valid |
| 7 | Wali melakukan pembayaran | Riwayat pembayaran bertambah | Sesuai expected output | TC07 | Valid |
| 8 | Wali melihat riwayat pendaftaran | Status dan keterangan pendaftaran tampil | Sesuai expected output | TC08 | Valid |
| 9 | Wali logout dari sistem | Session berakhir dan kembali ke halaman login | Sesuai expected output | TC09 | Valid |

---

## Alur Singkat Behavior Testing

1. Wali siswa membuat akun.
2. Wali siswa login ke sistem.
3. Wali siswa mendaftarkan anak.
4. Sistem menentukan status pendaftaran.
5. Wali siswa melakukan pembayaran.
6. Sistem menampilkan riwayat pendaftaran dan pembayaran.
7. Wali siswa logout.

---

## Kesimpulan

Behavior Testing menunjukkan bahwa alur utama sistem sudah sesuai dengan kebutuhan pengguna. Pengujian ini berfokus pada bagaimana sistem merespons tindakan pengguna dari awal registrasi sampai logout.

