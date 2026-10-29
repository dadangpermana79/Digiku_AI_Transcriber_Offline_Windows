# Pemecahan Masalah — DIGIKU AI Transcriber

## Python tidak terdeteksi

**Gejala:** `install.bat` menampilkan "Python tidak ditemukan".

**Solusi:**
1. Instal Python 3.11 dari https://www.python.org/downloads/
2. Saat instalasi, centang **"Add Python to PATH"**.
3. Tutup & buka ulang Command Prompt, lalu `python --version`.

## FFmpeg tidak ditemukan

**Gejala:** "FFmpeg TIDAK ditemukan di PATH" atau upload gagal "ffprobe tidak ditemukan".

**Solusi:**
```
winget install Gyan.FFmpeg
```
lalu restart Command Prompt. Verifikasi: `ffmpeg -version` dan `ffprobe -version`.

## CUDA tidak tersedia

**Gejala:** pil status menampilkan "💻 CPU (int8)".

**Kemungkinan penyebab & solusi:**
1. Driver NVIDIA belum terpasang → `nvidia-smi` (jika "not recognized", pasang driver).
2. Driver terlalu lama → perbarui dari https://www.nvidia.com/download/ (target ≥ 550).
3. GPU bukan NVIDIA / tidak mendukung CUDA → gunakan CPU (`start_cpu.bat`).

## cuDNN DLL errors

**Gejala:** error `cudnn...dll` atau `CUDA runtime` saat mulai transkripsi.

**Solusi:**
- Library CUDA/cuDNN dibundel dalam `ctranslate2`; error biasanya berarti versi driver
  tidak cocok. Perbarui driver NVIDIA ke ≥ 550.
- Pastikan tidak ada `CUDA_PATH`/`LD_LIBRARY_PATH` yang menunjuk CUDA Toolkit berbeda
  dan bertabrakan.

## GPU out of memory (OOM)

**Gejala:** transkripsi gagal dengan pesan "out of memory" / "CUDA error".

**Solusi:**
1. Ganti model ke `small`/`base`/`tiny`.
2. Pilih perangkat **CPU** untuk audio sangat panjang.
3. Tutup aplikasi lain yang memakai VRAM (game, editor, dll).

## Model belum diunduh (missing model)

**Gejala:** transkripsi gagal "model ... tidak ditemukan".

**Solusi:** jalankan `download_models.bat small` (atau model yang dipilih).

## Port sudah dipakai

**Gejala:** `[Errno 10048] error while attempting to bind on address` / "address in use".

**Solusi:**
```
stop.bat
```
atau ganti port di `.env`:
```
PORT=8001
```
lalu jalankan ulang dan buka `http://127.0.0.1:8001`.

## Transkripsi lambat

- Pastikan GPU aktif (pil "⚡ GPU").
- Gunakan model lebih kecil (`tiny`/`base`).
- Turunkan beam size (misal 3).
- Aktifkan VAD filter.

## Upload gagal

- Periksa format file (daftar format didukung ada di README).
- Periksa ukuran ≤ 200 MB dan durasi ≤ 2 jam 30 menit.
- Pastikan FFmpeg terpasang (ffprobe dipakai untuk validasi).

## Aplikasi tidak bisa start

**Solusi:**
1. `install.bat` ulang (pastikan tidak ada error saat pip install).
2. Pastikan `.venv` ada. Jika hilang, jalankan `install.bat` lagi.
3. Jalankan manual untuk melihat error lengkap:
   ```
   .venv\Scripts\activate
   python -m uvicorn app.main:app --host 127.0.0.1 --port 8000
   ```

## Masih bermasalah?

Buka `http://127.0.0.1:8000/api/health` dan `http://127.0.0.1:8000/api/system` —
kedua endpoint ini menampilkan status kesehatan sistem (FFmpeg, GPU, model).
