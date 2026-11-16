# Preprocessing Teks Ulasan E-Commerce Bahasa Indonesia

Tugas Natural Language Processing — analisis sentimen pada dataset ulasan *e-commerce* berbahasa
Indonesia, mulai dari pemeriksaan dataset sampai lima tahap *text preprocessing*.

| | |
|---|---|
| **Nama** | Hafiz Syauqi |
| **NIM** | 20146071 |
| **Mata kuliah** | Natural Language Processing (Pemrosesan Bahasa Alami) |
| **Dataset** | [dipawidia/ecommerce-product-reviews-sentiment](https://huggingface.co/datasets/dipawidia/ecommerce-product-reviews-sentiment) |

## Isi Repository

| Berkas | Keterangan |
|---|---|
| `tugas_nlp_preprocessing.ipynb` | Notebook utama: informasi dataset, 5 tahap preprocessing, 10 contoh sebelum/sesudah, dan analisis pengaruh preprocessing. Sudah dieksekusi, output tersimpan di dalamnya. |
| `Laporan_NLP_Hafiz_Syauqi_20146071.pdf` | Laporan tertulis hasil dari notebook (dibuat dari notebook yang sama, jadi angkanya identik). |
| `data/labeledReview.datasetFix.json` | Salinan dataset (11.606 ulasan) agar tidak perlu unduh ulang dari Hugging Face. |
| `requirements.txt` | Daftar pustaka Python yang dibutuhkan. |

## Cara Menjalankan

```bash
# 1. clone
git clone https://github.com/hafiz-syq/tugas-nlp-sentimen-ecommerce.git
cd tugas-nlp-sentimen-ecommerce

# 2. virtual environment (Windows)
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt

# 3. jalankan notebook
jupyter notebook tugas_nlp_preprocessing.ipynb
```

Jalankan seluruh sel berurutan dari atas (`Kernel → Restart & Run All`). Dataset sudah disertakan di
`data/labeledReview.datasetFix.json`, jadi tidak perlu mengunduh dari Hugging Face lagi. Koneksi
internet hanya diperlukan pada eksekusi pertama, ketika NLTK mengambil paket `stopwords` bahasa
Indonesia; setelah tersimpan di folder `nltk_data`, notebook bisa dijalankan sepenuhnya offline.

Catatan: tahap *stemming* Sastrawi berjalan per kata dan menjadi bagian paling berat — durasi untuk
seluruh korpus dicetak sendiri di bagian 4.6 notebook (pada mesin penulis sekitar 8 menit).

## Tahap Preprocessing yang Dikerjakan

1. **Case folding** — seluruh huruf menjadi kecil.
2. **Cleaning** — URL, penyebutan akun/*hashtag*, angka & harga, tanda baca, emoji, karakter khusus dihapus.
3. **Tokenisasi** — teks dipecah menjadi token kata dengan `nltk.tokenize.RegexpTokenizer`
   (pola `[a-z]+`, sehingga hanya deret huruf yang tersisa sebagai token).
4. **Stopword removal** — kata umum bahasa Indonesia dibuang (daftar *stopword* NLTK).
5. **Stemming** — kata berimbuhan dikembalikan ke bentuk dasar dengan **Sastrawi**.

## Ringkasan Dataset

| | |
|---|---|
| Jumlah data | 11.606 baris × 3 kolom |
| Kolom | `review` (teks ulasan), `sentimen` (1 = positif, 0 = negatif), `translate` (terjemahan Inggris, tidak dipakai) |
| Distribusi label | negatif 5.803 dan positif 5.803 — seimbang (50 % : 50 %) |

Hasil pengukuran dampak preprocessing (jumlah token, kosakata unik, *type-token ratio*, dan
sebaran panjang ulasan) dihitung pada seluruh korpus dan dicetak langsung di bagian 6 notebook.
