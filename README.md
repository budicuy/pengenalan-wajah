# Aplikasi Pengenalan Wajah Mahasiswa (Real-Time Webcam)

Aplikasi berbasis Python Jupyter Notebook (`main.ipynb`) yang digunakan untuk mendeteksi dan mengenali wajah mahasiswa secara *real-time* melalui kamera/webcam. Aplikasi ini memanfaatkan pustaka **face-recognition** (berbasis algoritma Deep Learning dlib) untuk pencocokan wajah dan **OpenCV** untuk pemrosesan video.

## 📁 Struktur Direktori
* `dataset/` : Tempat menyimpan foto wajah referensi mahasiswa (format gambar `.jpg`, `.jpeg`, atau `.png`).
* `venv/` : Lingkungan virtual Python (virtual environment) tempat seluruh dependensi diinstal.
* `main.ipynb` : File notebook utama tempat Anda menjalankan program sel demi sel.
* `README.md` : Dokumentasi panduan instalasi dan penggunaan aplikasi ini.

---

## 🛠️ Prasyarat Sistem (Prerequisites)

Sebelum melakukan instalasi, pastikan sistem Anda memiliki alat kompilasi berikut karena pustaka `dlib` membutuhkan proses kompilasi C++ dari *source code*:

### 1. Linux (Debian/Ubuntu/Arch/Fedora)
Pastikan Anda memiliki compiler C++ (`g++`), `cmake`, dan python development headers.
* **Arch Linux**: `sudo pacman -S gcc cmake python-pip`
* **Ubuntu/Debian**: `sudo apt update && sudo apt install build-essential cmake python3-dev`

### 2. Windows
* Pasang **CMake** (bisa melalui installer resmi atau `pip install cmake`).
* Pasang **Visual Studio Build Tools** dengan memilih beban kerja *Desktop Development with C++*.

---

## 🚀 Panduan Instalasi dan Setup Dependensi

Ikuti langkah-langkah di bawah ini untuk menyiapkan lingkungan pengembangan dari awal:

### Langkah 1: Kloning Repositori
Masuk ke direktori proyek Anda di terminal:
```bash
cd pengenalan-wajah
```

### Langkah 2: Buat & Aktifkan Virtual Environment
Sangat direkomendasikan menggunakan virtual environment agar dependensi proyek tidak mengganggu Python global sistem Anda.

* **Membuat Virtual Environment:**
  ```bash
  python -m venv venv
  ```

* **Mengaktifkan Virtual Environment:**
  * **Linux/macOS:**
    ```bash
    source venv/bin/activate
    ```
  * **Windows (PowerShell):**
    ```powershell
    .\venv\Scripts\Activate.ps1
    ```
  * **Windows (CMD):**
    ```cmd
    .\venv\Scripts\activate.bat
    ```
  *(Jika berhasil aktif, akan muncul tanda `(venv)` di sebelah kiri prompt terminal Anda).*

### Langkah 3: Instal Dependensi & Penanganan Masalah Kompatibilitas Python 3.14+
Untuk menghindari masalah kompatibilitas pada Python versi baru (seperti Python 3.14) di mana modul `pkg_resources` telah dihapus dari `setuptools` terbaru, kita wajib membatasi versi `setuptools` di bawah versi 82 sebelum memasang pustaka `face_recognition`.

Jalankan perintah instalasi berikut di dalam virtual environment Anda yang aktif:
```bash
# 1. Upgrade pip ke versi terbaru
pip install --upgrade pip

# 2. Downgrade/Kunci versi setuptools di bawah 82
pip install "setuptools<82"

# 3. Instal pustaka utama pengenalan wajah, OpenCV, dan kernel Jupyter
pip install face-recognition opencv-python numpy ipykernel
```
*(Catatan: Proses instalasi `face-recognition` akan mengompilasi `dlib` secara otomatis. Proses ini mungkin memakan waktu beberapa menit).*

### Langkah 4: Siapkan Dataset Foto Mahasiswa
Masukkan foto mahasiswa Anda ke dalam folder `dataset/`.
* Penamaan file secara otomatis akan menjadi nama mahasiswa yang terdaftar di sistem.
* Contoh: File foto bernama `Budi (1).JPG` atau `Budi.jpg` akan terdaftar sebagai mahasiswa bernama **Budi**.
* Format gambar yang didukung: `.jpg`, `.jpeg`, `.png` (sensitif terhadap huruf kapital ekstensi).

---

## 💻 Cara Menjalankan di VSCode

1. Buka folder proyek ini di **VSCode**.
2. Pastikan ekstensi **Python** dan **Jupyter** sudah terpasang di VSCode Anda.
3. Buka file [main.ipynb](file:///home/budi/Projects/pengenalan-wajah/main.ipynb).
4. **Pilih Kernel Jupyter yang Tepat:**
   * Di pojok kanan atas jendela notebook, klik tombol **"Select Kernel"**.
   * Pilih opsi **"Python Environments..."**.
   * Pilih kernel dari virtual environment yang sudah dibuat: `./venv/bin/python` (atau kernel berlabel `venv`).
5. Jalankan setiap sel (*cell*) kode secara berurutan dengan menekan tombol **Play** di samping kiri setiap sel:
   * **Cell 1**: Mengimpor pustaka.
   * **Cell 2**: Memindai direktori `dataset/` dan membuat database pola wajah (*face encodings*) mahasiswa.
   * **Cell 3**: Mengaktifkan kamera/webcam untuk mulai melakukan pengenalan wajah real-time.

> [!IMPORTANT]
> **Cara Menutup Kamera:**
> Untuk menghentikan kamera dan menutup jendela video secara aman, klik pada jendela video yang muncul lalu **tekan tombol huruf 'q'** di keyboard Anda. Menutup jendela secara paksa melalui tombol silang (X) dapat menyebabkan kamera tersangkut (*freezing/stuck*).

---

## 🔍 Troubleshooting

### 1. Error `NameError: name 'quit' is not defined` saat import
* **Penyebab**: Terjadi kegagalan import dependensi karena versi `setuptools` Anda di atas versi 82 yang tidak lagi menyertakan `pkg_resources`.
* **Solusi**: Pastikan Anda sudah menjalankan perintah `pip install "setuptools<82"` di dalam virtual environment, lalu klik tombol **"Restart Kernel"** (ikon putar melingkar ↻) di VSCode Jupyter untuk memuat ulang modul.

### 2. Error kompilasi `dlib` saat menjalankan `pip install`
* **Penyebab**: Komputer Anda belum memiliki compiler C++ (GCC/g++) atau pustaka CMake yang diperlukan untuk membangun biner `dlib`.
* **Solusi**: Ikuti bagian **Prasyarat Sistem** di atas untuk menginstal compiler C++ dan CMake yang sesuai dengan sistem operasi Anda.
