# Desk Checking

## 1. Pengertian Desk Checking

**Desk Checking** adalah salah satu model **White Box Testing** yang dilakukan dengan cara memeriksa logika program secara manual. Pemeriksaan dilakukan dengan membaca alur kode, memperhatikan nilai variabel, kondisi program, input yang dimasukkan, proses yang dilakukan, dan output yang dihasilkan.

Pada Sistem **PPDB TKQ AS-SALAM**, Desk Checking digunakan untuk memeriksa apakah alur program pada fitur **pendaftaran siswa** dan **pembayaran** sudah sesuai dengan kebutuhan sistem.

---

## 2. Tujuan Pengujian

Tujuan dari **Desk Checking** pada Sistem PPDB TKQ AS-SALAM adalah sebagai berikut:

| No | Tujuan Pengujian                                                                           |
| -- | ------------------------------------------------------------------------------------------ |
| 1  | Memeriksa logika program pada fitur pendaftaran siswa                                      |
| 2  | Memastikan data input yang dimasukkan pengguna diproses dengan benar                       |
| 3  | Memastikan validasi field wajib berjalan sesuai ketentuan                                  |
| 4  | Memastikan validasi dokumen upload berjalan sesuai format yang ditentukan                  |
| 5  | Memastikan proses pembayaran dan perubahan status pembayaran berjalan sesuai logika sistem |

---

## 3. Modul yang Diuji

| No | Modul                 | File Program                  | Keterangan                                                                              |
| -- | --------------------- | ----------------------------- | --------------------------------------------------------------------------------------- |
| 1  | **Pendaftaran Siswa** | `controllers/pendaftaran.php` | Mengelola proses pendaftaran siswa, validasi data, upload dokumen, dan seleksi otomatis |
| 2  | **Pembayaran**        | `models/Pembayaran.php`       | Mengelola proses penyimpanan data pembayaran dan perubahan status pembayaran            |

---

## 4. Source Code yang Diperiksa

### 4.1 Source Code Pendaftaran Siswa

```php
if (!isset($_SESSION['login_wali'])) {
    header('Location: ../views/login.php');
    exit();
}

$id_wali = $_SESSION['id_wali'];

if ($_SERVER['REQUEST_METHOD'] === 'POST') {

    $requiredFields = [
        'nama_siswa',
        'nik_siswa',
        'jenis_kelamin_siswa',
        'umur_siswa',
        'alamat_siswa'
    ];

    foreach ($requiredFields as $field) {
        if (empty(trim($_POST[$field] ?? ''))) {
            header("Location: ../views/register.php?error=Field $field wajib diisi");
            exit();
        }
    }

    $status = ($_POST['umur_siswa'] >= 4) ? 'Diterima' : 'Tidak Diterima';
}
```

### 4.2 Source Code Pembayaran

```php
public function insert($data)
{
    $sql = "INSERT INTO pembayaran 
    (id_biaya, id_wali, tanggal_pembayaran, nominal_dibayar, status_pembayaran, metode_pembayaran, keterangan_pembayaran)
    VALUES 
    (:id_biaya, :id_wali, :tanggal_pembayaran, :nominal_dibayar, :status_pembayaran, :metode_pembayaran, :keterangan_pembayaran)";

    $stmt = $this->pdo->prepare($sql);

    $stmt->execute([
        ':id_biaya' => $data['id_biaya'],
        ':id_wali' => $data['id_wali'],
        ':tanggal_pembayaran' => $data['tanggal_pembayaran'],
        ':nominal_dibayar' => $data['nominal_dibayar'],
        ':status_pembayaran' => $data['status_pembayaran'],
        ':metode_pembayaran' => $data['metode_pembayaran'],
        ':keterangan_pembayaran' => $data['keterangan_pembayaran']
    ]);
}
```

---

## 5. Tabel Desk Checking Modul Pendaftaran

| No | Input                                        | Proses Logika Program                                  | Output yang Diharapkan                           | Hasil  |
| -- | -------------------------------------------- | ------------------------------------------------------ | ------------------------------------------------ | ------ |
| 1  | Wali siswa belum login                       | Sistem memeriksa `$_SESSION['login_wali']`             | Pengguna diarahkan ke halaman login              | Passed |
| 2  | Wali siswa sudah login                       | Sistem mengambil `id_wali` dari session                | Wali dapat mengakses form pendaftaran            | Passed |
| 3  | Form pendaftaran dikirim dengan field kosong | Sistem memeriksa setiap field pada `$requiredFields`   | Sistem menampilkan pesan bahwa field wajib diisi | Passed |
| 4  | Form pendaftaran lengkap                     | Sistem melewati proses validasi field                  | Sistem melanjutkan ke proses validasi dokumen    | Passed |
| 5  | Dokumen tidak diupload                       | Sistem memeriksa file pada `$_FILES`                   | Sistem menampilkan pesan file wajib diupload     | Passed |
| 6  | File dokumen bukan JPG, PNG, atau PDF        | Sistem memeriksa tipe file berdasarkan `$allowedTypes` | Sistem menolak file yang tidak sesuai format     | Passed |
| 7  | Umur siswa 4 tahun atau lebih                | Sistem memeriksa kondisi `umur_siswa >= 4`             | Status pendaftaran menjadi `Diterima`            | Passed |
| 8  | Umur siswa kurang dari 4 tahun               | Sistem memeriksa kondisi `umur_siswa < 4`              | Status pendaftaran menjadi `Tidak Diterima`      | Passed |

---

## 6. Tabel Desk Checking Modul Pembayaran

| No | Input                            | Proses Logika Program                                    | Output yang Diharapkan                     | Hasil  |
| -- | -------------------------------- | -------------------------------------------------------- | ------------------------------------------ | ------ |
| 1  | Data pembayaran lengkap          | Sistem menerima data pembayaran melalui variabel `$data` | Data pembayaran dapat diproses             | Passed |
| 2  | `id_biaya` tersedia              | Sistem menyimpan relasi pembayaran berdasarkan biaya     | Data biaya tersimpan pada tabel pembayaran | Passed |
| 3  | `id_wali` tersedia               | Sistem menyimpan identitas wali siswa yang membayar      | Pembayaran terhubung dengan akun wali      | Passed |
| 4  | `tanggal_pembayaran` tersedia    | Sistem menyimpan tanggal transaksi pembayaran            | Tanggal pembayaran tercatat                | Passed |
| 5  | `nominal_dibayar` tersedia       | Sistem menyimpan jumlah nominal pembayaran               | Nominal pembayaran tercatat                | Passed |
| 6  | `status_pembayaran` tersedia     | Sistem menyimpan status pembayaran                       | Status pembayaran tersimpan                | Passed |
| 7  | Admin mengubah status pembayaran | Sistem menjalankan fungsi `updateStatus()`               | Status pembayaran berhasil diperbarui      | Passed |

---

## 7. Analisis Logika Program

### 7.1 Analisis Pendaftaran Siswa

Pada modul **pendaftaran siswa**, sistem terlebih dahulu memeriksa apakah wali siswa sudah login. Jika session login tidak tersedia, sistem akan mengarahkan pengguna ke halaman login. Hal ini menunjukkan bahwa sistem sudah memiliki logika keamanan dasar agar hanya wali siswa yang memiliki akun dapat melakukan pendaftaran.

Setelah wali siswa login, sistem memproses data pendaftaran melalui request POST. Sistem kemudian memeriksa field wajib seperti **nama siswa**, **NIK siswa**, **jenis kelamin siswa**, **umur siswa**, dan **alamat siswa**. Jika terdapat field kosong, sistem akan menghentikan proses dan menampilkan pesan error.

Selain itu, sistem juga memeriksa dokumen upload seperti **foto siswa**, **KK**, dan **akta kelahiran**. Jika file tidak diupload atau format file tidak sesuai, sistem akan menolak proses pendaftaran. Setelah data valid, sistem menentukan status pendaftaran berdasarkan umur siswa.

### 7.2 Analisis Pembayaran

Pada modul **pembayaran**, sistem menerima data pembayaran melalui variabel `$data`. Data tersebut berisi **id_biaya**, **id_wali**, **tanggal pembayaran**, **nominal dibayar**, **status pembayaran**, **metode pembayaran**, dan **keterangan pembayaran**.

Data pembayaran kemudian dimasukkan ke dalam query SQL dan diproses menggunakan prepared statement. Hal ini menunjukkan bahwa alur pembayaran sudah memiliki proses penyimpanan data yang jelas. Selain itu, sistem juga memiliki fungsi untuk memperbarui status pembayaran melalui fungsi `updateStatus()`.

---

## 8. Komunikasi Programmer dan SQ Tester

| No | Komunikasi     | Isi Komunikasi                                                                                          |
| -- | -------------- | ------------------------------------------------------------------------------------------------------- |
| 1  | **SQ Tester**  | Apakah sistem sudah membatasi akses pendaftaran hanya untuk wali siswa yang login?                      |
|    | **Programmer** | Ya, sistem memeriksa session `login_wali`. Jika tidak ada, pengguna diarahkan ke halaman login.         |
| 2  | **SQ Tester**  | Apakah field wajib pada form pendaftaran sudah divalidasi?                                              |
|    | **Programmer** | Sudah, sistem memeriksa field nama siswa, NIK, jenis kelamin, umur, dan alamat siswa.                   |
| 3  | **SQ Tester**  | Bagaimana jika wali siswa tidak mengupload dokumen?                                                     |
|    | **Programmer** | Sistem akan menolak proses pendaftaran dan menampilkan pesan bahwa file wajib diupload.                 |
| 4  | **SQ Tester**  | Bagaimana sistem menentukan status pendaftaran siswa?                                                   |
|    | **Programmer** | Sistem menentukan status berdasarkan umur siswa. Jika umur 4 tahun atau lebih, status menjadi diterima. |
| 5  | **SQ Tester**  | Apakah data pembayaran sudah tersimpan melalui model pembayaran?                                        |
|    | **Programmer** | Ya, data pembayaran disimpan melalui fungsi `insert()` pada model `Pembayaran.php`.                     |
| 6  | **SQ Tester**  | Apakah status pembayaran dapat diubah oleh sistem?                                                      |
|    | **Programmer** | Ya, status pembayaran dapat diperbarui melalui fungsi `updateStatus()`.                                 |

---

## 9. Hasil Pengujian

Berdasarkan hasil **Desk Checking**, logika program pada fitur **pendaftaran siswa** dan **pembayaran** sudah berjalan sesuai dengan kebutuhan sistem. Sistem dapat memeriksa session login, memvalidasi data pendaftaran, memvalidasi dokumen upload, menentukan status pendaftaran, menyimpan data pembayaran, dan memperbarui status pembayaran.

---

## 10. Kesimpulan

Berdasarkan pengujian menggunakan model **Desk Checking**, dapat disimpulkan bahwa logika program pada Sistem PPDB TKQ AS-SALAM sudah berjalan dengan baik. Setiap input yang dimasukkan oleh pengguna dapat diproses melalui alur program yang sesuai.

Pada fitur **pendaftaran siswa**, sistem mampu melakukan validasi data dan dokumen sebelum menyimpan data ke database. Pada fitur **pembayaran**, sistem mampu menyimpan data pembayaran dan memperbarui status pembayaran. Dengan demikian, modul pendaftaran dan pembayaran dinyatakan layak berdasarkan pengujian Desk Checking.

---

## 11. Rekomendasi

| No | Rekomendasi                                                                                 |
| -- | ------------------------------------------------------------------------------------------- |
| 1  | Menambahkan validasi ukuran file agar dokumen yang terlalu besar tidak dapat diupload       |
| 2  | Menambahkan validasi nominal pembayaran agar tidak menerima nilai kosong, nol, atau negatif |
| 3  | Menambahkan notifikasi yang lebih jelas ketika pendaftaran dan pembayaran berhasil          |
| 4  | Melakukan pemeriksaan logika program secara berkala ketika ada perubahan kode               |
| 5  | Mendokumentasikan hasil pengujian di GitHub agar riwayat pengujian tersimpan dengan rapi    |

---
