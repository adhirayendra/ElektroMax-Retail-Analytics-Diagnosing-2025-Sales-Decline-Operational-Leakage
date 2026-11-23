# 📊 ElektroMax Retail Analytics: Diagnosing 2025 Sales Decline & Operational Leakage

![Tools](https://img.shields.io/badge/Tools-SQL%20%7C%20Power%20BI-blue)
![Focus](https://img.shields.io/badge/Focus-Retail%20Analytics%20%26%20BI-green)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

## 📌 Project Overview
**ElektroMax** adalah perusahaan ritel elektronik dengan **10 cabang** di **4 region** yang membukukan total omzet kumulatif sebesar **Rp290,73 miliar** dengan *Gross Profit Margin* (GPM) **30,89%** dari **56.728 transaksi** (**73.649 unit**). 

Namun, kinerja penjualan pada **tahun 2025 mengalami kontraksi** dibandingkan tahun sebelumnya. Proyek ini bertujuan mendiagnosis akar masalah penurunan kinerja tersebut menggunakan **SQL** dan membangun *dashboard* pemantauan interaktif 3 halaman menggunakan **Power BI**.

> **Disclaimer:** *Dataset yang digunakan dalam proyek ini merupakan data simulasi yang dibuat untuk keperluan studi kasus dan portofolio analisis data.*

---

## 🎯 Key Business Questions
1. **Branch & Product Disparity:** Cabang dan kategori mana yang mengalami kontraksi *Year-on-Year* (YoY) terdalam di 2025, dan apakah penyebabnya berasal dari penurunan volume unit atau penurunan harga jual (*ASP*)?
2. **Promotion Effectiveness:** Apakah kampanye promosi benar-benar meningkatkan penjualan, atau justru hanya menggerus *gross profit margin*?
3. **Customer Frequency Drop:** Mengapa frekuensi belanja pelanggan turun tajam pada tahun 2025?
4. **Return & Logistics Leakage:** Bagaimana pola tingkat retur (~10%) memengaruhi hilangnya *gross profit* dan beban biaya logistik?
5. **Customer Acquisition:** Bagaimana komposisi pelanggan aktif dibandingkan akuisisi pelanggan baru sepanjang 2024–2025?

---

## 🗂️ Data Architecture & Methodology
Analisis dilakukan pada skema *star-schema* yang terdiri dari:
- **Fact Table:** `fact_penjualan` (transaksi, kuantitas, harga satuan, diskon, *total_neto*, *gross_profit*, *status_transaksi*).
- **Dimension Tables:** `dim_toko`, `dim_produk`, `dim_pelanggan`, `dim_promosi`, dan `dim_waktu`.

**Aturan Analitis Utama:**
- Perhitungan omzet bersih, margin, dan perilaku belanja mengecualikan transaksi berstatus `'Retur'`.
- Evaluasi kampanye promosi dinormalisasi per hari aktif (`total_hari`) agar adil membandingkan periode promo singkat dengan hari normal (*Baseline*).
- Estimasi beban logistik retur dihitung menggunakan asumsi **Rp50.000 per transaksi retur**.

---

## 🔍 Key Analytical Findings

### 1. Disparitas YoY Antar Cabang & Fenomena *Downtrading*
- **6 dari 10 cabang** mengalami penurunan omzet pada 2025 dengan rentang pertumbuhan antara **+4,57%** (*Pondok Indah Mall*) hingga **-12,38%** (*Sun Plaza*).
- Penurunan terdalam terjadi pada dua penopang omzet terbesar 2024: **ElektroMax Sun Plaza (-12,38%)** dan **ElektroMax Mall of Indonesia (-9,05%)**.
- Kontraksi tidak disebabkan oleh sepinya jumlah pembeli, melainkan kombinasi **pergeseran ke produk berharga katalog lebih murah (*downtrading*)**—seperti *ASP* Televisi di Sun Plaza turun **11,6%** (Rp7,20 jt → Rp6,36 jt) dan Kulkas di MOI turun **8,7%** (Rp4,04 jt → Rp3,68 jt)—serta penurunan volume unit pada **AC Sun Plaza (-18,0%)** dan **Mesin Cuci MOI (-17,3%)**.

### 2. Dominasi Penjualan Organik & Inflasi Diskon
- Sebanyak **67,20% omzet (Rp195,36 miliar)** berasal dari transaksi organik **Tanpa Promosi**.
- Dari 17 skema promosi, kontribusi riil hanya terpusat pada **Flash Sale Weekend (16,24%; Rp47,23 M)** dan **Bundling AC + Instalasi (14,62%; Rp42,52 M)**, sedangkan 15 promo musiman lainnya menyumbang **<2%**.
- Kenaikan pemberian diskon efektif di tahun 2025 (dari **~3,5% menjadi ~5,0%**) gagal mendongkrak jumlah transaksi dan justru memperdalam penurunan harga bayar bersih (*net ASP*).

### 3. Stagnasi Akuisisi (0 Pelanggan Baru) & Penurunan Frekuensi *Repeat Buyers*
- Sepanjang 2024–2025, jumlah pelanggan aktif stagnan di **521 pelanggan** dengan **0 akuisisi pelanggan baru**.
- Pelanggan paling loyal memangkas frekuensi belanja hampir **50%** di tahun 2025 (misalnya ID `#40` turun dari 51 menjadi 28 transaksi; selisih omzet `-Rp147,4 juta`).

### 4. Tingkat Retur Sistemik (10,01%) Membebani Logistik Rp284 Juta
- Tercatat **5.681 transaksi retur (10,01%)**, dengan **54,1%** di antaranya berasal dari kategori utama: **AC (1.085)**, **Televisi (1.055)**, dan **Kulkas (936)**, serta lonjakan retur pada **Microwave (834)**.
- Distribusi retur merata di seluruh 10 toko (**527–591 retur/cabang**), menandakan perlunya perbaikan standar *quality control* dan pengiriman di level perusahaan.
- Total retur ini menimbulkan estimasi pemborosan biaya logistik sebesar **Rp284,05 juta** (di luar hilangnya *gross profit*).

---

## 💡 Strategic Recommendations
1. **Pemulihan Cabang & ASP:** Fokuskan strategi *upselling* dan paket *bundling* bernilai tambah pada kategori AC dan TV di **Sun Plaza** serta **Mall of Indonesia** untuk memulihkan *Average Selling Price* (+5%–8%).
2. **Pre-Delivery QC & Pengendalian Retur:** Terapkan inspeksi kualitas wajib sebelum pengiriman untuk unit AC, TV, Kulkas, dan Microwave guna menekan rasio retur dari ~10% menjadi **<6%**.
3. **Program Reaktivasi *Top Buyers*:** Jalankan kampanye *win-back* terpersonalisasi dengan insentif *cashback* QRIS/Transfer Bank bagi pelanggan 2024 yang mengalami penurunan frekuensi tajam.
4. **Rasionalisasi Kalender Promo:** Pangkas promo musiman ber-margin rendah dan alokasikan anggaran ke format **Bundling Produk + Instalasi** yang menjaga GPM tetap stabil di atas **31%**.

---

## 🖥️ Power BI Dashboard Preview
Dashboard interaktif terdiri dari 3 halaman utama:
1. **Overview:** Ringkasan KPI utama, tren omzet & transaksi bulanan vs *Last Year*, kontribusi subkategori, dan peringkat pencapaian toko.
2. **Product & Toko:** Analisis kontribusi region, *Gross Profit Margin %*, serta tabel *drill-down* performa toko dan SKU produk.
3. **Pelanggan:** Pemetaan retensi 521 pelanggan, distribusi segmen & kelompok usia, metode pembayaran, efektivitas promo, dan rasio retur.

*(Tambahkan screenshot dashboard Anda di folder `/assets` dan tampilkan di sini)*

---

## 🔗 Project Links & Contact
- 📊 **Interactive Power BI Dashboard:** [Link Dashboard Power BI]
- 📑 **Presentation Slide Deck (PDF):** [Link Slide Deck]
- 💼 **LinkedIn:** [Link Profil LinkedIn Anda]
- 🌐 **Portfolio Website:** [Link Portfolio Anda]
