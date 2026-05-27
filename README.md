# Analisis Sentimen Komentar YouTube MBG

Repo ini berisi pipeline end-to-end untuk scraping komentar YouTube terkait program Makan Bergizi Gratis (MBG), pembersihan teks, pelabelan, hingga training model IndoBERT untuk analisis sentimen.

## Deskripsi dataset

| File | Jumlah baris | Kolom utama | Keterangan |
| --- | ---: | --- | --- |
| `data/raw/dataset_komentar_mbg_youtube.csv` | 1302 | author, published_at, like_count, text, public, video_id | Dataset mentah hasil scraping komentar YouTube. |
| `data/processed/dataset_komentar_mbg_youtube_processed.csv` | 1166 | author, published_at, like_count, text, public, video_id, text_clean, text_normalized, text_final, label | Dataset setelah pembersihan dan normalisasi teks. |
| `data/processed/dataset_komentar_mbg_indobert_labeled.csv` | 871 | author, published_at, like_count, text, public, video_id, text_clean, text_normalized, text_final, label, label_id, label_indobert, confidence | Dataset berlabel untuk evaluasi IndoBERT. |
| `data/processed/validation_sample_100.csv` | 100 | text, text_clean, text_normalized, text_final, label | Sampel validasi berukuran kecil. |

## Langkah menjalankan kode

1. Buat environment Python 3.10+ dan aktifkan.
2. Install dependensi. Jika memakai GPU CUDA 11.8 gunakan perintah berikut; jika CPU-only ganti baris pertama menjadi `pip install torch torchvision torchaudio`.

   ```
   pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
   pip install transformers==4.44.0 datasets==2.19.0 "accelerate>=1.1.0" scikit-learn seaborn pandas numpy matplotlib wordcloud Sastrawi google-api-python-client
   ```

3. Buka notebook `scripts\scraping_komentar_youtube_mbg_fixed (1).ipynb`.
4. Masukkan API Key YouTube Data API v3 pada cell "Masukkan API Key".
5. Jalankan cell secara berurutan dari atas sampai selesai. Output utama akan tersimpan di `data/raw`, `data/processed`, `models/indobert_mbg_sentiment`, dan `data/processed/confusion_matrix_indobert.png`.

## Visualisasi Word Cloud (sebelum vs sesudah pembersihan)

**Sebelum pembersihan**

![Word Cloud Raw](data/processed/wordcloud_raw.png)

**Sesudah pembersihan**

![Word Cloud Clean](data/processed/wordcloud_clean.png)
