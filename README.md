# Web QR Code Absence Scan

Proyek ini adalah sistem absensi berbasis web menggunakan pemindaian QR Code. Sistem ini terintegrasi dengan Google Sheets sebagai database melalui Google Apps Script.

## Fitur

- **Pemindaian QR Code:** Menggunakan kamera web atau ponsel untuk memindai QR code absensi.
- **Pencatatan Waktu:** Mencatat waktu kehadiran (Time In) dan kepulangan (Time Out).
- **Dashboard Absensi:** Menampilkan data absensi secara real-time yang diambil dari Google Sheets.
- **Notifikasi Kehadiran:** Memberikan alert sukses saat data berhasil dikirimkan.

## Persyaratan

- Browser modern yang mendukung HTML5 (Chrome, Firefox, Safari, dll).
- Koneksi internet (untuk integrasi Google Apps Script dan library eksternal).
- Akun Google (untuk membuat Spreadsheet dan Google Apps Script).

## Instalasi & Konfigurasi

1. **Clone Repository**
   ```bash
   git clone https://github.com/Imamabdulfatah/web-qrcode-absence-scan.git
   ```

2. **Setup Google Sheets**
   - Buat Spreadsheet baru di Google Sheets dengan nama sheet `User_Data` dan `Attendance`.
   - Di `User_Data`, buat kolom untuk Nama dan UID.
   - Di `Attendance`, kolom akan otomatis terisi oleh script.
   - Dapatkan **Spreadsheet ID** dari URL Google Sheets Anda.

3. **Penerapan di Google Apps Script**
   - Buka Spreadsheet yang baru Anda buat, lalu klik menu **Extensions > Apps Script**.
   - Pada editor Apps Script, Anda akan melihat file bernama `Code.gs`.
   - Buka file `Code.gs` dari repository ini, kemudian salin seluruh isinya dan tempelkan (paste) untuk menggantikan isi dari `Code.gs` di editor Apps Script Anda.
   - Simpan perubahan (tekan ikon save atau Ctrl+S / Cmd+S).
   - Klik tombol **Deploy** di bagian kanan atas, lalu pilih **New deployment**.
   - Pada tipe deployment, klik ikon roda gigi (gear) dan pastikan memilih **Web app**.
   - Isi bagian deskripsi jika diperlukan.
   - Pada bagian **Execute as**, pilih **Me** (akun Anda).
   - Pada bagian **Who has access**, pilih **Anyone**.
   - Klik tombol **Deploy** dan berikan otorisasi akses (Authorize Access) jika diminta oleh Google. Lanjutkan dengan memilih akun Anda (bila muncul peringatan "Google hasn't verified this app", klik "Advanced" dan lanjutkan).
   - Salin **Web App URL** yang dihasilkan. URL ini akan Anda gunakan di langkah selanjutnya.

4. **Konfigurasi Keamanan (Tokens & Keys)**
   Demi keamanan, semua token dan key telah dihapus dari source code. Anda perlu menggantinya dengan kredensial Anda sendiri:
   
   - Buka `Code.gs` di editor Apps Script Anda, dan ganti nilai variabel `sheet_id` (sekitar baris ke-47) yang bernilai `"YOUR_SPREADSHEET_ID"` dengan Spreadsheet ID milik Anda.
   - Buka `index.html` dan cari bagian form action (sekitar baris ke-122). Ganti `YOUR_GOOGLE_SCRIPT_URL_HERE` dengan **Web App URL** dari Google Apps Script Anda.
   - Buka `dashboard.html` dan cari variabel `apiUrl` di dalam fungsi `fetchData()` (sekitar baris ke-90). Ganti `YOUR_API_URL_WITH_CONTENT_KEY_HERE` dengan URL echo API Google Script Anda untuk menampilkan data dashboard.

## Penggunaan

1. Buka file `index.html` di browser Anda.
2. Berikan izin akses kamera saat diminta.
3. Arahkan QR Code ke kamera untuk melakukan absensi.
4. Data akan otomatis dikirim dan disimpan ke dalam Google Sheets.
5. Anda dapat melihat rekapan data absensi dengan membuka file `dashboard.html`.

## Keamanan

- Jangan pernah mengunggah (commit/push) URL Apps Script rahasia atau Spreadsheet ID Anda ke repository publik. Pastikan file yang berisi kredensial Anda tetap aman dan tidak tersebar.
