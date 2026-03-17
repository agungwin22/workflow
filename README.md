# 🚀 AI Website Development Workflow
**Panduan Lengkap: Plan → Generate → Review → Polish**

> Workflow ini dirancang untuk membuat website / template komersial secara efisien menggunakan kombinasi model AI gratis terbaik.

---

## 📌 Ringkasan Workflow

```
1. PLAN          → Claude (claude.ai)
2. GENERATE      → Qwen3-Coder (gratis)
3. PREVIEW       → Browser lokal kamu
4. SCREENSHOT    → Kamu ambil manual
5. VISUAL REVIEW → Gemini 3 Flash (gemini.google.com)
6. REFINE        → Qwen3-Coder atau DeepSeek
7. FINAL POLISH  → Claude (claude.ai)
```

---

## 🔵 TAHAP 1 — PLAN (Claude)

### Tujuan
Mendefinisikan struktur, komponen, dan logic website **sebelum** satu baris kode pun ditulis. Ini adalah tahap paling penting — plan yang buruk = kode yang berantakan.

### Kapan Pakai Claude untuk Plan?
- Membuat website baru dari nol
- Memulai template baru untuk dijual
- Ketika kamu belum tahu harus mulai dari mana

---

### 📋 Template Prompt — PLAN

Salin prompt di bawah ini ke Claude. Ganti bagian dalam `[ ]` sesuai proyekmu.

```
Kamu adalah senior frontend developer dan UI/UX consultant.

Aku akan membuat sebuah [JENIS WEBSITE] untuk [TARGET PENGGUNA/INDUSTRI].

Detail proyek:
- Nama proyek   : [nama template / website]
- Tujuan utama  : [apa fungsi website ini?]
- Stack         : HTML, CSS, JavaScript vanilla (no framework)
- Target pasar  : [contoh: UMKM, startup, portofolio freelancer]
- Gaya visual   : [contoh: modern minimalis, bold colorful, corporate clean]
- Halaman/section yang diinginkan: [list section yang kamu mau]

Catatan teknis PENTING:
- Output kode nanti hanya 1 file: index.html
- CSS ditulis inline di dalam <style> tag
- JavaScript ditulis inline di dalam <script> tag
- Tidak ada file terpisah (tidak ada style.css, tidak ada script.js)

Tugasmu:
1. Buat DAFTAR SECTION lengkap beserta komponen di tiap section
2. Tentukan COLOR PALETTE (max 4 warna) + font pairing yang sesuai
3. Tentukan CSS custom properties (--variable) yang akan digunakan secara global
4. Buat URUTAN GENERATE yang logis (section mana dulu yang dibuat, bagi jadi batch)
5. Identifikasi POTENSI MASALAH teknis yang mungkin muncul dalam single file

Format output:
- Gunakan heading yang jelas
- Sertakan contoh nama class CSS yang akan dipakai (BEM convention)
- Sertakan catatan khusus untuk Qwen3-Coder yang akan generate kodenya

Jangan generate kode dulu. Fokus pada planning.
```

---

### ✅ Yang Harus Kamu Dapat dari Tahap Ini
- [ ] Daftar section + komponen tiap section
- [ ] Color palette + font + daftar CSS custom properties
- [ ] Urutan pengerjaan (dibagi per batch)
- [ ] Catatan teknis untuk Qwen3-Coder

### 💡 Tips Tahap Plan
- Jika website-mu punya lebih dari 6 section, minta Claude bagi jadi **2-3 batch generate**
- Simpan output planning ini — kamu akan paste ke Qwen3-Coder nanti
- Kalau hasilnya kurang spesifik, follow-up dengan: *"Perjelas bagian [X], sertakan contoh konkret"*

---

## 🟢 TAHAP 2 — GENERATE (Qwen3-Coder)

### Tujuan
Mengubah plan dari Claude menjadi kode HTML/CSS/JS yang aktual. Qwen3-Coder dipilih karena kemampuan coding yang sangat kuat dan gratis.

### Kapan Pakai Qwen3-Coder?
- Generate kode dari awal berdasarkan plan
- Generate section per section
- Tambah fitur baru ke kode yang sudah ada

---

### 📋 Template Prompt — GENERATE (Session Pertama)

```
Kamu adalah senior frontend developer spesialis HTML/CSS/JS vanilla.

Berikut adalah PLAN dari proyek website yang akan kita buat:

[PASTE SELURUH OUTPUT PLANNING DARI CLAUDE DI SINI]

---

Sekarang generate kode untuk BATCH PERTAMA:
[Sebutkan section apa saja yang ada di batch pertama, contoh: Navbar + Hero + About]

ATURAN OUTPUT — WAJIB DIIKUTI:
- Semua kode dalam SATU FILE index.html
- CSS ditulis di dalam <style> tag di bagian <head>
- JavaScript ditulis di dalam <script> tag sebelum </body>
- TIDAK BOLEH ada file eksternal (tidak ada style.css, tidak ada script.js)
- TIDAK BOLEH pakai CDN untuk CSS framework (Bootstrap, Tailwind, dll)
- Google Fonts CDN BOLEH dipakai untuk load font

Ketentuan kode:
- HTML semantik (gunakan tag yang tepat: header, nav, main, section, article, footer)
- CSS menggunakan custom properties (--variable) untuk warna dan font sesuai plan
- JavaScript vanilla murni, tidak pakai jQuery atau library apapun
- Responsive: mobile first, breakpoint di 768px dan 1024px
- Komentar kode dalam Bahasa Inggris
- Tidak pakai placeholder "Lorem Ipsum" — tulis dummy content yang relevan

Output: Satu file index.html lengkap yang siap dijalankan di browser.
```

---

### 📋 Template Prompt — GENERATE (Section Tambahan / Lanjutan)

```
Kamu adalah senior frontend developer spesialis HTML/CSS/JS vanilla.

Berikut adalah kode index.html yang sudah ada:

[PASTE KODE index.html TERAKHIR DI SINI]

---

Sekarang TAMBAHKAN section berikut ke dalam file di atas:
[Nama section yang ingin ditambahkan]

Spesifikasi section:
[Deskripsi detail komponen, layout, dan behaviour yang diinginkan]

ATURAN OUTPUT — WAJIB DIIKUTI:
- Tetap satu file index.html — jangan pisahkan ke file lain
- CSS baru ditambahkan di dalam <style> yang sudah ada (jangan buat <style> baru)
- JavaScript baru ditambahkan di dalam <script> yang sudah ada (jangan buat <script> baru)

Ketentuan:
- Gunakan CSS custom properties (--variable) yang sudah ada, jangan definisikan ulang
- Pastikan tidak ada konflik nama class CSS dengan kode yang sudah ada
- Tambahkan HTML section di posisi yang tepat dalam struktur

Output: Satu file index.html lengkap yang sudah include section baru.
```

---

### ✅ Yang Harus Kamu Dapat dari Tahap Ini
- [ ] File HTML yang bisa langsung dibuka di browser
- [ ] Semua section batch pertama selesai
- [ ] Kode responsive dan tidak ada error di console

### 💡 Tips Tahap Generate
- Generate **section per section** atau maksimal 3 section per prompt — jangan minta semua sekaligus
- Selalu paste **seluruh isi index.html** saat minta lanjutan — jangan hanya paste sebagian
- Kalau kode terpotong di tengah, ketik: *"Lanjutkan dari baris terakhir, output hanya bagian yang belum selesai"*
- Kalau model tiba-tiba memisah ke file lain, ingatkan: *"Semua harus dalam satu file index.html, tidak boleh ada file terpisah"*

---

## 🌐 TAHAP 3 — PREVIEW DI BROWSER

### Tujuan
Melihat hasil kode secara visual sebelum di-review.

### Cara Cepat Preview
1. Simpan kode sebagai `index.html`
2. Buka dengan browser (klik kanan → Open with Chrome)
3. Atau pakai Live Server extension di VS Code

### Yang Perlu Dicek Sebelum Screenshot
- [ ] Tidak ada broken layout
- [ ] Font sudah load dengan benar
- [ ] Gambar / icon sudah tampil (kalau ada)
- [ ] Coba resize window untuk cek responsiveness

---

## 📸 TAHAP 4 — SCREENSHOT

### Cara Ambil Screenshot yang Baik untuk Review

**Desktop view:**
- Lebar window: **1440px** (standar template marketplace)
- Ambil full-page screenshot — gunakan browser extension seperti *GoFullPage* atau *FireShot*

**Mobile view:**
- Gunakan Chrome DevTools → Toggle Device Toolbar
- Set ke **iPhone 14 Pro** (390px) atau **Samsung Galaxy S21**
- Screenshot seluruh halaman

### Penamaan File Screenshot
```
review-desktop-v1.png
review-mobile-v1.png
```
Nomor versi membantu kamu tracking progress revisi.

---

## 🟡 TAHAP 5 — VISUAL REVIEW (Gemini 3 Flash)

### Tujuan
Menganalisis tampilan visual dari screenshot — mencari masalah UI/UX, spacing, tipografi, dan konsistensi warna.

### Di Mana?
Buka **gemini.google.com** → Upload screenshot → Paste prompt di bawah

---

### 📋 Template Prompt — VISUAL REVIEW (Desktop)

```
Kamu adalah UI/UX reviewer profesional untuk website template komersial.

Ini adalah screenshot DESKTOP dari website template yang sedang saya kembangkan untuk dijual di marketplace.

Review screenshot ini dengan fokus pada:

1. VISUAL HIERARCHY
   - Apakah mata pengguna terarah ke elemen yang benar?
   - Mana headline/CTA yang seharusnya paling menonjol?

2. SPACING & LAYOUT
   - Ada section yang terlalu padat atau terlalu longgar?
   - Alignment elemen sudah konsisten?

3. TYPOGRAPHY
   - Apakah ukuran font sudah proporsional?
   - Kontras teks vs background cukup?

4. WARNA & KONSISTENSI
   - Apakah color palette digunakan secara konsisten?
   - Ada elemen yang warnanya "lompat" dari keseluruhan desain?

5. KESAN PERTAMA
   - Apakah kesan pertama dalam 5 detik sudah sesuai dengan jenis bisnisnya?
   - Apakah tampilannya terlihat profesional dan layak dijual?

Output yang diinginkan:
- List masalah spesifik dengan LOKASI ELEMEN (contoh: "Section Hero — tombol CTA terlalu kecil")
- Prioritaskan dari masalah PALING KRITIS ke minor
- Sertakan SARAN PERBAIKAN singkat untuk setiap masalah
- Tidak perlu panjang, langsung ke poin
```

---

### 📋 Template Prompt — VISUAL REVIEW (Mobile)

```
Kamu adalah UI/UX reviewer profesional untuk website template komersial.

Ini adalah screenshot MOBILE (390px) dari website template yang sedang saya kembangkan.

Review khusus untuk tampilan mobile:

1. READABILITY
   - Apakah font sudah cukup besar untuk dibaca di layar kecil?
   - Tidak ada teks yang terpotong atau overflow?

2. TOUCH TARGET
   - Tombol/link cukup besar untuk di-tap jari? (minimum 44x44px)
   - Tidak ada elemen yang terlalu berdekatan?

3. LAYOUT ADAPTATION
   - Apakah layout sudah menyesuaikan dengan baik dari desktop?
   - Elemen yang di desktop side-by-side — sudah stack dengan benar?

4. WHITESPACE
   - Margin/padding section sudah proporsional untuk mobile?

Output: List masalah + lokasi + saran perbaikan. Prioritas dari kritis ke minor.
```

---

### ✅ Yang Harus Kamu Dapat dari Tahap Ini
- [ ] List masalah visual yang spesifik (bukan saran generik)
- [ ] Lokasi elemen yang bermasalah
- [ ] Prioritas perbaikan

### 💡 Tips Tahap Visual Review
- Upload **dua screenshot sekaligus** (desktop + mobile) untuk review komprehensif
- Kalau feedback Gemini terlalu generik, follow-up: *"Berikan contoh CSS yang konkret untuk memperbaiki masalah nomor [X]"*
- Simpan output review ini — paste ke Qwen3-Coder di tahap berikutnya

---

## 🔴 TAHAP 6 — REFINE (Qwen3-Coder / DeepSeek)

### Tujuan
Menerapkan semua perbaikan dari Visual Review ke dalam kode.

### Kapan Pakai Qwen3-Coder vs DeepSeek?
| Kondisi | Pilihan |
|---|---|
| Perbaikan banyak & kompleks | Qwen3-Coder |
| Perbaikan ringan, 1-3 item | DeepSeek |
| Qwen3-Coder sedang lambat/error | DeepSeek sebagai fallback |

---

### 📋 Template Prompt — REFINE

```
Kamu adalah senior frontend developer spesialis HTML/CSS/JS vanilla.

Berikut adalah file index.html yang sudah ada:

[PASTE KODE index.html TERAKHIR DI SINI]

---

Berikut adalah hasil VISUAL REVIEW dari UI/UX reviewer:

[PASTE OUTPUT REVIEW DARI GEMINI 3 FLASH DI SINI]

---

Tugasmu:
Perbaiki kode berdasarkan feedback review di atas.

Prioritaskan perbaikan dalam urutan ini:
1. Masalah KRITIS (layout broken, tidak terbaca)
2. Masalah VISUAL (spacing, warna, tipografi)
3. Masalah MINOR (detail kecil)

ATURAN OUTPUT — WAJIB DIIKUTI:
- Tetap output satu file index.html — jangan pisahkan ke file lain
- Semua CSS tetap di dalam <style> yang sudah ada
- Semua JavaScript tetap di dalam <script> yang sudah ada
- Jangan ubah struktur section yang sudah ada kecuali diminta
- Tambahkan komentar singkat /* REVISED: alasan */ di CSS/JS yang diubah

Output: Satu file index.html lengkap yang sudah diperbaiki.
```

---

### ✅ Yang Harus Kamu Dapat dari Tahap Ini
- [ ] Kode dengan semua perbaikan visual sudah diterapkan
- [ ] Tidak ada regresi (hal yang tadinya bagus jadi rusak)
- [ ] Siap untuk Final Polish

---

## ⚫ TAHAP 7 — FINAL POLISH (Claude)

### Tujuan
Review menyeluruh dari sisi **kualitas kode**, **konsistensi**, dan **kesiapan untuk dijual** sebagai template komersial.

### Kapan Pakai Claude untuk Final Polish?
- Setelah semua perbaikan visual selesai
- Sebelum packaging dan upload ke marketplace
- Ketika butuh feedback mendalam tentang kualitas kode

---

### 📋 Template Prompt — FINAL POLISH

```
Kamu adalah senior frontend developer dan code reviewer.

Berikut adalah file index.html FINAL dari website template yang akan saya jual di marketplace.
Semua kode ada dalam satu file — CSS inline di <style>, JavaScript inline di <script>.

[PASTE KODE index.html FINAL DI SINI]

---

Lakukan FINAL POLISH dengan fokus pada:

1. CODE QUALITY
   - Apakah ada CSS rule yang redundan atau tidak digunakan?
   - Apakah penamaan class sudah konsisten dan deskriptif?
   - Apakah ada potensi error JavaScript yang terlewat?
   - Apakah CSS custom properties sudah digunakan secara konsisten (tidak ada nilai hardcode yang seharusnya pakai variable)?

2. PERFORMANCE (single file context)
   - Apakah ada CSS selector yang terlalu berat atau tidak efisien?
   - Apakah JavaScript dijalankan setelah DOM ready?
   - Apakah Google Fonts hanya load font-weight yang benar-benar dipakai?

3. ACCESSIBILITY (A11Y)
   - Semua gambar punya alt text yang deskriptif?
   - Form elements punya label yang proper?
   - Heading hierarchy sudah benar (h1 → h2 → h3)?
   - Warna teks punya kontras yang cukup?

4. CROSS-BROWSER COMPATIBILITY
   - Apakah ada CSS property yang butuh vendor prefix?
   - Apakah ada JavaScript yang tidak didukung browser lama?

5. MARKETPLACE READINESS
   - Apakah ada bagian kode yang mudah dikustomisasi pembeli? (Beri komentar /* CUSTOMIZE: ... */)
   - Apakah color palette dan font sudah terpusat di CSS custom properties sehingga mudah diganti?
   - Apakah kode cukup rapi dan terbaca oleh pembeli yang bukan developer ahli?

Output:
- List temuan per kategori
- Sertakan potongan kode yang sudah diperbaiki untuk setiap temuan
- Output akhir: satu file index.html yang sudah dipolish
- Berikan SKOR KESIAPAN dari 1-10 beserta alasannya
```

---

### ✅ Yang Harus Kamu Dapat dari Tahap Ini
- [ ] Kode yang bersih dan siap dikustomisasi pembeli
- [ ] Tidak ada error atau potensi bug
- [ ] Skor kesiapan + catatan apa yang perlu diperbaiki sebelum upload

---

## 📦 SETELAH FINAL POLISH — Persiapan Upload

Setelah kode selesai, struktur ZIP yang dikirim ke marketplace hanya ini:

```
template-name.zip
├── index.html          ← satu file utama, semua kode ada di sini
├── LICENSE.txt
├── README.txt
├── CHANGELOG.txt
└── Documentation.pdf
```

> Satu file `index.html` sudah cukup — tidak perlu folder `css/`, `js/`, atau `assets/` karena semua sudah inline. Ini justru mempermudah pembeli untuk langsung pakai tanpa setup apapun.

> Untuk membuat Documentation.pdf dan file pendukung lainnya, gunakan Claude dengan konteks lengkap tentang template yang kamu buat.

---

## 📊 Ringkasan Penggunaan Tiap Model

| Tahap | Model | Platform | Alasan |
|---|---|---|---|
| Plan | **Claude** | claude.ai | Reasoning & struktur terbaik |
| Generate | **Qwen3-Coder** | Gratis | Coding kuat, context window besar |
| Visual Review | **Gemini 3 Flash** | gemini.google.com | Multimodal visual terbaik di tier gratis |
| Refine | **Qwen3-Coder / DeepSeek** | Gratis | Efisien untuk iterasi cepat |
| Final Polish | **Claude** | claude.ai | Review mendalam & feedback actionable |

---

## 🔁 Checklist Per Iterasi

Gunakan checklist ini setiap kali kamu selesai satu putaran revisi:

```
ITERASI #___  |  Tanggal: ___________

[ ] Plan selesai dan disimpan
[ ] Generate batch 1 selesai
[ ] Generate batch 2 selesai (jika ada)
[ ] Preview di browser — tidak ada broken layout
[ ] Screenshot desktop (1440px) diambil
[ ] Screenshot mobile (390px) diambil
[ ] Visual Review Gemini selesai — feedback disimpan
[ ] Refine selesai — feedback diterapkan
[ ] Preview ulang setelah refine
[ ] Final Polish Claude selesai
[ ] File packaging siap (LICENSE, README, docs)
```

---

## 💬 Catatan Penting

1. **Selalu simpan index.html** di setiap tahap — rename dengan versi, contoh: `index-v1.html`, `index-v2.html`
2. **Jangan skip tahap Plan** meskipun template-nya terlihat sederhana — planning 15 menit menghemat 2 jam debugging
3. **Satu session = satu konteks** — kalau ganti tab atau refresh, paste ulang konteks proyekmu
4. **Gemini 3 Flash bisa error saat upload gambar besar** — kompres screenshot ke maksimal 1MB sebelum upload
5. **Kalau model memaksa pisah file** — selalu ingatkan dengan kalimat: *"Output harus satu file index.html, CSS di dalam \<style\>, JS di dalam \<script\>"*
6. **Iterasi adalah normal** — rata-rata template komersial butuh 2-3 putaran Visual Review + Refine sebelum siap

---

*Dibuat untuk workflow pengembangan template website komersial — versi Maret 2026*
