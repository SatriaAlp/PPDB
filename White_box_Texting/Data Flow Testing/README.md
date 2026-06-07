# Data Flow Testing

## 1. Pengertian Data Flow Testing

**Data Flow Testing** adalah salah satu model **White Box Testing** yang berfokus pada aliran data di dalam program. Pengujian ini dilakukan dengan melihat bagaimana data atau variabel didefinisikan, digunakan, diproses, dan disimpan oleh sistem.

Pada Sistem **PPDB TKQ AS-SALAM**, Data Flow Testing digunakan untuk menguji aliran data pada fitur **pendaftaran siswa** dan **pembayaran**. Pengujian ini bertujuan untuk memastikan bahwa data yang dimasukkan oleh pengguna dapat diproses dengan benar oleh sistem, mulai dari input form, validasi data, upload dokumen, penyimpanan ke database, hingga menghasilkan status pendaftaran dan pembayaran.

---

## 2. Tujuan Pengujian

Tujuan dari **Data Flow Testing** pada Sistem PPDB TKQ AS-SALAM adalah sebagai berikut:

| No | Tujuan Pengujian                                                                                              |
| -- | ------------------------------------------------------------------------------------------------------------- |
| 1  | Memastikan data pendaftaran siswa dapat mengalir dari form input menuju database dengan benar                 |
| 2  | Memastikan variabel yang digunakan pada program sudah didefinisikan sebelum diproses                          |
| 3  | Memastikan data dokumen seperti foto siswa, KK, dan akta kelahiran dapat divalidasi dan disimpan dengan benar |
| 4  | Memastikan data pembayaran dapat disimpan dan status pembayaran dapat diperbarui                              |
| 5  | Mengetahui apakah terdapat kesalahan aliran data yang dapat menyebabkan error pada sistem                     |

---

## 3. Modul yang Diuji

| No | Modul                 | File Program                  | Keterangan                                                                        |
| -- | --------------------- | ----------------------------- | --------------------------------------------------------------------------------- |
| 1  | **Pendaftaran Siswa** | `controllers/pendaftaran.php` | Mengelola proses input data siswa, validasi, upload dokumen, dan seleksi otomatis |
| 2  | **Pembayaran**        | `models/Pembayaran.php`       | Mengelola proses penyimpanan data pembayaran dan perubahan status pembayaran      |

---

## 4. Source Code yang Diuji

### 4.1 Source Code Modul Pendaftaran

```php
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

    $requiredFiles = ['akta_kelahiran', 'kk', 'foto_siswa'];
    $allowedTypes = ['image/jpeg', 'image/png', 'application/pdf'];

    foreach ($requiredFiles as $fileKey) {
        if (!isset($_FILES[$fileKey]) || $_FILES[$fileKey]['error'] !== UPLOAD_ERR_OK) {
            header("Location: ../views/register.php?error=File $fileKey wajib diupload.");
            exit();
        }

        if (!in_array($_FILES[$fileKey]['type'], $allowedTypes)) {
            header("Location: ../views/register.php?error=File $fileKey harus bertipe JPG, PNG, atau PDF.");
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
    $keterangan = ($status === 'Diterima') ? 'Usia memenuhi syarat' : 'Umur tidak memenuhi syarat';
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

## 5. Tabel Data Flow Testing Modul Pendaftaran

| Komponen                      | Definisi                                          | Penggunaan                                                       | Deskripsi                                                                               |
| ----------------------------- | ------------------------------------------------- | ---------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **Input id_wali**             | Data wali siswa yang diperoleh dari session login | Digunakan sebagai identitas wali pada data pendaftaran siswa     | Sistem mengambil `id_wali` dari session untuk menghubungkan data siswa dengan akun wali |
| **Input nama_siswa**          | Data nama siswa dari form pendaftaran             | Digunakan dalam proses validasi dan penyimpanan data siswa       | Sistem memastikan nama siswa tidak kosong sebelum data disimpan                         |
| **Input nik_siswa**           | Data NIK siswa dari form pendaftaran              | Digunakan sebagai identitas siswa                                | Sistem memvalidasi NIK agar data siswa memiliki identitas yang jelas                    |
| **Input jenis_kelamin_siswa** | Data jenis kelamin siswa dari form                | Digunakan sebagai bagian dari informasi siswa                    | Sistem memastikan jenis kelamin sudah dipilih oleh pengguna                             |
| **Input umur_siswa**          | Data umur siswa dari form pendaftaran             | Digunakan untuk menentukan status seleksi otomatis               | Jika umur siswa 4 tahun atau lebih, status menjadi diterima                             |
| **Input alamat_siswa**        | Data alamat siswa dari form                       | Digunakan sebagai informasi tempat tinggal siswa                 | Sistem memastikan alamat tidak kosong sebelum disimpan                                  |
| **Input foto_siswa**          | File foto siswa yang diupload pengguna            | Digunakan sebagai dokumen pendukung pendaftaran                  | Sistem memvalidasi file agar hanya menerima format JPG, PNG, atau PDF                   |
| **Input kk**                  | File kartu keluarga yang diupload pengguna        | Digunakan sebagai dokumen persyaratan PPDB                       | Sistem mengecek apakah file KK sudah diupload dan formatnya sesuai                      |
| **Input akta_kelahiran**      | File akta kelahiran siswa                         | Digunakan sebagai dokumen pendukung pendaftaran                  | Sistem memvalidasi file sebelum dipindahkan ke folder upload                            |
| **Fungsi register siswa**     | Proses penyimpanan data siswa ke database         | Digunakan untuk menyimpan seluruh data siswa yang sudah valid    | Sistem menyimpan data siswa setelah semua input dan dokumen memenuhi ketentuan          |
| **Fungsi seleksi otomatis**   | Proses penentuan status berdasarkan umur siswa    | Digunakan untuk menghasilkan status diterima atau tidak diterima | Sistem menentukan status pendaftaran berdasarkan syarat umur siswa                      |
| **Output status_pendaftaran** | Hasil akhir dari proses seleksi siswa             | Ditampilkan sebagai status hasil seleksi                         | Output berupa status `Diterima` atau `Tidak Diterima`                                   |

---

## 6. Tabel Data Flow Testing Modul Pembayaran

| Komponen                        | Definisi                                     | Penggunaan                                                                           | Deskripsi                                                                                  |
| ------------------------------- | -------------------------------------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| **Input id_biaya**              | Data biaya atau tagihan PPDB                 | Digunakan sebagai relasi pembayaran terhadap jenis biaya                             | Sistem menggunakan `id_biaya` untuk mengetahui pembayaran dilakukan untuk tagihan tertentu |
| **Input id_wali**               | Data wali siswa yang melakukan pembayaran    | Digunakan sebagai identitas pembayar                                                 | Sistem menghubungkan pembayaran dengan akun wali siswa                                     |
| **Input tanggal_pembayaran**    | Data tanggal saat pembayaran dilakukan       | Digunakan untuk mencatat waktu transaksi pembayaran                                  | Sistem menyimpan tanggal pembayaran ke tabel pembayaran                                    |
| **Input nominal_dibayar**       | Jumlah uang yang dibayarkan oleh wali siswa  | Digunakan sebagai nilai transaksi pembayaran                                         | Sistem menyimpan nominal pembayaran sebagai bukti jumlah pembayaran                        |
| **Input status_pembayaran**     | Status pembayaran pada sistem                | Digunakan untuk mengetahui apakah pembayaran sudah lunas, pending, atau diverifikasi | Sistem dapat memperbarui status pembayaran melalui fungsi update status                    |
| **Input metode_pembayaran**     | Metode pembayaran yang digunakan wali siswa  | Digunakan sebagai informasi cara pembayaran                                          | Sistem mencatat metode pembayaran yang dipilih                                             |
| **Input keterangan_pembayaran** | Catatan tambahan terkait pembayaran          | Digunakan untuk memberikan informasi tambahan pada transaksi                         | Sistem menyimpan keterangan pembayaran jika diperlukan                                     |
| **Fungsi insert pembayaran**    | Proses menyimpan data pembayaran ke database | Digunakan saat wali siswa melakukan pembayaran                                       | Sistem menyimpan data pembayaran ke tabel pembayaran                                       |
| **Fungsi updateStatus**         | Proses mengubah status pembayaran            | Digunakan oleh admin untuk memverifikasi pembayaran                                  | Sistem mengubah status pembayaran berdasarkan `id_pembayaran`                              |
| **Output status pembayaran**    | Hasil akhir dari proses pembayaran           | Ditampilkan sebagai status pembayaran wali siswa                                     | Output menunjukkan apakah pembayaran sudah diproses atau belum                             |

---

## 7. Alur Data Sistem

### 7.1 Alur Data Pendaftaran Siswa

1. Pengguna login sebagai wali siswa.
2. Sistem mengambil data **id_wali** dari session.
3. Wali siswa mengisi form pendaftaran.
4. Sistem memeriksa field wajib seperti nama, NIK, jenis kelamin, umur, dan alamat.
5. Sistem memeriksa file dokumen seperti foto siswa, KK, dan akta kelahiran.
6. Sistem memvalidasi tipe file.
7. Sistem menyusun data siswa ke dalam variabel `$data_siswa`.
8. Data siswa disimpan ke database melalui fungsi register.
9. Sistem menentukan status seleksi berdasarkan umur siswa.
10. Sistem menyimpan hasil seleksi.
11. Sistem menampilkan hasil pendaftaran kepada pengguna.

### 7.2 Alur Data Pembayaran

1. Wali siswa melakukan pembayaran.
2. Sistem menerima data pembayaran.
3. Data pembayaran terdiri dari **id_biaya**, **id_wali**, **tanggal_pembayaran**, **nominal_dibayar**, **status_pembayaran**, **metode_pembayaran**, dan **keterangan_pembayaran**.
4. Sistem menyusun data pembayaran dalam variabel `$data`.
5. Data pembayaran dikirim ke fungsi `insert()`.
6. Sistem menyimpan data pembayaran ke database.
7. Admin dapat melakukan verifikasi pembayaran.
8. Sistem memperbarui status pembayaran melalui fungsi `updateStatus()`.
9. Status pembayaran ditampilkan kepada pengguna.

---

## 8. Skenario Pengujian

| No | Skenario Pengujian                                    | Data yang Diuji                  | Hasil yang Diharapkan                                     | Status |
| -- | ----------------------------------------------------- | -------------------------------- | --------------------------------------------------------- | ------ |
| 1  | Wali siswa belum login                                | Session `login_wali`             | Sistem mengarahkan pengguna ke halaman login              | Passed |
| 2  | Wali siswa mengisi form pendaftaran lengkap           | Data siswa                       | Sistem menerima dan menyimpan data siswa                  | Passed |
| 3  | Wali siswa mengosongkan salah satu field wajib        | Field pendaftaran                | Sistem menolak dan menampilkan pesan error                | Passed |
| 4  | Wali siswa tidak mengupload dokumen wajib             | File dokumen                     | Sistem menolak proses pendaftaran                         | Passed |
| 5  | Wali siswa mengupload file dengan format tidak sesuai | File foto, KK, atau akta         | Sistem menolak file selain JPG, PNG, atau PDF             | Passed |
| 6  | Umur siswa 4 tahun atau lebih                         | Umur siswa                       | Sistem menghasilkan status `Diterima`                     | Passed |
| 7  | Umur siswa kurang dari 4 tahun                        | Umur siswa                       | Sistem menghasilkan status `Tidak Diterima`               | Passed |
| 8  | Data pembayaran lengkap dimasukkan                    | Data pembayaran                  | Sistem menyimpan data pembayaran ke database              | Passed |
| 9  | Admin memperbarui status pembayaran                   | Status pembayaran                | Sistem mengubah status pembayaran sesuai verifikasi admin | Passed |
| 10 | Pembayaran ditampilkan kepada wali siswa              | Data pembayaran berdasarkan wali | Sistem menampilkan riwayat pembayaran wali siswa          | Passed |

---

## 9. Komunikasi Programmer dan SQ Tester

| No | Komunikasi     | Isi Komunikasi                                                                                       |
| -- | -------------- | ---------------------------------------------------------------------------------------------------- |
| 1  | **SQ Tester**  | Apakah data wali siswa sudah digunakan pada proses pendaftaran?                                      |
|    | **Programmer** | Ya, data `id_wali` diambil dari session login dan digunakan untuk menyimpan data siswa.              |
| 2  | **SQ Tester**  | Apakah sistem sudah memvalidasi field wajib pada form pendaftaran?                                   |
|    | **Programmer** | Sudah, sistem memeriksa nama siswa, NIK, jenis kelamin, umur, dan alamat siswa.                      |
| 3  | **SQ Tester**  | Bagaimana sistem memproses file dokumen siswa?                                                       |
|    | **Programmer** | Sistem mengecek apakah file sudah diupload dan memvalidasi tipe file JPG, PNG, atau PDF.             |
| 4  | **SQ Tester**  | Bagaimana sistem menentukan status pendaftaran siswa?                                                |
|    | **Programmer** | Sistem menentukan status berdasarkan umur siswa. Jika umur 4 tahun atau lebih, maka status diterima. |
| 5  | **SQ Tester**  | Bagaimana data pembayaran disimpan?                                                                  |
|    | **Programmer** | Data pembayaran disimpan melalui fungsi `insert()` pada model `Pembayaran.php`.                      |
| 6  | **SQ Tester**  | Apakah status pembayaran dapat diperbarui?                                                           |
|    | **Programmer** | Ya, status pembayaran dapat diperbarui melalui fungsi `updateStatus()`.                              |

---

## 10. Hasil Pengujian

Berdasarkan hasil **Data Flow Testing**, aliran data pada Sistem PPDB TKQ AS-SALAM sudah berjalan dengan baik. Data yang dimasukkan oleh wali siswa dapat diproses melalui form pendaftaran, divalidasi oleh sistem, kemudian disimpan ke database.

Pada modul pendaftaran, data seperti **id_wali**, **nama_siswa**, **nik_siswa**, **jenis_kelamin_siswa**, **umur_siswa**, **alamat_siswa**, **foto_siswa**, **kk**, dan **akta_kelahiran** sudah digunakan sesuai kebutuhan sistem.

Pada modul pembayaran, data seperti **id_biaya**, **id_wali**, **tanggal_pembayaran**, **nominal_dibayar**, **status_pembayaran**, **metode_pembayaran**, dan **keterangan_pembayaran** sudah mengalir ke proses penyimpanan pembayaran.

---

## 11. Kesimpulan

Berdasarkan pengujian menggunakan model **Data Flow Testing**, dapat disimpulkan bahwa aliran data pada Sistem PPDB TKQ AS-SALAM khususnya pada fitur **pendaftaran siswa** dan **pembayaran** sudah berjalan sesuai dengan kebutuhan sistem.

Sistem mampu menerima input dari pengguna, melakukan validasi data, memproses dokumen, menyimpan data siswa, menentukan status pendaftaran, menyimpan pembayaran, dan memperbarui status pembayaran. Dengan demikian, modul pendaftaran dan pembayaran dinyatakan layak berdasarkan pengujian aliran data.

---

## 12. Rekomendasi

Adapun rekomendasi perbaikan dari hasil pengujian adalah sebagai berikut:

| No | Rekomendasi                                                                                                                  |
| -- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1  | Menambahkan validasi ukuran file upload agar dokumen yang terlalu besar tidak dapat diproses                                 |
| 2  | Menambahkan kode unik pada nama file agar file dengan nama siswa yang sama tidak saling menimpa                              |
| 3  | Menambahkan validasi nominal pembayaran agar sistem tidak menerima pembayaran bernilai kosong atau negatif                   |
| 4  | Menyediakan tampilan notifikasi yang lebih jelas ketika proses pendaftaran atau pembayaran berhasil                          |
| 5  | Melakukan pengujian sistem secara berkala melalui GitHub agar perubahan kode dan dokumentasi pengujian tersimpan dengan rapi |

---

[⬅ Kembali ke README](../README.md)
