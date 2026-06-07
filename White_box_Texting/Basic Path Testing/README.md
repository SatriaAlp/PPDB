# Model Basic Path Testing

## 1. Pengertian Basic Path Testing

**Basic Path Testing** adalah salah satu model **White Box Testing** yang berfokus pada identifikasi semua jalur eksekusi yang mungkin terjadi dalam suatu program. Pengujian ini dilakukan dengan menganalisis alur logika program, percabangan kondisi, dan jalur proses dari awal sampai akhir.

Pada Sistem **PPDB TKQ AS-SALAM**, Basic Path Testing digunakan untuk menguji alur program pada fitur **pendaftaran siswa** dan **pembayaran**. Pengujian ini bertujuan untuk memastikan setiap jalur logika program dapat berjalan sesuai dengan kondisi yang diberikan.

---

## 2. Tujuan Pengujian

Tujuan dari **Basic Path Testing** pada Sistem PPDB TKQ AS-SALAM adalah sebagai berikut:

| No | Tujuan Pengujian                                                         |
| -- | ------------------------------------------------------------------------ |
| 1  | Mengidentifikasi jalur eksekusi pada fitur pendaftaran siswa             |
| 2  | Mengidentifikasi jalur eksekusi pada fitur pembayaran                    |
| 3  | Menghitung kompleksitas logika program menggunakan Cyclomatic Complexity |
| 4  | Memastikan setiap percabangan kondisi dapat diuji                        |
| 5  | Mengetahui apakah alur program berjalan sesuai dengan kebutuhan sistem   |

---

## 3. Modul yang Diuji

| No | Modul                 | File Program                  | Keterangan                                                                               |
| -- | --------------------- | ----------------------------- | ---------------------------------------------------------------------------------------- |
| 1  | **Pendaftaran Siswa** | `controllers/pendaftaran.php` | Mengelola validasi login wali, validasi data siswa, upload dokumen, dan seleksi otomatis |
| 2  | **Pembayaran**        | `models/Pembayaran.php`       | Mengelola penyimpanan pembayaran dan perubahan status pembayaran                         |

---

## 4. Source Code yang Diuji

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

    $id_siswa = $siswaModel->register($data_siswa);

    $status = ($_POST['umur_siswa'] >= 4) ? 'Diterima' : 'Tidak Diterima';

    $hasilSeleksiModel->insert([
        'id_siswa' => $id_siswa,
        'id_wali' => $id_wali,
        'status_pendaftaran' => $status
    ]);

    header('Location: ../views/dashboard_wali.php?register_success=1');
    exit();
}
```

---

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

## 5. Flow Graph Modul Pendaftaran

### 5.1 Node Program

| Node | Keterangan                   |
| ---- | ---------------------------- |
| 1    | Start                        |
| 2    | Cek session login wali       |
| 3    | Redirect ke halaman login    |
| 4    | Ambil `id_wali` dari session |
| 5    | Cek request POST             |
| 6    | Validasi field wajib         |
| 7    | Redirect error field kosong  |
| 8    | Validasi file dokumen        |
| 9    | Redirect error file          |
| 10   | Validasi tipe file           |
| 11   | Redirect error tipe file     |
| 12   | Simpan data siswa            |
| 13   | Cek umur siswa               |
| 14   | Status `Diterima`            |
| 15   | Status `Tidak Diterima`      |
| 16   | Simpan hasil seleksi         |
| 17   | Redirect ke dashboard wali   |
| 18   | End                          |

---

### 5.2 Edge Program

| Edge | Alur    |
| ---- | ------- |
| E1   | 1 → 2   |
| E2   | 2 → 3   |
| E3   | 2 → 4   |
| E4   | 3 → 18  |
| E5   | 4 → 5   |
| E6   | 5 → 18  |
| E7   | 5 → 6   |
| E8   | 6 → 7   |
| E9   | 6 → 8   |
| E10  | 7 → 18  |
| E11  | 8 → 9   |
| E12  | 8 → 10  |
| E13  | 9 → 18  |
| E14  | 10 → 11 |
| E15  | 10 → 12 |
| E16  | 11 → 18 |
| E17  | 12 → 13 |
| E18  | 13 → 14 |
| E19  | 13 → 15 |
| E20  | 14 → 16 |
| E21  | 15 → 16 |
| E22  | 16 → 17 |
| E23  | 17 → 18 |

---

## 6. Perhitungan Cyclomatic Complexity

Rumus Cyclomatic Complexity:

```text
V(G) = E - N + 2P
```

Keterangan:

| Simbol | Keterangan                | Nilai |
| ------ | ------------------------- | ----- |
| E      | Jumlah edge               | 23    |
| N      | Jumlah node               | 18    |
| P      | Jumlah komponen terhubung | 1     |

Maka:

```text
V(G) = E - N + 2P
V(G) = 23 - 18 + 2(1)
V(G) = 23 - 18 + 2
V(G) = 7
```

Jadi, nilai **Cyclomatic Complexity** pada modul pendaftaran siswa adalah:

```text
V(G) = 7
```

Artinya, terdapat **7 jalur independen** yang perlu diuji pada modul pendaftaran siswa.

---

## 7. Independent Path Modul Pendaftaran

| Path   | Jalur                            | Keterangan                                                           |
| ------ | -------------------------------- | -------------------------------------------------------------------- |
| Path 1 | 1-2-3-18                         | Wali siswa belum login, sistem redirect ke halaman login             |
| Path 2 | 1-2-4-5-18                       | Wali siswa login, tetapi request bukan POST                          |
| Path 3 | 1-2-4-5-6-7-18                   | Field wajib kosong, sistem menampilkan error                         |
| Path 4 | 1-2-4-5-6-8-9-18                 | File dokumen tidak diupload, sistem menampilkan error                |
| Path 5 | 1-2-4-5-6-8-10-11-18             | Tipe file tidak sesuai, sistem menampilkan error                     |
| Path 6 | 1-2-4-5-6-8-10-12-13-14-16-17-18 | Data valid dan umur siswa 4 tahun atau lebih, status diterima        |
| Path 7 | 1-2-4-5-6-8-10-12-13-15-16-17-18 | Data valid dan umur siswa kurang dari 4 tahun, status tidak diterima |

---

## 8. Skenario Pengujian Modul Pendaftaran

| No | Path   | Skenario Pengujian                           | Input                                      | Output yang Diharapkan                       | Status |
| -- | ------ | -------------------------------------------- | ------------------------------------------ | -------------------------------------------- | ------ |
| 1  | Path 1 | Wali siswa belum login                       | Session kosong                             | Sistem redirect ke halaman login             | Passed |
| 2  | Path 2 | Wali siswa login tetapi belum submit form    | Session login tersedia, request bukan POST | Sistem tidak memproses pendaftaran           | Passed |
| 3  | Path 3 | Field wajib kosong                           | Salah satu field kosong                    | Sistem menampilkan pesan field wajib diisi   | Passed |
| 4  | Path 4 | File dokumen tidak diupload                  | File foto/KK/akta kosong                   | Sistem menampilkan pesan file wajib diupload | Passed |
| 5  | Path 5 | Tipe file tidak sesuai                       | File selain JPG, PNG, atau PDF             | Sistem menolak file                          | Passed |
| 6  | Path 6 | Data valid dan umur memenuhi syarat          | Umur siswa 4 tahun atau lebih              | Status pendaftaran menjadi `Diterima`        | Passed |
| 7  | Path 7 | Data valid tetapi umur belum memenuhi syarat | Umur siswa kurang dari 4 tahun             | Status pendaftaran menjadi `Tidak Diterima`  | Passed |

---
Dokumentasi
---
<img width="535" height="343" alt="image" src="https://github.com/user-attachments/assets/78137807-ccba-4e11-962f-e9cfe5ce3565" /> <img width="535" height="343" alt="image" src="https://github.com/user-attachments/assets/7fab58d0-f92d-4887-a123-d23a42d96d35" />

---
<img width="535" height="343" alt="image" src="https://github.com/user-attachments/assets/048a2aef-d2ec-49b9-8c5f-1a8a223818da" />





## 9. Basic Path Testing Modul Pembayaran

### 9.1 Node Program Pembayaran

| Node | Keterangan                                                  |
| ---- | ----------------------------------------------------------- |
| 1    | Start                                                       |
| 2    | Fungsi `insert($data)` menerima data pembayaran             |
| 3    | Query insert pembayaran dibuat                              |
| 4    | Query dipersiapkan dengan `prepare()`                       |
| 5    | Query dijalankan dengan `execute()`                         |
| 6    | Data pembayaran tersimpan                                   |
| 7    | Fungsi `updateStatus()` menerima `id_pembayaran` dan status |
| 8    | Query update status dibuat                                  |
| 9    | Query update dijalankan                                     |
| 10   | Status pembayaran diperbarui                                |
| 11   | End                                                         |

---

### 9.2 Independent Path Modul Pembayaran

| Path   | Jalur          | Keterangan                                               |
| ------ | -------------- | -------------------------------------------------------- |
| Path 1 | 1-2-3-4-5-6-11 | Data pembayaran disimpan ke database                     |
| Path 2 | 1-7-8-9-10-11  | Status pembayaran diperbarui berdasarkan `id_pembayaran` |

---

### 9.3 Skenario Pengujian Modul Pembayaran

| No | Path   | Skenario Pengujian                  | Input                           | Output yang Diharapkan                | Status |
| -- | ------ | ----------------------------------- | ------------------------------- | ------------------------------------- | ------ |
| 1  | Path 1 | Wali siswa melakukan pembayaran     | Data pembayaran lengkap         | Data pembayaran tersimpan ke database | Passed |
| 2  | Path 2 | Admin memperbarui status pembayaran | `id_pembayaran` dan status baru | Status pembayaran berhasil diperbarui | Passed |

---
Dokumentasi
---
<img width="544" height="339" alt="image" src="https://github.com/user-attachments/assets/40c52621-41d0-4ef2-8899-7d9a81008112" />  <img width="544" height="339" alt="image" src="https://github.com/user-attachments/assets/3429f102-c73f-4c48-8438-8a83f52e163b" />

---
<img width="544" height="339" alt="image" src="https://github.com/user-attachments/assets/1600125c-2756-45c7-9085-f1e961d51cf6" />  <img width="544" height="339" alt="image" src="https://github.com/user-attachments/assets/59397c08-7e5c-4166-875f-324932f1278c" />





## 10. Komunikasi Programmer dan SQ Tester

| No | Komunikasi     | Isi Komunikasi                                                                                     |
| -- | -------------- | -------------------------------------------------------------------------------------------------- |
| 1  | **SQ Tester**  | Apakah alur pendaftaran sudah memiliki jalur untuk kondisi wali belum login?                       |
|    | **Programmer** | Ya, jika session login wali tidak tersedia, sistem langsung mengarahkan pengguna ke halaman login. |
| 2  | **SQ Tester**  | Apakah sistem memiliki jalur untuk field pendaftaran yang kosong?                                  |
|    | **Programmer** | Ya, sistem memeriksa setiap field wajib. Jika ada yang kosong, sistem menampilkan pesan error.     |
| 3  | **SQ Tester**  | Apakah sistem memiliki jalur untuk validasi dokumen?                                               |
|    | **Programmer** | Ya, sistem memeriksa apakah dokumen sudah diupload dan apakah tipe file sesuai.                    |
| 4  | **SQ Tester**  | Bagaimana jalur program ketika umur siswa memenuhi syarat?                                         |
|    | **Programmer** | Sistem akan menentukan status pendaftaran menjadi `Diterima`.                                      |
| 5  | **SQ Tester**  | Bagaimana jalur program ketika umur siswa belum memenuhi syarat?                                   |
|    | **Programmer** | Sistem akan menentukan status pendaftaran menjadi `Tidak Diterima`.                                |
| 6  | **SQ Tester**  | Apakah pembayaran memiliki jalur penyimpanan data?                                                 |
|    | **Programmer** | Ya, data pembayaran disimpan melalui fungsi `insert()` pada model pembayaran.                      |
| 7  | **SQ Tester**  | Apakah pembayaran memiliki jalur perubahan status?                                                 |
|    | **Programmer** | Ya, status pembayaran diperbarui melalui fungsi `updateStatus()`.                                  |

---

## 11. Hasil Pengujian

Berdasarkan hasil **Basic Path Testing**, modul pendaftaran siswa memiliki nilai **Cyclomatic Complexity V(G) = 7**, sehingga terdapat 7 jalur independen yang harus diuji. Jalur tersebut mencakup kondisi wali belum login, request bukan POST, field kosong, file tidak diupload, tipe file tidak sesuai, umur siswa memenuhi syarat, dan umur siswa belum memenuhi syarat.

Pada modul pembayaran, terdapat dua jalur utama yaitu jalur penyimpanan data pembayaran dan jalur perubahan status pembayaran. Kedua jalur tersebut sudah berjalan sesuai dengan kebutuhan sistem.

---

## 12. Kesimpulan

Berdasarkan pengujian menggunakan **Model Basic Path Testing**, dapat disimpulkan bahwa alur logika program pada Sistem PPDB TKQ AS-SALAM sudah memiliki jalur eksekusi yang jelas. Fitur **pendaftaran siswa** memiliki 7 jalur independen yang dapat diuji, sedangkan fitur **pembayaran** memiliki jalur utama untuk menyimpan data pembayaran dan memperbarui status pembayaran.

Hasil pengujian menunjukkan bahwa setiap jalur program dapat menghasilkan output sesuai kondisi yang diberikan. Dengan demikian, modul pendaftaran dan pembayaran dinyatakan layak berdasarkan pengujian Basic Path Testing.

---

## 13. Rekomendasi

| No | Rekomendasi                                                                               |
| -- | ----------------------------------------------------------------------------------------- |
| 1  | Menambahkan validasi ukuran file agar dokumen upload lebih aman                           |
| 2  | Menambahkan validasi nominal pembayaran agar tidak menerima nilai kosong atau negatif     |
| 3  | Menambahkan pesan notifikasi yang lebih jelas pada setiap kondisi error                   |
| 4  | Melakukan pengujian ulang setiap kali ada perubahan pada alur pendaftaran atau pembayaran |
| 5  | Mendokumentasikan hasil pengujian Basic Path Testing di GitHub secara berkala             |

---
