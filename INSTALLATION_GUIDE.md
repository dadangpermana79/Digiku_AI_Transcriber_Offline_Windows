# Panduan Instalasi — DIGIKU AI Transcriber (Windows)

Panduan ini menjelaskan semua prasyarat dan langkah instalasi agar aplikasi berjalan
dengan akselerasi GPU (atau CPU) secara offline.

## 1. Prasyarat

| Prasyarat | Wajib? | Keterangan |
|---|---|---|
| Windows 10/11 64-bit | Ya | — |
| Python 3.11 | Ya | Pastikan "Add Python to PATH" dicentang |
| FFmpeg | Ya | ffmpeg + ffprobe untuk validasi media |
| Driver NVIDIA | Opsional | Hanya untuk akselerasi GPU (CUDA) |
| Koneksi internet | Sekali | Hanya saat instalasi & unduh model |

## 2. Instal Python 3.11

1. Unduh dari https://www.python.org/downloads/windows/
2. Pilih **Python 3.11** (Windows installer 64-bit).
3. **PENTING**: centang **"Add Python to PATH"** saat instalasi.
4. Verifikasi di Command Prompt:
   ```
   python --version
   ```
   Harus menampilkan `Python 3.11.x`.

## 3. Instal FFmpeg

FFmpeg digunakan untuk memvalidasi konten media (ffprobe).

**Cara cepat (winget):**
```
winget install Gyan.FFmpeg
```
**Cara manual:**
1. Unduh build dari https://www.gyan.dev/ffmpeg/builds/ (pilih `release-essentials`).
2. Ekstrak, salin folder `bin` (berisi `ffmpeg.exe`, `ffprobe.exe`).
3. Tambahkan path folder `bin` ke PATH sistem.

**Verifikasi:**
```
ffmpeg -version
ffprobe -version
```

## 4. Driver NVIDIA & CUDA/cuDNN (untuk GPU)

Mesin transkripsi (`faster-whisper` + `ctranslate2`) **membundel library CUDA dan
cuDNN di dalam paket pip** — Anda **tidak perlu** menginstal CUDA Toolkit atau cuDNN
secara terpisah. Yang dibutuhkan hanya **driver NVIDIA**.

- Paket `ctranslate2 4.5.x` membundel **CUDA 12.x + cuDNN 9.x**.
- Driver NVIDIA **≥ 550** disarankan (mendukung CUDA 12.4).
- GPU target: **RTX 3050** (arsitektur Ampere, `sm_86`) — didukung penuh.

**Verifikasi driver:**
```
nvidia-smi
```
Jika versi driver lebih lama, perbarui dari https://www.nvidia.com/download/

**Jika GPU tidak tersedia / driver lama:** aplikasi tetap berjalan dengan CPU (int8)
melalui `start_cpu.bat`.

## 5. Instalasi Aplikasi

1. Ekstrak `Digiku_AI_Transcriber_Offline_Windows.zip` ke folder (misal `D:\Digiku`).
2. Buka folder tersebut, jalankan:
   ```
   install.bat
   ```
   Script akan:
   - Mendeteksi Python
   - Membuat virtual environment `.venv`
   - Menginstal dependensi (`requirements.txt`)
   - Memeriksa FFmpeg
   - Memeriksa GPU NVIDIA (`nvidia-smi`)
   - Menyiapkan direktori (`models`, `uploads`, `outputs`, `logs`, `data`)

## 6. Unduh Model AI

```
download_models.bat
```
Secara default mengunduh model `small`. Untuk model lain:
```
download_models.bat tiny base small medium
```
Model disimpan di folder `models/` (diunduh sekali, lalu sepenuhnya offline).

| Model | Ukuran ± | Akurasi | Kecepatan |
|---|---|---|---|
| tiny | ~75 MB | rendah | tercepat |
| base | ~145 MB | cukup | cepat |
| small | ~484 MB | baik | seimbang |
| medium | ~1.5 GB | tinggi | lambat |

## 7. Verifikasi GPU

1. Jalankan `start.bat`.
2. Buka `http://127.0.0.1:8000`.
3. Perhatikan pil status di kanan atas: **"⚡ GPU: … (float16)"** berarti GPU aktif,
   **"💻 CPU (int8)"** berarti berjalan di CPU.

## 8. Selesai

Aplikasi siap digunakan. Lihat `USER_GUIDE.md` untuk cara pakai.
