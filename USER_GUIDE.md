# Panduan Pengguna — DIGIKU AI Transcriber

## Menjalankan Aplikasi

- **GPU (otomatis):** jalankan `start.bat`
- **Paksa CPU:** jalankan `start_cpu.bat`
- Browser terbuka otomatis ke `http://127.0.0.1:8000`
- **Berhenti:** tekan `Ctrl+C` di jendela server, atau jalankan `stop.bat`

## Antarmuka

Dashboard terdiri dari 6 bagian:

1. **Unggah File** — seret & lepas atau pilih file
2. **Pengaturan AI** — model, bahasa, perangkat, opsi lanjutan
3. **Proses** — mulai transkripsi, batalkan, pantau progress
4. **Editor Transkrip** — edit teks per segmen
5. **Ekspor** — unduh TXT / SRT / VTT
6. **Riwayat** — daftar job sebelumnya

## Mengunggah File

1. Klik area unggah atau seret file ke sana.
2. Format didukung: MP3, WAV, M4A, AAC, FLAC, OGG, WMA, MP4, MOV, MKV, WEBM.
3. Batas bawaan: **200 MB** dan **2 jam 30 menit** (dapat diubah di `.env`).

## Memilih Model

- **Tiny** — tercepat, akurasi rendah
- **Base** — cepat
- **Small** — seimbang (disarankan)
- **Medium** — terakurat, paling lambat & butuh VRAM besar

## Memilih Bahasa

- **Auto Detect** — bahasa dideteksi otomatis
- **Bahasa Indonesia** — paksa transkripsi bahasa Indonesia
- **English** — paksa transkripsi bahasa Inggris

## Memilih Perangkat

- **Auto** — GPU jika tersedia, selain itu CPU
- **GPU (CUDA)** — hanya tersedia jika GPU terdeteksi
- **CPU** — mode CPU (int8), lebih lambat tapi hemat VRAM

## Pengaturan Lanjutan

- **Beam size** (1–10) — nilai lebih besar = lebih akurat tapi lebih lambat (default 5)
- **Filter VAD** — melewatkan bagian senyap/jeda (default aktif)

## Menjalankan Transkripsi

1. Pilih file.
2. Atur model/bahasa/perangkat.
3. Klik **"Mulai Transkripsi →"**.
4. Pantau progress (tahap, persentase, waktu berjalan).
5. Klik **"✕ Batalkan"** untuk menghentikan proses.

## Mengedit Transkrip

- Setelah selesai, editor menampilkan segmen ber-timestamp.
- Edit teks langsung di kotak teks.
- **Cari**: ketik di kotak pencarian untuk menyorot segmen.
- **Salin**: menyalin seluruh teks ke clipboard.
- **Simpan Edit**: menyimpan perubahan (ekspor akan memakai teks terbaru).

## Mengekspor

- **TXT** — teks polos
- **SRT** — subtitle dengan timestamp `HH:MM:SS,mmm`
- **VTT** — subtitle web dengan timestamp `HH:MM:SS.mmm`

## Mengelola Riwayat

- Semua job tercatat di **Riwayat** (nama file, waktu, durasi, model, status).
- **Buka** — membuka ulang transkrip yang selesai.
- **Hapus** — menghapus job dan file terkait (dengan konfirmasi).

## Berjalan Sepenuhnya Offline

Setelah instalasi dan unduh model, putuskan koneksi internet — semua fitur
(transkripsi, edit, ekspor) tetap berfungsi. Aplikasi hanya bind ke `127.0.0.1`
dan tidak mengirim data apa pun ke luar.
