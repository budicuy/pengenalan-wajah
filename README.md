# Aplikasi Pengenalan Wajah Mahasiswa (Webcam Real-Time)

Aplikasi berbasis Python Jupyter Notebook untuk melakukan pengenalan wajah mahasiswa secara real-time dari kamera/webcam. Aplikasi menggunakan pustaka `face-recognition` (berbasis `dlib`) dan `OpenCV`.

## 📁 Struktur Direktori
* `dataset/` : Tempat menyimpan foto wajah mahasiswa referensi (berisi 30 berkas gambar).
* `venv/` : Lingkungan virtual Python (virtual environment) berisi seluruh dependensi.
* `main.ipynb` : Berkas notebook utama tempat menjalankan aplikasi.

## 🚀 Langkah Menjalankan Aplikasi

### 1. Aktifkan Virtual Environment
Buka terminal di VSCode dan jalankan perintah berikut:
```bash
source venv/bin/activate
```

### 2. Pilih Kernel Python di VSCode
1. Buka file `main.ipynb` di VSCode.
2. Di pojok kanan atas, klik **Select Kernel** -> **Python Environments...**
3. Pilih kernel python dari path `./venv/bin/python`.

### 3. Jalankan Jupyter Notebook
Jalankan setiap cell di dalam `main.ipynb` secara berurutan:
1. **Cell Langkah 1**: Memuat semua library.
2. **Cell Langkah 2**: Memindai gambar di folder `dataset/` dan menyimpan pola wajah mahasiswa.
3. **Cell Langkah 3**: Menyalakan kamera dan melakukan pengenalan wajah real-time.

> **PENTING**: Tekan tombol **'q'** pada keyboard (saat jendela tampilan kamera aktif) untuk menghentikan program dan mematikan kamera secara aman.

## 🔍 Troubleshooting: NameError: name 'quit' is not defined saat Import
Jika Anda menemui error `NameError: name 'quit' is not defined` saat menjalankan cell **Langkah 1 (Import)**:
* **Penyebab**: Modul `face_recognition` membutuhkan modul `pkg_resources` yang telah dihapus di versi `setuptools` terbaru (>= 82.0.0) pada Python 3.14. Hal ini menyebabkan kegagalan import yang memicu panggilan internal fungsi `quit()` yang tidak dikenali oleh Jupyter.
* **Solusi**: Kami telah menurunkan (*downgrade*) versi `setuptools` di dalam `venv` ke versi `<82`.
* **Tindakan Anda**: Cukup klik tombol **"Restart Kernel"** (ikon putar melingkar ↻) di bagian atas menu VSCode Jupyter Notebook Anda, lalu jalankan kembali sel kodenya.

