# Tugas Individu: Eksplorasi Autoencoder

## Deskripsi
Eksplorasi autoencoder berbasis CNN menggunakan dataset Fashion MNIST. Tujuan proyek adalah memahami representasi laten dan struktur encoder-decoder.

## Isi Repo
- `eksplorasi-autoencoder.ipynb`: Notebook utama dengan semua eksperimen
- `laporan.pdf`: Laporan reflektif tugas
- `README.md`: Ringkasan dan petunjuk eksekusi

## Cara Menjalankan
1. Clone repo ini
2. Jalankan `eksplorasi-autoencoder.ipynb` di Jupyter/Kaggle Notebook
3. Pastikan sudah install library: `torch`, `torchvision`, `matplotlib`, `numpy`

Atau:
1. Buka [Notebook](https://www.kaggle.com/code/ahmadmukhlisfarhan/eksplorasi-autoencoder) di Kaggle.
2. Jalankan sel berturut-turut (data sudah tersedia di Kaggle)
3. Lihat hasil evaluasi di bagian akhir notebook

## Hasil Singkat
- Model autoencoder berhasil merekonstruksi citra Fashion MNIST
- Eksperimen dengan variasi latent space menunjukkan perbedaan kualitas hasil
- Visualisasi latent space menggunakan PCA memberikan insight tentang clustering

## Refleksi
Tugas ini membantu saya memahami cara kerja autoencoder, serta pentingnya eksplorasi arsitektur untuk memperoleh hasil optimal.
