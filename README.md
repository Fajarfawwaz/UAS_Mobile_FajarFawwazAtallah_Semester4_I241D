# Absensi Fajar v2.0: Enterprise Cloud-Based Attendance System 🚀

## IDENTITAS MAHASISWA :

## Nama : Fajar Fawwaz Atallah 

## Kelas : I241D

## NIM : 312410357

## MATKUL : PEMROGRAMAN MOBILE 

# SAYA MEMBUAT TUGAS INI UNTUK MENGERJAKAN TUGAS UAS PEMROGRAMAN MOBILE SEMESTER 4

## DI BAWAH INI ADALAH GANT DI CLICK UP PERUBAHAN DARI APLIKASI SAYA YANG SEBELUMNYA , SAYA MERUBAH SEDIKIT TAMPILAN DAN MENAMBAHKAN BEBERAPA FITUR :

<img width="1823" height="757" alt="image" src="https://github.com/user-attachments/assets/62fc26cd-1bc6-44b0-aa2a-08e283020e3c" />

## UNTUK LINK CLICK UP ( SCRUM ) YANG LEBIH LENGKAPNYA SEBAGAI BERIKUT : https://sharing.clickup.com/90181768471/g/h/2kzm158q-638/0a2b95cb74cd5f0

## Absensi Fajar adalah solusi manajemen kehadiran berbasis Android yang menggabungkan presisi Biometric Face Recognition dengan validasi lokasi Geofencing GPS. Sistem ini dirancang untuk memastikan integritas data kehadiran dengan teknologi sinkronisasi Cloud yang aman dan efisien.

# 🏗️ Arsitektur Sistem (System Architecture)

## Aplikasi ini menggunakan model Hybrid Synchronization:

### 1. Local Storage (SQLite): Digunakan untuk manajemen sesi, caching data riwayat, dan operasional offline terbatas.

### 2. Cloud Storage (MySQL via AwardSpace): Berperan sebagai Single Source of Truth (Sumber data utama) untuk monitoring Administrator secara real-time.

### 3. Communication: Menggunakan Retrofit 2 dengan arsitektur REST API untuk pertukaran data format JSON.

# DI Bawah Ini adalah UI login dan  HALAMAN MAHASISWA : 

<img width="1018" height="788" alt="Screenshot 2026-04-30 132424" src="https://github.com/user-attachments/assets/13724084-bac6-4cdf-882d-f33f4a3e873a" />


# 📱 Penjelasan Detail Halaman (Page-by-Page Explanation)

# 1. Modul Mahasiswa (User Interface)

# - Halaman Login & Recovery:

# LOGIN, REGISTER, FORGOT PASSWORD : 

<img width="220" alt="image" src="https://github.com/user-attachments/assets/6eaaffbb-2989-4040-8421-de88a9383aee" />
<img width="220" alt="image" src="https://github.com/user-attachments/assets/bb072d3d-7845-4599-980d-79e0f0179527" />
<img width="220" alt="image" src="https://github.com/user-attachments/assets/98358d4b-11e7-49e4-a809-d14f1a4c11e7" />

## ◦ Mendukung autentikasi ganda (Lokal & Cloud).

## ◦ Fitur Identity Recovery: Jika user pindah perangkat atau re-install aplikasi, sistem secara otomatis menarik kembali nama, role, dan data wajah (embedding) dari Cloud ke SQLite lokal.

# - Halaman Dashboard Utama:

<img width="250" alt="image" src="https://github.com/user-attachments/assets/6c85796b-ff35-4a29-926f-2bb58e604c41" />

## ◦ Statistik Dinamis: Menampilkan total hadir, telat, dan izin yang disinkronkan langsung dari server AwardSpace.

## ◦ Real-time Greeting: Ucapan selamat berdasarkan waktu sistem (Pagi/Siang/Malam).

## ◦ Profile Preview: Menampilkan foto profil yang diambil saat pendaftaran wajah.

# - Halaman Registrasi Wajah (Biometric Enrollment):

<img width="250" alt="image" src="https://github.com/user-attachments/assets/bb3142f2-06b3-493c-b93b-8c44187cc484" />

## ◦ Menggunakan Google ML Kit untuk mendeteksi wajah dan FaceNet Model untuk mengonversi citra wajah menjadi 192 titik koordinat angka (embeddings).

## ◦ Data ini di-upload ke Cloud untuk keamanan identitas permanen.

# - Halaman Absensi (Scanning & Geofencing):

<img width="250" alt="image" src="https://github.com/user-attachments/assets/13509c91-17c0-4c33-9749-47c17a21994e" />

## ◦ Validasi Lokasi: Memeriksa jarak user dengan koordinat Kampus UPB. Jika jarak > 150 meter, akses scan wajah ditutup (mencegah manipulasi lokasi).

## ◦ Biometric Verification: Mencocokkan wajah saat ini dengan data pendaftaran menggunakan algoritma Cosine Similarity.

# - Halaman Riwayat (Attendance History):

<img width="250" alt="image" src="https://github.com/user-attachments/assets/ae48e7d5-5b64-432d-971b-d035204abb9a" />

## ◦ Menampilkan list kronologis kehadiran user yang diambil dari basis data lokal (SQLite).

# - Halaman Pengajuan Izin (Digital Leave Request) :

<img width="250" alt="image" src="https://github.com/user-attachments/assets/a28fc16b-5d01-4e1d-861d-48a76a1eae20" />

## Halaman ini berfungsi sebagai sistem administrasi jika mahasiswa berhalangan hadir (Sakit, Izin, atau Cuti).

## • Formulir Digital: Input jenis izin (Sakit/Izin/Cuti), alasan keterangan tertulis, dan pemilihan tanggal.

## • Lampiran Bukti (Camera Integration): Mahasiswa diwajibkan melampirkan foto bukti (misalnya: Surat Keterangan Dokter) yang diambil langsung melalui kamera sebagai validasi.

## • Data Persistence:
   
   ### ◦ Lokal: Data disimpan ke tabel pengajuan_izin di SQLite.
   
   ### ◦ Cloud: Secara otomatis mengirimkan notifikasi status ke database AwardSpace sehingga Admin dapat melihat alasan ketidakhadiran di tabel rekapitulasi secara real-time.

## • Business Logic: Pengajuan izin otomatis mengisi kolom status pada riwayat absensi sehingga persentase kehadiran tetap terhitung secara administratif.

# - Halaman Profil & Manajemen Identitas (Identity Module) :

<img width="250" alt="image" src="https://github.com/user-attachments/assets/b7b4131a-2c81-4dfd-86eb-b16c9d3dc351" />

## Halaman ini adalah pusat pengaturan data pribadi dan verifikasi keamanan perangkat user.

## • Visual Identity: Menampilkan foto profil mahasiswa yang diambil saat pendaftaran biometrik pertama kali (Face Enrollment).

## • Informasi Personal: Menampilkan detail data yang tersimpan di server:
   
   ### ◦ Nama Lengkap & Email Akun.
   
   ### ◦ Nomor Telepon & Alamat.
   
   ### ◦ Tanggal Lahir.
   
   ### ◦ Role User: Menandakan status akun (Mahasiswa/Admin).

## • Security Info (Device Integrity): 
   
   ### ◦ Face Registry Status: Menampilkan indikator apakah data wajah sudah tersinkronisasi dengan server Cloud.
   
   ### ◦ Device ID Binding: Menampilkan ID unik perangkat untuk memastikan akun tidak disalahgunakan di banyak perangkat berbeda.
   
## • Edit Profile: Fitur untuk memperbarui data nomor telepon dan alamat secara dinamis yang langsung memperbarui database SQLite lokal dan MySQL Cloud.

# 🖥️ Menu Utama Modul Administrator (Control Panel) :

<img width="250" alt="image" src="https://github.com/user-attachments/assets/3361891e-b95e-4419-ab70-81a3280369f2" />

## Panel Administrator menyediakan 5 menu fungsional utama untuk mengelola seluruh ekosistem absensi di tempat yang dia gunakan :

# - 📊 Menu Monitoring (Rekapitulasi Kehadiran) :  

<img width="250" alt="image" src="https://github.com/user-attachments/assets/41798e55-1830-4895-903c-d87b849f7860" />

# Menu ini berfungsi sebagai pusat pantauan performa kehadiran seluruh mahasiswa.

## • Rekapitulasi Otomatis: Menampilkan daftar nama mahasiswa beserta total akumulasi status Hadir, Terlambat, dan Izin.

## • Detail Individu: Admin dapat mengklik salah satu nama untuk melihat rincian riwayat absensi spesifik milik mahasiswa tersebut.

# -  👥 Menu Mahasiswa (Manajemen Akun) :

<img width="250" alt="image" src="https://github.com/user-attachments/assets/f5c802d6-bb23-466a-8003-f279de753f4d" />

## Menu yang digunakan untuk mendata seluruh akun mahasiswa yang telah terdaftar di sistem. 

## • Interaktif Tabel: Menggunakan desain Zebra-Style untuk memudahkan pembacaan data dalam jumlah banyak.

## • Real-time Search: Dilengkapi fitur pencarian instan berdasarkan Nama atau Email untuk efisiensi manajemen data.

## • Badge Role: Identifikasi visual untuk membedakan antara akun Mahasiswa dan Administrator.

# - 📄 Menu Rekap Excel (Reporting) :

<img width="250" alt="image" src="https://github.com/user-attachments/assets/25ce7219-a919-488a-81c7-9c3a1b418ea7" />

## Menu ini didedikasikan untuk keperluan administratif dan pelaporan formal. 

## • Auto-Generator: Sistem secara otomatis mengonversi data dari database Cloud menjadi file format Excel (.xls).

## • Global Report: Laporan yang dihasilkan mencakup seluruh record absensi yang masuk di server, siap untuk dicetak atau diarsipkan oleh bagian akademik.

# - ⚙️ Menu Sistem (Konfigurasi & Maintenance) :

<img width="250" alt="image" src="https://github.com/user-attachments/assets/a4e4892b-b216-4b08-8442-bdd2ca939921" />

## Dikenal sebagai fitur "Obeng", menu ini memberikan fleksibilitas bagi Admin untuk mengatur kebijakan kampus secara dinamis.

## • Dynamic Geofencing: Admin dapat mengubah batas radius absen (misal: 150 meter) langsung dari aplikasi tanpa harus merubah kode program.

## • Time Policy: Pengaturan jam masuk kampus yang fleksibel sesuai kebijakan universitas.

## • Security Tools: Tersedia fitur Reset Data (pembersihan riwayat per-semester) dan SQL Cloud Backup untuk keamanan basis data.

# - 📩 Menu Validasi Izin & Sakit (Document Verification) :

<img width="250" alt="image" src="https://github.com/user-attachments/assets/a019b116-c228-43da-bd1c-4dadd1db93cc" />
<img width="250" alt="image" src="https://github.com/user-attachments/assets/8e14f165-536d-4014-ab29-47bca5dd6643" />

## Menu terbaru yang berfungsi untuk memvalidasi alasan ketidakhadiran mahasiswa.

## • Digital Evidence: Admin dapat melihat bukti foto (seperti surat dokter) yang diunggah mahasiswa melalui jalur Cloud.

## • Cross-Check: Menampilkan jenis izin, tanggal, dan alasan tertulis mahasiswa secara mendetail.

## • Swipe to Refresh: Mendukung fitur tarik layar untuk menyinkronkan data pengajuan izin terbaru yang masuk.

# - 🕒 Live Activity Stream (Feed Dashboard) :

<img width="420" alt="image" src="https://github.com/user-attachments/assets/9e1888e8-7f64-425d-b867-9fbe94ffbb42" />

## Selain 5 menu di atas, Dashboard Admin dilengkapi dengan barisan Aktivitas Absensi Terbaru yang berfungsi untuk:

## • Memberikan notifikasi visual instan mengenai siapa mahasiswa yang baru saja melakukan absensi.

## • Menampilkan jam presisi (WIB) dan status absensi secara live saat Admin membuka aplikasi.

# 🛠️ Teknologi & Spesifikasi Teknis (Tech Stack)

| Komponen | Teknologi | | :--- | :--- | | Language | Java (JDK 11) | | Networking | Retrofit 2.9.0 & OkHttp | | AI/ML | Google ML Kit Face Detection & FaceNet TFLite | | Location | Google Play Services Location (Fused Location) | | UI/UX | Material Design 3, CardView, Lottie Animation | | Backend | PHP 7.4 (RESTful API) | | Database | MySQL (Cloud) & SQLite (Local) | | Reporting | Spreadsheet Logic (HTML to XLS Stream) |

# 🗄️ Skema Database Utama (MySQL)

<img width="1914" height="414" alt="image" src="https://github.com/user-attachments/assets/1b9f33ad-5ad8-4d5f-aeb6-ed37270be217" />

## • Table users: ``` id, nama, email, password, embedding (TEXT), role (INT) ```

## • Table tb_absensi: ``` id, user_id, tanggal, jam, status, lat, lng ```

## • Table settings: ``` id, radius, jam_masuk, broadcast_msg ```

# 📝 Kesimpulan Validasi (Core Logic)

# Aplikasi ini menerapkan standar keamanan "Anti-Cheating":

## 1. Anti-Foto: Model AI dilatih untuk membedakan wajah asli dan replika.

## 2. Anti-Fake GPS: Penggunaan Fused Location Provider mempersulit penggunaan aplikasi manipulasi koordinat.

## 3. Device Integrity: Sinkronisasi Cloud menjamin data tidak dapat dimanipulasi melalui clear cache atau pembersihan data lokal oleh user.


## Di bawah ini adalah Link Folder Android Studio Project Saya, dan link download aplikasi ( jika ingin mencoba ) : 

### Link Folder Android Studio : https://drive.google.com/file/d/1cDR3nn-R3_LMhvkLk3ytWINYQP-ZEl9u/view?usp=sharing

### Link Download Aplikasi Saya : https://drive.google.com/file/d/1U1XOHtmTXr0z_YSWPCpnxTi_UPGqL4yF/view?usp=sharing 

# 👤 Developer

Fajar Fawwaz Atallah Mahasiswa Teknik Informatika - Universitas Pelita Bangsa
