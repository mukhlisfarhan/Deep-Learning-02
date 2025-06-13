# Klasifikasi Gambar: [Objek 1] vs [Objek 2]

Proyek ini menggunakan transfer learning dengan ResNet50 untuk mengklasifikasikan dua jenis objek: **[Objek 1]** dan **[Objek 2]**. Dataset dikumpulkan secara mandiri dengan total 200 gambar (100 per kelas), diambil dari berbagai sudut untuk meningkatkan generalisasi.

## 📁 Struktur Proyek
- `notebook.ipynb` — Notebook utama di Kaggle
- `laporan.pdf` — Laporan teknis lengkap
- `README.md` — File ini

## 🔗 Dataset
Dataset disusun sendiri dan diupload secara lokal ke Kaggle.

## 🚀 Cara Menjalankan
1. Buka [Kaggle Notebook](LINK_KAGGLE_NOTEBOOK)
2. Jalankan semua sel (runtime ~5-10 menit)
3. Model akan dilatih dan divalidasi secara otomatis

## 🧠 Model
- Pretrained Model: ResNet50
- Input size: 224x224
- Optimizer: Adam
- Epochs: 10
- Augmentasi: `ImageDataGenerator`

## 📊 Hasil Singkat
- Akurasi Validasi: XX.XX%
- Precision / Recall: lihat laporan lengkap

## 📎 Tautan
- 📘 Kaggle Notebook: [LINK_KAGGLE_NOTEBOOK]
- 💾 GitHub Repo: [LINK_GITHUB]

