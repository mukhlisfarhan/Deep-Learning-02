# Machine Translation dengan PyTorch

Proyek ini bertujuan untuk membangun dan membandingkan dua arsitektur *deep learning* untuk tugas *Machine Translation* (Penerjemahan Otomatis): **RNN dengan Mekanisme *Attention*** dan **Transformer**. Model-model ini dilatih untuk menerjemahkan teks dari bahasa Inggris (EN) ke bahasa Indonesia (ID) menggunakan *framework* PyTorch.

---

## Daftar Isi

* [Pendahuluan](#pendahuluan)
* [Dataset](#dataset)
* [Arsitektur Model](#arsitektur-model)
    * [RNN dengan Mekanisme Attention](#rnn-dengan-mekanisme-attention)
    * [Transformer](#transformer)
* [Hasil Pelatihan](#hasil-pelatihan)
* [Ablation Study: Pengaruh Ukuran Vocabulary](#ablation-study-pengaruh-ukuran-vocabulary)
* [Cara Menjalankan Proyek](#cara-menjalankan-proyek)
* [Referensi](#referensi)

---

## Pendahuluan

*Machine Translation* (MT) adalah salah satu aplikasi kunci dalam *Natural Language Processing* (NLP) yang memungkinkan penerjemahan teks secara otomatis antarbahasa. Proyek ini mengeksplorasi implementasi dan perbandingan dua arsitektur terkemuka: **Recurrent Neural Network (RNN) dengan mekanisme *attention*** dan **arsitektur Transformer** yang revolusioner.

---

## Dataset

Dataset yang digunakan terdiri dari pasangan kalimat bahasa Inggris-Indonesia. Tahapan persiapan data meliputi:

1.  **Pembersihan Teks:** Normalisasi Unicode ke ASCII, konversi ke huruf kecil, pemisahan tanda baca, dan pembersihan karakter non-alfabet.
2.  **Pembagian Data:** Dataset dibagi menjadi 80% data pelatihan, 10% data validasi, dan 10% data pengujian. Total 14881 pasangan kalimat digunakan.
3.  **Tokenisasi Subword:** Menggunakan **SentencePiece** dengan algoritma BPE (*Byte Pair Encoding*) untuk membuat *vocabulary* subword untuk kedua bahasa, dengan ukuran *vocabulary* 8000. Token khusus (`<pad>`, `<unk>`, `<bos>`, `<eos>`) ditambahkan.
4.  **DataLoader PyTorch:** Data dikemas ke dalam `TranslationDataset` dan `DataLoader` untuk memfasilitasi pelatihan *batch*.

---

## Arsitektur Model

### RNN dengan Mekanisme Attention

Model ini terdiri dari:

* **EncoderRNN:** GRU bidireksional memproses input, menggabungkan *hidden state* untuk menghasilkan *hidden state* awal dekoder.
* **Attention:** Mekanisme *attention* lugh-style yang menghitung bobot relevansi antara *hidden state* dekoder saat ini dengan semua *output* *encoder*.
* **DecoderRNN:** GRU yang menghasilkan sekuens output, dengan input berupa kombinasi *embedding* token saat ini dan *weighted sum* dari *output* *encoder*.

Model ini memiliki total **31.173.952 parameter** yang dapat dilatih.

### Transformer

Arsitektur Transformer dibangun berdasarkan mekanisme *self-attention* dan tidak menggunakan RNN rekuren. Komponen utamanya adalah:

* **TransformerEncoder:** Terdiri dari `EncoderLayer` yang mencakup *multi-head self-attention* dan *position-wise feedforward network*.
* **TransformerDecoder:** Terdiri dari `DecoderLayer` dengan dua lapisan *multi-head attention* (untuk *self-attention* target dan *attention* encoder-decoder).
* **Masking:** Masker digunakan untuk *padding* dan mencegah *decoder* melihat token masa depan.

Model ini memiliki total **10.156.864 parameter** yang dapat dilatih.

---

## Hasil Pelatihan

Kedua model dilatih selama 10 *epoch* menggunakan *optimizer* Adam dan *CrossEntropyLoss*.

| Model               | Loss Latihan Akhir | PPL Latihan Akhir | Loss Validasi Akhir | PPL Validasi Akhir | Waktu per Epoch | Total Parameter |
| :------------------ | :---------------- | :---------------- | :----------------- | :----------------- | :------------- | :-------------- |
| RNN + Attention     | 1.154             | 3.170             | 3.604              | 36.753             | ~27s           | 31,173,952      |
| Transformer (8000)  | 3.322             | 27.708            | 3.722              | 41.360             | ~5s            | 10,156,864      |

---

## Ablation Study: Pengaruh Ukuran Vocabulary

Studi ablasi dilakukan untuk menganalisis dampak ukuran *vocabulary* pada model Transformer.

| Ukuran Vocab | Epoch | Loss Validasi Akhir | PPL Validasi Akhir |
| :----------- | :---- | :------------------ | :----------------- |
| 4000         | 5     | 4.288               | 72.824             |
| 14000        | 5     | 4.285               | 72.632             |

Hasil menunjukkan bahwa ukuran *vocabulary* 8000 dengan pelatihan 10 *epoch* memberikan keseimbangan performa terbaik dibandingkan ukuran 4000 atau 14000 dengan 5 *epoch*.

---

## Cara Menjalankan Proyek

1.  **Clone repositori ini dan *branch* `machine_translation`:**
    ```bash
    git clone -b machine_translation [https://github.com/mukhlisfarhan/Deep-Learning-02.git](https://github.com/mukhlisfarhan/Deep-Learning-02.git)
    cd Deep-Learning-02
    ```
2.  **Instal dependensi:**
    ```bash
    pip install torch sentencepiece sacrebleu tqdm
    ```
3.  **Siapkan dataset:**
    Unduh *file* dataset dari [https://www.manythings.org/anki/ind-eng.zip](https://www.manythings.org/anki/ind-eng.zip) dan ekstrak `ind.txt` ke direktori proyek Anda. Pastikan *file* `ind.txt` berada di direktori yang sama atau sesuaikan `DATA_PATH` dalam kode. Contoh baris dalam `ind.txt`:
    ```
    Hello.    Halo.
    How are you?    Apa kabar?
    ```
4.  **Jalankan notebook Jupyter:**
    Buka `Machine_Translation.ipynb` dengan Jupyter Notebook atau Google Colab dan ikuti langkah-langkah di dalamnya untuk pra-pemrosesan data, pelatihan model, dan evaluasi.

---

## Referensi

[1] D. P. Kingma and M. Welling, “Auto-encoding variational Bayes,” 2013, arXiv:1312.6114. [Online]. Available: <https://arxiv.org/abs/1312.6114>

[2] K. Eves and J. Valasek, “Adaptive control for singularly perturbed systems examples,” Code Ocean, Aug. 2023. [Online]. Available: <https://codeocean.com/capsule/4989235/tree>

[3] S. Liu, “Wi-Fi Energy Detection Testbed (12MTC),” 2023, gitHub repository. [Online]. Available: <https://github.com/liustone99/Wi-Fi-Energy-Detection-Testbed-12MTC>

[4] “Treatment episode data set: discharges (TEDS-D): concatenated, 2006 to 2009.” U.S. Department of Health and Human Services, Substance Abuse and Mental Health Administration, Office of Applied Studies, August, 2013, DOI:10.3886/ICPSR30122.v2

[5] A. Vaswani, N. Shazeer, N. Parmar, J. Uszkoreit, L. Jones, A. N. Gomez, Ł. Kaiser, and I. Polosukhin, "Attention Is All You Need," *Advances in Neural Information Processing Systems 30* (NIPS 2017).
