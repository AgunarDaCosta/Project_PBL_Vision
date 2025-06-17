# Project_PBL_Vision (Keamanan-Lab-Kampus)

Sistem Keamanan Laboratorium Berbasis Deteksi Wajah dan Gerakan Mencurigakan Real-Time dengan Raspberry Pi dan Kamera CCTV menggunakan Artificial Intelligence (AI).

---

## Deskripsi Proyek

Proyek ini bertujuan untuk meningkatkan keamanan di laboratorium kampus melalui sistem pengawasan cerdas berbasis AI. Sistem ini tidak hanya merekam video, tetapi juga mampu:

- Mendeteksi keberadaan manusia (object detection)
- Mengidentifikasi wajah-wajah yang dikenal (face recognition)
- Mendeteksi gerakan tubuh mencurigakan (pose estimation)

Dibangun menggunakan Raspberry Pi dan kamera webcam/CCTV, sistem ini mendeteksi secara real-time dan memberikan notifikasi otomatis saat aktivitas mencurigakan terdeteksi, seperti seseorang menyembunyikan atau memindahkan barang.

---

## Metode yang Digunakan

### 1. **YOLOv5 – Object Detection**
Digunakan untuk mendeteksi keberadaan manusia secara cepat dalam setiap frame kamera. Model ini sangat efisien dan dapat berjalan dengan baik pada perangkat ringan seperti Raspberry Pi.

### 2. **Face Recognition – Identifikasi Wajah**
Menggunakan library `face_recognition` berbasis model deep learning (HOG/CNN), sistem mampu mengenali wajah-wajah terdaftar dan mengklasifikasikan wajah tidak dikenal sebagai “Unknown”.

### 3. **MediaPipe Pose Estimation – Deteksi Gerakan Mencurigakan**
Digunakan untuk melacak pose tubuh dan mendeteksi gestur yang tidak biasa, seperti:
- Tangan masuk ke saku (menyembunyikan barang)
- Mengangkat benda
- Gerakan tangan ke arah tas

---

## Teknologi yang Digunakan

- Python 3.10+
- OpenCV
- YOLOv5
- face_recognition
- MediaPipe Pose
- Flask (untuk web monitoring)
- Raspberry Pi 4 (opsional)
- Kamera USB / CCTV

---

## Hasil Pengujian

### Face Recognition
- **2 meter (terang)**: Akurasi tinggi, wajah dikenali dengan cepat.
- **3 meter (terang/gelap)**: Akurasi menurun namun masih dapat mengenali.
- **5 meter**: Bounding box tidak muncul, namun sistem secara otomatis menandai wajah sebagai “Unknown”.

### MediaPipe Pose Estimation
- Mampu mendeteksi gestur mencurigakan dengan **baik bahkan hingga jarak 5 meter**, baik dalam kondisi terang maupun pencahayaan minim.
- Nilai MSE pada jarak jauh tetap stabil, menunjukkan ketahanan terhadap perubahan cahaya.

| Jarak       | Face Recognition (MSE) | MediaPipe Pose (MSE) |
|-------------|------------------------|------------------------|
| 2 Meter     | 0.12 - 0.25            | 0.12 - 0.25            |
| 3 Meter     | 0.26 - 0.38            | 0.26 - 0.38            |
| 5 Meter     | Gagal Deteksi (Unknown)| 0.43 - 0.58            |

---

## Kesimpulan

- Sistem bekerja optimal pada **jarak 2 meter** dengan **pencahayaan terang** untuk Face Recognition.
- **MediaPipe Pose** menunjukkan akurasi tinggi bahkan pada **jarak 5 meter** dan **pencahayaan minim**, menjadikannya lebih fleksibel untuk deteksi gerakan mencurigakan.
- Sistem fallback klasifikasi wajah sebagai "Unknown" bekerja dengan baik saat bounding box tidak muncul akibat jarak atau pencahayaan.
- Sistem ini efektif digunakan sebagai solusi keamanan adaptif dan real-time untuk laboratorium atau fasilitas serupa.

---

## Cara Menjalankan Proyek

### 1. Kloning Repository
```bash
git clone https://github.com/username/Keamanan-Lab-Kampus.git
cd Keamanan-Lab-Kampus
### 2. Install Dependencies
pip install -r requirements.txt
3. Siapkan Dataset Wajah
Buat folder dataset/ dan tambahkan foto wajah:
dataset/
├── Carlos/
│   ├── 1.jpg
│   ├── 2.jpg
├── Rina/
│   ├── 1.jpg
│   ├── 2.jpg
4. Encode Wajah
python encode_faces.py
5. Jalankan Sistem
python app.py
Akses di browser: http://localhost:5000

