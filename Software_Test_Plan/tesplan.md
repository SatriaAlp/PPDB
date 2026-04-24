# Software Quality Test Plan

## 1. Tujuan Pengujian
Dokumen ini bertujuan untuk merencanakan proses evaluasi dan pengujian perangkat lunak guna memastikan kualitas produk sesuai dengan standar spesifikasi kebutuhan. Proses ini mencakup tahapan *Software Review* dan eksekusi *Testing*.

## 2. Rencana Software Review
Sesuai dengan prosedur jaminan kualitas, sebelum masuk ke tahap pengujian, dokumen dan rancangan akan dievaluasi melalui tiga tahap berikut:

### A. Walkthrough
* **Deskripsi:** Pembuat kode/dokumen (Author) akan mempresentasikan alur kerja sistem kepada tim pengembang.
* **Target:** Menemukan anomali logika atau skenario yang terlewat secara informal.

### B. Software Inspection
* **Deskripsi:** Evaluasi formal berbasis *checklist* standar kualitas.
* **Peran (Roles):**
    * **Author:** Pengembang fitur.
    * **Inspector / Auditor:** (Nama Teman Kamu/Kontributor GitHub) bertugas memeriksa kesesuaian dengan *checklist*.
    * **Moderator:** Mengatur jalannya inspeksi.
* **Checklist Inspeksi:**
    * [ ] Keamanan data pengguna.
    * [ ] Penanganan *error* (Error handling).
    * [ ] Standar penulisan kode (Clean code).

### C. Technical Review
* **Deskripsi:** *Peer-review* atau peninjauan sejawat oleh tim teknis melalui fitur **Pull Request** di GitHub.
* **Target:** Memastikan arsitektur sistem dan efisiensi algoritma sudah tepat sebelum di-*merge* ke *branch* utama.

## 3. Strategi Pengujian (Testing Approaches)
Pengujian akan dibagi menjadi tiga metode untuk mendapatkan *coverage* (cakupan) yang maksimal:

### A. White Box Testing
* **Fokus:** Logika internal dan struktur kode (pengujian *statement, branch, path*).
* **Eksekusi:** Dilakukan oleh Developer menggunakan *Unit Testing* (misal: memeriksa fungsi validasi email di *backend*).

### B. Black Box Testing
* **Fokus:** Fungsionalitas antarmuka (UI) dan output tanpa melihat kode internal.
* **Eksekusi:** Dilakukan oleh tim QA (Quality Assurance).
* **Contoh Skenario:** Menguji tombol "Login" dengan memasukkan kombinasi *username* dan *password* yang salah, lalu memastikan muncul notifikasi error yang tepat.

### C. Grey Box Testing
* **Fokus:** Kombinasi *White Box* dan *Black Box*. Menguji fungsionalitas dari luar, namun dengan pengetahuan tentang struktur *database* atau arsitektur sistem.
* **Eksekusi:** Pengujian integrasi API atau memanipulasi *input* UI untuk melihat reaksi *database*.

## 4. Kriteria Lolos Pengujian (Acceptance Criteria)
* 100% *checklist* pada *Software Inspection* terpenuhi.
* Tidak ada *bug* dengan level *Critical* atau *High* pada hasil *Black Box Testing*.
* Semua diskusi pada *Technical Review* (Pull Request) telah diselesaikan (*resolved*).
