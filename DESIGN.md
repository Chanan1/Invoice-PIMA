# INVOICE_DESIGN.md
## Website Invoice — PT PIMA KIMAGRO SEJAHTERA
> Design reference document untuk development website generator invoice berbasis desain brand PT PIMA KIMAGRO SEJAHTERA.

---

## 1. Overview Produk

**Nama Aplikasi:** PIMA Invoice Generator  
**Tipe:** Web App (Single Page Application)  
**Fungsi utama:** Membuat, preview, dan cetak/export invoice dalam format PDF dengan tampilan profesional sesuai brand perusahaan.  
**Target user:** Staff admin / keuangan PT PIMA KIMAGRO SEJAHTERA  
**Bahasa UI:** Bahasa Indonesia  
**Mode:** Light Mode Only

---

## 2. Design Token

### 2.1 Color Palette

| Token | Nama | Hex | Penggunaan |
|---|---|---|---|
| `--color-primary` | Navy Dark | `#0D2B55` | Header tabel, background section judul, teks utama |
| `--color-primary-light` | Navy Medium | `#1A3F7A` | Hover states, border aktif |
| `--color-accent` | Green Leaf | `#2D7A3A` | Label "DISTRIBUTOR", icon, highlight |
| `--color-accent-light` | Green Soft | `#4CAF60` | Badge status, indicator |
| `--color-bg` | White | `#FFFFFF` | Background halaman & invoice |
| `--color-bg-muted` | Gray Light | `#F4F6F9` | Background field input, row alternating |
| `--color-bg-section` | Gray Pale | `#EEF1F5` | Background section "Terbilang", info box |
| `--color-border` | Gray Line | `#D0D7E2` | Border tabel, divider |
| `--color-text-primary` | Dark | `#1A1A2E` | Teks konten utama |
| `--color-text-secondary` | Gray | `#5A6475` | Label, catatan kaki |
| `--color-total-bg` | Navy Total | `#0D2B55` | Background baris TOTAL |
| `--color-total-text` | White | `#FFFFFF` | Teks di baris TOTAL |
| `--color-invoice-badge` | Green Dark | `#1E5C28` | Background badge nomor invoice |

### 2.2 Typography

| Token | Font | Weight | Size | Penggunaan |
|---|---|---|---|---|
| `--font-display` | **Plus Jakarta Sans** | 700–800 | 28–36px | Nama perusahaan, judul "INVOICE" |
| `--font-body` | **Plus Jakarta Sans** | 400–500 | 13–15px | Konten invoice, label, tabel |
| `--font-mono` | **JetBrains Mono** | 400 | 12–13px | Nomor invoice, nomor rekening, kode |

**Type Scale:**
```
display-xl : 36px / 800 / -0.5px → "INVOICE"
display-lg : 22px / 700 / -0.3px → Nama perusahaan
heading-md : 14px / 700 / 0.8px uppercase → Header tabel, label section
body-md    : 14px / 400 / normal → Isi konten
body-sm    : 12px / 400 / normal → Catatan, label kecil
mono       : 12px / 400 / 1.2px → Kode, nomor rekening
```

### 2.3 Spacing & Radius

```
spacing-xs  : 4px
spacing-sm  : 8px
spacing-md  : 16px
spacing-lg  : 24px
spacing-xl  : 32px
spacing-2xl : 48px

radius-sm   : 4px   → Badge, tag
radius-md   : 8px   → Card, input, info box
radius-lg   : 12px  → Modal, section card
```

### 2.4 Shadow

```
shadow-card    : 0 2px 8px rgba(13,43,85,0.08)
shadow-invoice : 0 4px 24px rgba(13,43,85,0.12)
shadow-button  : 0 2px 6px rgba(13,43,85,0.18)
```

---

## 3. Layout Invoice (Print Area)

Invoice menggunakan layout A4 portrait (794px × 1123px) saat preview, dan mengikuti print stylesheet saat dicetak/export PDF.

```
┌─────────────────────────────────────────────────────┐
│  [LOGO + NAMA PERUSAHAAN]         [INVOICE / badge] │  ← Header Band (navy top border 4px)
│  Tagline distributor                                 │
├─────────────────────────────────────────────────────│
│  📍 Alamat   📞 Telp   ✉ Email   🌐 Website         │  ← Info Kontak
│               │         Tgl Invoice: __              │
│               │         Tgl Jatuh Tempo: __          │
│               │         Metode Pembayaran: __        │
│               │         Mata Uang: IDR               │
├──────────────────────┬──────────────────────────────┤
│  DITAGIHKAN KEPADA   │  ALAMAT PENGIRIMAN   │ INFO  │  ← 3-column info
│  Nama PT             │  Nama PT             │ LAIN  │
│  Alamat              │  Alamat              │       │
│  Email / Telp        │  Telp                │       │
├──────────────────────┴──────────────────────────────┤
│  NO │ DESKRIPSI PRODUK │ SATUAN │ QTY │ HRGA │TOTAL │  ← Tabel Header (navy bg)
│   1 │ Pupuk NPK 16-16  │  SAK   │  50 │  280K│  14M │
│   2 │ Asam Humat 90%   │ KARUNG │  20 │  325K│ 6.5M │
│  ... (rows)                                         │
├──────────────────────────────────┬──────────────────┤
│  Terbilang :                     │  SUBTOTAL    39M │
│  [teks terbilang dalam box]      │  PPN 11%    4.3M │
│                                  │  TOTAL      43M  │  ← navy bg, white text
├──────────────────────────────────┴──────────────────┤
│  INFORMASI PEMBAYARAN            │  Hormat kami,    │
│  Bank, No Rek, Atas Nama         │  [Tanda tangan]  │
│  CATATAN                         │  Nama PT         │
└─────────────────────────────────────────────────────┘
```

---

## 4. Komponen UI

### 4.1 Header Invoice

- Logo di kiri (upload-able, default placeholder)  
- Nama perusahaan: `display-lg`, warna `--color-primary`  
- Tagline: `body-sm`, warna `--color-accent`, uppercase  
- Kanan: teks "INVOICE" besar (`display-xl`, bold, navy), di bawahnya badge nomor invoice (green dark background, white text, font-mono)

### 4.2 Info Bar (Kontak)

- 4 ikon inline: lokasi, telepon, email, website  
- Kanan: grid 2-kolom berisi metadata invoice (Tanggal, Jatuh Tempo, Metode Pembayaran, Mata Uang)  
- Border bawah tipis `--color-border`

### 4.3 Section "Ditagihkan / Pengiriman / Info Lain"

- 3-kolom grid  
- Kolom 1 & 2: label header box navy (`heading-md`, putih), isi nama & alamat  
- Kolom 3: box dengan border, label field + value (No. PO, Sales, Pengiriman, Syarat)

### 4.4 Tabel Produk

- Header: `--color-primary` background, white text, uppercase `heading-md`  
- Row body: border bawah tipis, alternating background `--color-bg` / `--color-bg-muted`  
- Kolom: NO (center, 5%), DESKRIPSI PRODUK (left, 40%), SATUAN (center, 12%), QTY (center, 8%), HARGA SATUAN (right, 17%), TOTAL (right, 18%)  
- Deskripsi produk: bold nama produk + `body-sm` grey untuk keterangan (misal ukuran kemasan)
- Dynamic: bisa tambah / hapus baris

### 4.5 Section Terbilang & Summary

- Kiri: label "Terbilang:" + box abu-abu dengan teks terbilang (auto-generate dari angka total)  
- Kanan: tabel ringkasan (SUBTOTAL, PPN %, TOTAL)  
- Baris TOTAL: background `--color-primary`, teks putih, bold

### 4.6 Footer Invoice

- Kiri: box "INFORMASI PEMBAYARAN" (ikon bank, nama bank, no rekening, atas nama) + CATATAN (bullet list)  
- Kanan: tanda tangan area + nama perusahaan  
- Garis dekorasi navy + green di bagian paling bawah (mirror dari header)

---

## 5. Halaman Aplikasi (Web App)

### 5.1 Halaman Form Input (`/`)

**Layout:** Sidebar kiri (navigasi/aksi) + area utama (preview invoice)

```
┌──────────────┬─────────────────────────────────────┐
│  SIDEBAR     │  PREVIEW INVOICE (A4 scale)          │
│              │                                      │
│  Logo upload │  [Invoice rendered real-time]        │
│  Info PT     │                                      │
│  Info Client │                                      │
│  Produk      │                                      │
│  [+ Tambah]  │                                      │
│              │                                      │
│  [Preview]   │                                      │
│  [Export PDF]│                                      │
│  [Reset]     │                                      │
└──────────────┴─────────────────────────────────────┘
```

**Form fields (kiri):**

**Informasi Perusahaan** (bisa disimpan sebagai default):
- Nama Perusahaan
- Tagline
- Upload Logo
- Alamat, Telepon, Email, Website
- Info Bank (Nama Bank, No. Rekening, Atas Nama)

**Detail Invoice:**
- Nomor Invoice (auto-generate: `INV-YYMMDD-XXX`, bisa manual)
- Tanggal Invoice (date picker)
- Tanggal Jatuh Tempo (date picker / pilih durasi: 7/14/30 hari)
- Metode Pembayaran (dropdown)
- Mata Uang (default: IDR)
- No. PO
- Sales / Marketing
- Pengiriman

**Info Klien:**
- Nama Perusahaan Klien
- Alamat Penagihan
- Alamat Pengiriman (checkbox: sama dengan penagihan)
- Email, Telepon

**Produk (dinamis):**
- Tombol `+ Tambah Produk`
- Per baris: Deskripsi, Keterangan, Satuan, Qty, Harga Satuan → Total otomatis
- Tombol hapus per baris
- Drag-to-reorder

**Pajak:**
- Toggle PPN (default: 11%)
- Field persentase bisa diubah

**Catatan:**
- Textarea untuk catatan kustom

### 5.2 Halaman Daftar Invoice (`/invoices`)

- Tabel daftar invoice tersimpan
- Kolom: No Invoice, Klien, Tanggal, Jatuh Tempo, Total, Status (Lunas/Belum/Jatuh Tempo)
- Badge status berwarna
- Aksi: Preview, Download PDF, Duplikat, Hapus

### 5.3 Halaman Settings (`/settings`)

- Simpan profil perusahaan default
- Konfigurasi pajak default
- Konfigurasi nomor invoice (prefix, urutan)
- Upload logo default

---

## 6. Interaksi & State

| Aksi | Behavior |
|---|---|
| Input angka produk | Total per baris & grand total update real-time |
| Tambah baris produk | Row baru muncul dengan animasi slide-down |
| Toggle PPN | Subtotal, PPN, Total recalculate langsung |
| Tanggal + durasi | Jatuh tempo otomatis terisi |
| Preview PDF | Modal full-screen atau tab baru dengan invoice rendered |
| Export PDF | Generate PDF via `window.print()` dengan print-stylesheet khusus A4 |
| Simpan | Tersimpan ke localStorage / database |

---

## 7. Print / PDF Stylesheet

```css
@media print {
  /* Sembunyikan UI chrome */
  .sidebar, .toolbar, .no-print { display: none !important; }

  /* A4 sizing */
  @page {
    size: A4 portrait;
    margin: 12mm 14mm;
  }

  .invoice-container {
    width: 100%;
    box-shadow: none;
    border-radius: 0;
    font-size: 11px;
  }

  /* Jaga warna background saat print */
  .table-header, .total-row {
    -webkit-print-color-adjust: exact;
    print-color-adjust: exact;
  }
}
```

---

## 8. Tech Stack Rekomendasi

| Layer | Pilihan |
|---|---|
| Framework | Next.js 15 (App Router) |
| Styling | Tailwind CSS v4 |
| PDF Export | `react-to-print` atau `html2pdf.js` |
| State | React useState + useReducer |
| Penyimpanan | Supabase (jika multi-user) / localStorage (single-user) |
| Terbilang IDR | Library `terbilang` npm atau custom function |
| Font | Google Fonts: Plus Jakarta Sans, JetBrains Mono |

---

## 9. Signature Element

> **Elemen khas desain ini:** Garis dekorasi diagonal navy + green di sudut kanan atas header dan kiri bawah footer (mirrored), memberi kesan dokumen resmi korporat tanpa terasa kaku. Ini adalah satu-satunya dekorasi non-fungsional yang dipertahankan — semua elemen lain bersifat informatif.

---

## 10. Aksesibilitas & Responsif

- Preview invoice tidak responsif (fixed A4 ratio) — tapi form input di sidebar wajib responsif
- Di layar kecil (mobile): form full-width, preview dapat di-toggle
- Semua input punya label yang visible
- Fokus keyboard visible (outline `--color-primary`)
- Contrast ratio teks minimum 4.5:1

---

*Dokumen ini dibuat sebagai panduan desain dan struktur untuk development website invoice PT PIMA KIMAGRO SEJAHTERA. Update sesuai kebutuhan bisnis.*
