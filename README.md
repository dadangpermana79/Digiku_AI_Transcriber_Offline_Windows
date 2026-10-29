# DIGIKU AI Transcriber — Offline Windows Edition

**Offline AI Transcription Studio** — ubah audio & video menjadi teks, seluruhnya di
komputer Anda sendiri. Tanpa cloud, tanpa API berbayar, tanpa internet setelah instalasi.

## Ringkasan Produk

DIGIKU AI Transcriber adalah aplikasi desktop berbasis web (FastAPI + browser) yang
menjalankan mesin **faster-whisper** secara lokal di Windows. Mendukung akselerasi
GPU NVIDIA (CUDA) dengan fallback CPU (int8).

## Fitur Utama

- 🎙️ **Transkripsi audio & video** — MP3, WAV, M4A, AAC, FLAC, OGG, WMA, MP4, MOV, MKV, WEBM
- ⚡ **Akselerasi GPU (CUDA)** — otomatis mendeteksi GPU, fallback CPU jika tidak ada
- 🌐 **Deteksi bahasa otomatis** + pilihan Bahasa Indonesia / English
- 📊 **Progress real-time** — tahap proses, waktu berjalan, persentase (dari posisi segmen)
- ✏️ **Editor transkrip** — segmen ber-timestamp, bisa diedit, cari, salin
- 📤 **Ekspor** TXT / SRT / VTT (UTF-8, timestamp benar)
- 🗂️ **Riwayat job** — status, durasi, model, buka ulang, hapus
- 🔒 **100% offline** — bind ke `127.0.0.1`, tanpa telemetri, tanpa CDN

## Kebutuhan Sistem

| Komponen | Minimum | Disarankan |
|---|---|---|
| OS | Windows 10/11 64-bit | Windows 11 64-bit |
| Python | 3.11 | 3.11 |
| RAM | 8 GB | 32 GB |
| GPU | — | NVIDIA RTX 3050 (6 GB VRAM, CUDA) |
| FFmpeg | wajib (ffmpeg + ffprobe) | versi terbaru |

## Mulai Cepat

1. `install.bat` — buat environment & pasang dependensi
2. `download_models.bat` — unduh model (default: `small`)
3. `start.bat` — jalankan (auto GPU/CPU), browser terbuka otomatis
   - atau `start_cpu.bat` — paksa mode CPU

Buka `http://127.0.0.1:8000` di browser.

## Struktur Proyek

```
Digiku_AI_Transcriber/
├── app/            # backend FastAPI + mesin transkripsi
├── static/         # frontend (HTML/CSS/JS, tanpa CDN)
├── tests/          # automated test (pytest)
├── models/         # model Whisper lokal (diunduh)
├── uploads/        # file sementara upload
├── outputs/        # (disediakan untuk ekspor masa depan)
├── logs/           # log aplikasi
├── data/           # database SQLite (riwayat job)
├── install.bat / download_models.bat / start.bat / start_cpu.bat / stop.bat
├── requirements.txt / config.example.env
└── README / INSTALLATION_GUIDE / USER_GUIDE / TROUBLESHOOTING
```

## Dokumentasi

- `INSTALLATION_GUIDE.md` — prasyarat & instalasi Windows
- `USER_GUIDE.md` — panduan penggunaan
- `TROUBLESHOOTING.md` — pemecahan masalah umum

## Lisensi

MIT — lihat `LICENSE`.
