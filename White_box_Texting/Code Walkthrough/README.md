# Model Code Walkthrough

## 1. Pengertian Model Code Walkthrough

**Model Code Walkthrough** adalah salah satu model **White Box Testing** yang dilakukan dengan cara meninjau kode program secara formal atau informal bersama programmer dan SQ tester. Pengujian ini bertujuan untuk memahami logika kode, menemukan potensi kesalahan, dan meningkatkan kualitas program.

Pada Sistem **PPDB TKQ AS-SALAM**, Model Code Walkthrough dilakukan pada fitur **pendaftaran siswa** dan **pembayaran**. Pengujian dilakukan dengan membaca bagian kode program yang berhubungan dengan validasi data, proses upload dokumen, penyimpanan data siswa, penyimpanan pembayaran, dan perubahan status pembayaran.

---

## 2. Tujuan Pengujian

| No | Tujuan Pengujian                                         |
| -- | -------------------------------------------------------- |
| 1  | Memahami alur kode pada fitur pendaftaran siswa          |
| 2  | Memahami alur kode pada fitur pembayaran                 |
| 3  | Menemukan potensi kesalahan pada proses validasi data    |
| 4  | Menemukan potensi kesalahan pada proses penyimpanan data |
| 5  | Memberikan rekomendasi perbaikan terhadap kode program   |

---

## 3. Modul yang Diuji

| No | Modul                 | File Program                  | Keterangan                                                                              |
| -- | --------------------- | ----------------------------- | --------------------------------------------------------------------------------------- |
| 1  | **Pendaftaran Siswa** | `controllers/pendaftaran.php` | Mengelola proses pendaftaran siswa, validasi data, upload dokumen, dan seleksi otomatis |
| 2  | **Pembayaran**        | `models/Pembayaran.php`       | Mengelola penyimpanan data pembayaran dan perubahan status pembayaran                   |

---

## 4. Source Code yang Direview

### 4.1 Source Code Modul Pendaftaran

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

    $data_siswa = [
        'id_wali' => $id_wali,
        'nama_siswa' => $_POST['nama_siswa'],
        'nik_siswa' => $_POST['nik_siswa'],
        'jenis_kelamin_siswa' => $_POST['jenis_kelamin_siswa'],
        'umur_siswa' => (int) $_POST['umur_siswa'],
        'alamat_siswa' => $_POST['alamat_siswa']
    ];

    $id_siswa = $siswaModel->register($data_siswa);

    $status = ($_POST['umur_siswa'] >= 4) ? 'Diterima' : 'Tidak Diterima';
}
```

### 4.2 Source Code Modul Pembayaran

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

public function updateStatus($id_pembayaran, $status)
{
    $sql = "UPDATE pembayaran 
            SET status_pembayaran = :status_pembayaran 
            WHERE id_pembayaran = :id_pembayaran";

    $stmt = $this->pdo->prepare($sql);

    $stmt->execute([
        ':status_pembayaran' => $status,
        ':id_pembayaran' => $id_pembayaran
    ]);
}
```

---

## 5. Tabel Model Code Walkthrough Modul Pendaftaran

| No | Bagian Kode yang Direview               | Fungsi Kode                                        | Hasil Review                                                                  | Status |
| -- | --------------------------------------- | -------------------------------------------------- | ----------------------------------------------------------------------------- | ------ |
| 1  | `$_SESSION['login_wali']`               | Memeriksa apakah wali siswa sudah login            | Kode sudah sesuai karena pengguna yang belum login diarahkan ke halaman login | Passed |
| 2  | `$id_wali = $_SESSION['id_wali'];`      | Mengambil ID wali dari session                     | Kode sudah sesuai karena data siswa harus terhubung dengan akun wali          | Passed |
| 3  | `$_SERVER['REQUEST_METHOD'] === 'POST'` | Memastikan proses hanya berjalan saat form dikirim | Kode sudah sesuai karena data diproses ketika request POST                    | Passed |
| 4  | `$requiredFields`                       | Menentukan field wajib pada form pendaftaran       | Kode sudah sesuai karena field penting sudah dicantumkan                      | Passed |
| 5  | `foreach ($requiredFields as $field)`   | Mengecek field wajib satu per satu                 | Kode sudah sesuai karena semua field wajib diperiksa                          | Passed |
| 6  | `empty(trim($_POST[$field] ?? ''))`     | Mengecek apakah field kosong                       | Kode sudah sesuai karena input kosong akan ditolak                            | Passed |
| 7  | `$data_siswa`                           | Menyusun data siswa sebelum disimpan               | Kode sudah sesuai karena data dikumpulkan dalam satu array                    | Passed |
| 8  | `$siswaModel->register($data_siswa)`    | Menyimpan data siswa ke database                   | Kode sudah sesuai karena penyimpanan dilakukan melalui model                  | Passed |
| 9  | `$status = ($_POST['umur_siswa'] >= 4)` | Menentukan status pendaftaran berdasarkan umur     | Kode sudah sesuai dengan aturan seleksi otomatis                              | Passed |

---

## 6. Tabel Model Code Walkthrough Modul Pembayaran

| No | Bagian Kode yang Direview               | Fungsi Kode                          | Hasil Review                                                           | Status                     |
| -- | --------------------------------------- | ------------------------------------ | ---------------------------------------------------------------------- | -------------------------- |
| 1  | `public function insert($data)`         | Menerima data pembayaran             | Kode sudah sesuai karena pembayaran diproses melalui fungsi khusus     | Passed                     |
| 2  | `$sql = "INSERT INTO pembayaran..."`    | Membuat query penyimpanan pembayaran | Kode sudah sesuai karena data pembayaran disiapkan untuk disimpan      | Passed                     |
| 3  | `$this->pdo->prepare($sql)`             | Menyiapkan query SQL                 | Kode sudah baik karena menggunakan prepared statement                  | Passed                     |
| 4  | `$stmt->execute([...])`                 | Menjalankan query pembayaran         | Kode sudah sesuai karena setiap data memiliki parameter masing-masing  | Passed                     |
| 5  | `$data['id_biaya']`                     | Mengambil data biaya                 | Kode sudah sesuai untuk menghubungkan pembayaran dengan biaya tertentu | Passed                     |
| 6  | `$data['id_wali']`                      | Mengambil data wali                  | Kode sudah sesuai untuk menghubungkan pembayaran dengan wali siswa     | Passed                     |
| 7  | `$data['nominal_dibayar']`              | Mengambil nominal pembayaran         | Kode sudah sesuai, tetapi sebaiknya ditambah validasi nominal          | Passed with Recommendation |
| 8  | `updateStatus($id_pembayaran, $status)` | Mengubah status pembayaran           | Kode sudah sesuai karena status pembayaran dapat diperbarui            | Passed                     |
| 9  | `WHERE id_pembayaran = :id_pembayaran`  | Menentukan pembayaran yang diubah    | Kode sudah sesuai karena update dilakukan berdasarkan ID pembayaran    | Passed                     |

---

## 7. Hasil Review Kode

| No | Komponen             | Hasil Review                                          | Rekomendasi                                                           |
| -- | -------------------- | ----------------------------------------------------- | --------------------------------------------------------------------- |
| 1  | Session login        | Sistem sudah memeriksa login wali sebelum pendaftaran | Pertahankan pemeriksaan session                                       |
| 2  | Validasi field wajib | Sistem sudah memeriksa field kosong                   | Tambahkan validasi format NIK                                         |
| 3  | Status pendaftaran   | Sistem menentukan status berdasarkan umur siswa       | Pertahankan aturan umur minimal 4 tahun                               |
| 4  | Insert pembayaran    | Sistem sudah memiliki fungsi penyimpanan pembayaran   | Pertahankan penggunaan prepared statement                             |
| 5  | Nominal pembayaran   | Nominal pembayaran disimpan ke database               | Tambahkan validasi agar nominal tidak boleh kosong, nol, atau negatif |

---

## 8. Komunikasi Programmer dan SQ Tester

| No | Komunikasi     | Isi Komunikasi                                                                                                             |
| -- | -------------- | -------------------------------------------------------------------------------------------------------------------------- |
| 1  | **SQ Tester**  | Apakah proses pendaftaran hanya dapat dilakukan oleh wali siswa yang sudah login?                                          |
|    | **Programmer** | Ya, sistem memeriksa session `login_wali`. Jika session tidak tersedia, pengguna diarahkan ke halaman login.               |
| 2  | **SQ Tester**  | Apakah semua field wajib pada pendaftaran sudah diperiksa?                                                                 |
|    | **Programmer** | Sudah, field nama siswa, NIK, jenis kelamin, umur, dan alamat siswa diperiksa menggunakan array `$requiredFields`.         |
| 3  | **SQ Tester**  | Apakah data siswa langsung disimpan ke database?                                                                           |
|    | **Programmer** | Data siswa disusun terlebih dahulu dalam variabel `$data_siswa`, kemudian dikirim ke fungsi `register()` pada model siswa. |
| 4  | **SQ Tester**  | Bagaimana sistem menentukan status pendaftaran siswa?                                                                      |
|    | **Programmer** | Sistem menentukan status berdasarkan umur siswa. Jika umur siswa 4 tahun atau lebih, maka status menjadi `Diterima`.       |
| 5  | **SQ Tester**  | Apakah proses pembayaran sudah menggunakan fungsi khusus?                                                                  |
|    | **Programmer** | Ya, proses pembayaran menggunakan fungsi `insert()` pada model `Pembayaran.php`.                                           |
| 6  | **SQ Tester**  | Apakah status pembayaran dapat diperbarui?                                                                                 |
|    | **Programmer** | Ya, status pembayaran dapat diperbarui melalui fungsi `updateStatus()` berdasarkan `id_pembayaran`.                        |

---

## 9. Temuan Pengujian

| No | Temuan                                                        | Tingkat Risiko | Rekomendasi                                                      |
| -- | ------------------------------------------------------------- | -------------- | ---------------------------------------------------------------- |
| 1  | Sistem sudah memeriksa session login wali sebelum pendaftaran | Rendah         | Pertahankan validasi session                                     |
| 2  | Field wajib pada pendaftaran sudah divalidasi                 | Rendah         | Tambahkan validasi format NIK                                    |
| 3  | Status pendaftaran hanya berdasarkan umur siswa               | Sedang         | Jika diperlukan, tambahkan kriteria seleksi lain                 |
| 4  | Data pembayaran sudah disimpan menggunakan prepared statement | Rendah         | Pertahankan penggunaan prepared statement                        |
| 5  | Nominal pembayaran belum terlihat memiliki validasi khusus    | Sedang         | Tambahkan validasi nominal tidak boleh kosong, nol, atau negatif |

---

## 10. Kesimpulan

Berdasarkan hasil **Model Code Walkthrough**, kode program pada fitur **pendaftaran siswa** dan **pembayaran** sudah memiliki alur yang jelas. Pada fitur pendaftaran, sistem sudah memeriksa session login wali, memvalidasi field wajib, menyusun data siswa, menyimpan data ke database, dan menentukan status pendaftaran berdasarkan umur siswa.

Pada fitur pembayaran, sistem sudah memiliki fungsi untuk menyimpan data pembayaran dan memperbarui status pembayaran. Dengan demikian, kode pada modul pendaftaran dan pembayaran dinyatakan layak berdasarkan pengujian Model Code Walkthrough.

---

## 11. Rekomendasi

| No | Rekomendasi                                                                                 |
| -- | ------------------------------------------------------------------------------------------- |
| 1  | Menambahkan validasi format NIK agar data siswa lebih akurat                                |
| 2  | Menambahkan validasi ukuran file upload                                                     |
| 3  | Menambahkan validasi nominal pembayaran agar tidak menerima nilai kosong, nol, atau negatif |
| 4  | Menambahkan notifikasi ketika pembayaran berhasil diverifikasi                              |
| 5  | Melakukan review kode secara berkala melalui GitHub setiap ada perubahan fitur              |
