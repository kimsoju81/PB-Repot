# 🛡️ Sistem Aplikasi Rasmi Polis Bantuan UTeM

Aplikasi web mudah alih (Single-Page Application) khusus untuk warga **Polis Bantuan Universiti Teknikal Malaysia Melaka (UTeM)** bagi menguruskan dokumentasi harian, buku poket, laporan formal, repot polis, dan perharian balai dengan pantas, teratur, dan patuh piawaian rasmi.

---

## ✨ Ciri-Ciri Utama & Aliran Kerja (2-Layer Workflow)
Setiap modul di dalam aplikasi ini direka dengan sistem 2 lapisan:
1. **Layer 1 (Borang Input / Smart OCR):** Antaramuka borang mesra mudah alih untuk memasukkan data mentah atau menggunakan fungsi **Kamera AI OCR** bagi membaca dan menyusun semula tulisan tangan daripada buku fizikal secara automatik.
2. **Layer 2 (Output Dokumen Rasmi):** Paparan dokumen rasmi yang dijana secara *real-time* lengkap dengan tera air (watermark), garisan jadual penuh, dan susun atur format rasmi yang boleh dikongsi terus melalui **PDF, WhatsApp, dan Emel**.

---

## 📂 Modul Sistem
* **Buku Poket Polima:** Rekod aktiviti harian mengikut format saiz ISO A6 landscape dengan pengiraan baris automatik.
* **Laporan Formal:** Templat surat rasmi/memo keselamatan untuk rujukan pentadbiran dan kepimpinan.
* **Repot Polis Bantuan:** Borang laporan rasmi berseksyen (Balai, Pengadu, Penerima, dan Keterangan) dengan cetakan automatik tanpa tandatangan fizikal.
* **Buku Station Diary (POL. 40):** Modul perharian balai berformat landskap 6 kolum lengkap dengan fungsi carian imej tulisan tangan fizikal (hardcopy).

---

## 🎨 Tema Warna Rasmi
* **Putih Bersih (`#FFFFFF`)** — Latar belakang utama.
* **Biru Navy Gelap (`#001B3A`)** — Header dan butang navigasi utama.
* **Kuning Emas (`#FFD700`)** — Warna aksen, lencana, dan border penyerlahan.
* **Hitam (`#000000`)** — Teks dan garisan sempadan jadual rasmi.

---

## 🛠️ Stack Teknologi
* **Frontend:** HTML5, CSS3 (Flexbox/Grid), JavaScript (Vanilla JS)
* **Pustaka Dokumen:** `html2pdf.js` untuk penjanaan fail PDF bersaiz tepat (ISO A6 & A4).
* **AI Engine:** Google Gemini API (Multimodal Vision) untuk pengecaman tulisan tangan (*Handwriting OCR* & *Semantic Mapping*).
