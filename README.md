# PB Repot — Sistem Dokumen & Laporan Polis Bantuan

Aplikasi web progresif (**PWA**) untuk pengurusan rekod, penyediaan dokumen rasmi, dan rujukan operasi harian **Polis Bantuan** di Malaysia. Dibina menggunakan React 19, TypeScript, Tailwind CSS v4, Vite 8, dan pelayan Express.

---

## Ciri & Modul Utama

1. **Buku Poket Polima (A6)**
   - Catatan tugasan harian dan rondaan mengikut format buku poket rasmi berserta pengiraan jam bertugas.
   - Sokongan mod nota pantas (*note taking*) dan penjimatan terus ke arkib tempatan.

2. **Laporan Formal (A4)**
   - Penyediaan laporan eksekutif formal termasuk sokongan penjanaan/penstrukturan laporan automatik melalui pelayan (`/api/generate-report` menggunakan Gemini API).
   - Pra-tonton cetakan A4 berformat rasmi dengan logo dan tera air agensi tersuai.

3. **Repot Polis Bantuan (A4)**
   - Borang penyediaan repot Polis Bantuan mengikut susun atur rasmi dengan sokongan tandatangan, maklumat pengadu/pegawai, dan eksport terus ke fail Microsoft Word (`.docx`) serta cetakan PDF/A4.

4. **Buku Station Diary (POL. 40)**
   - Rekod Perharian Balai mengikut format buku daftar harian balai Polis Bantuan.

5. **Arkib & Perpustakaan Rujukan**
   - **Arkib Dokumen**: Simpanan tempatan, carian, sandaran, serta import/eksport fail JSON.
   - **Perpustakaan Rujukan**: Himpunan bahan rujukan perundangan dan operasi Polis Bantuan termasuk Akta Polis 1967 (Akta 344), Kanun Keseksaan (Akta 574), Kanun Tatacara Jenayah (Akta 593), Akta Perhimpunan Aman (Akta 736), PTKPN H602 & PTKPN Wajib Tahu, APJ & Pendaftaran Negara, Senjata Berjadual (T-Baton), Kawad Kaki PDRM, Garis Panduan Pakaian Seragam, Panduan Penugasan MAPA, Undang-undang Am Malaysia, serta Buku Lagu.

6. **Tetapan Agensi, Profil & Kebolehcapaian**
   - Pengurusan profil pegawai, pilihan agensi/logo/tera air tersuai, penskalaan saiz teks global (`Normal` hingga `+4`), dan tetapan aturan aplikasi.

---

## Keupayaan Progressive Web App (PWA)

Aplikasi ini menyokong pemasangan penuh sebagai PWA merentas desktop dan peranti mudah alih melalui `public/manifest.json` dan Service Worker (`src/sw.ts` via `vite-plugin-pwa`):

- **Butang Pasang Aplikasi**: Butang **"Pasang Aplikasi"** pada papan pemuka utama dan tab Aturan dalam Tetapan (menyokong `beforeinstallprompt` pada Chromium/Android dan panduan pemasangan Safari iOS).
- **Sokongan Luar Talian (*Offline*)**: Cache aset teras dan sumber aplikasi supaya modul serta arkib kekal boleh diakses tanpa sambungan internet.
- **Paparan & Integrasi OS**:
  - `display_override` menyokong mod `tabbed` (`tab_strip`), `window-controls-overlay`, `standalone`, dan `minimal-ui`.
  - `edge_side_panel`, `launch_handler` (`focus-existing`), `scope_extensions`, `related_applications`, dan `iarc_rating_id`.
  - `screenshots` (paparan mudah alih `narrow`, desktop `wide`, dan pratonton widget).
- **Pintasan & Pengendali (*Handlers*)**:
  - `shortcuts` terus ke modul Polima, Laporan Formal, Repot Polis Bantuan, dan Station Diary.
  - `note_taking` untuk catatan pantas Buku Poket Polima.
  - `file_handlers` untuk membuka fail sandaran `.json` dan nota `.txt`.
  - `protocol_handlers` menggunakan skema `web+pbreport://`.
  - `share_target` untuk menerima teks atau pautan yang dikongsi daripada aplikasi lain ke dalam Arkib Polima.
- **Widget, Penyegerakan Latar Belakang & Notifikasi**:
  - `widgets` menggunakan templat Adaptive Card (`/widgets/pbreport-template.json` dan `/widgets/pbreport-data.json`).
  - **Background Sync API** (`pbreport-sync-records`) dan **Periodic Sync API** (`pbreport-periodic-refresh`).
  - **Web Push Notifications API** untuk pemberitahuan status penyegerakan dan peringatan.

---

## Teknologi Yang Digunakan

- **Bahagian Hadapan (*Frontend*)**: React 19, TypeScript, Vite 8, Tailwind CSS v4, Lucide React, Motion
- **Dokumen**: `docx` (penjanaan fail `.docx` serta muat turun HTTP sejagat untuk pelayar mudah alih/WebView)
- **PWA**: `vite-plugin-pwa` (strategi `injectManifest` dengan `src/sw.ts`)
- **Bahagian Pelayan (*Backend*)**: Node.js, Express, `tsx`, `@google/genai`, Firebase SDK

---

## Struktur Utama Projek

```text
├── public/
│   ├── .well-known/
│   │   └── web-app-origin-association
│   ├── screenshots/              # Tangkapan skrin PWA & widget
│   ├── widgets/                  # Templat & data widget Adaptive Card
│   ├── manifest.json             # Konfigurasi lengkap PWA
│   ├── icon.svg / pwa-*.png      # Ikon aplikasi & maskable
│   └── favicon.ico
├── src/
│   ├── components/               # Komponen UI & modul dokumen
│   ├── data/                     # Data rujukan undang-undang, PTKPN & agensi
│   ├── hooks/
│   │   └── usePWAInstall.ts      # Hook pemasangan PWA & status luar talian
│   ├── services/
│   │   ├── docxService.ts        # Pembina dokumen Microsoft Word (.docx)
│   │   ├── pwaService.ts         # Service Worker, Background/Periodic Sync & Notifikasi
│   │   └── storageService.ts     # Simpanan tempatan & import/eksport JSON
│   ├── sw.ts                     # Service Worker tersuai (cache, sync, push, widget)
│   ├── App.tsx                   # Penghalaan modul & pengendalian parameter pelancaran PWA
│   └── main.tsx
├── server.ts                     # Pelayan Express + middleware Vite & API pelayan
├── vite.config.ts                # Konfigurasi Vite & VitePWA
├── metadata.json                 # Metadata aplikasi
└── package.json
```

---

## Pemasangan & Cara Menjalankan

### 1. Pasang Kebergantungan
```bash
npm install
```

### 2. Konfigurasi Pemboleh Ubah Persekitaran
Salin `.env.example` kepada `.env` dan tetapkan nilai yang diperlukan:
```env
GEMINI_API_KEY="MASUKKAN_KUNCI_API_GEMINI_ANDA"
APP_URL="http://localhost:3000"
```

### 3. Jalankan Mod Pembangunan
```bash
npm run dev
```
Pelayan berjalan di `http://localhost:3000`.

### 4. Binaan & Pengeluaran
```bash
npm run lint    # Semakan jenis TypeScript (tsc --noEmit)
npm run build   # Bina aset statik pengeluaran ke direktori dist/
npm start       # Jalankan pelayan Express dalam mod aplikasi penuh
```

---

## Laluan API Pelayan (`server.ts`)

| Laluan | Kaedah | Fungsi |
| :--- | :--- | :--- |
| `/api/generate-report` | `POST` | Menyusun input/nota rondaan kepada Format Laporan Ringkas Eksekutif menggunakan Gemini API. |
| `/api/export-docx` | `POST` | Menyimpan penimbal fail `.docx` sementara dan memulangkan pautan muat turun universal. |
| `/api/export-docx/:token/:filename?` | `GET` | Memuat turun fail `.docx` menggunakan token sementara (serasi Android WebView/DownloadManager). |
| `/api/export-docx-direct` | `POST` | Muat turun terus fail `.docx` daripada kandungan Base64. |
| `/api/pwa/sync` | `POST` | Titik akhir penyegerakan latar belakang Service Worker. |
| `/.well-known/web-app-origin-association` | `GET` | Pengesahan kaitan domain PWA (`application/json`). |
