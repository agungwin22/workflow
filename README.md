# Website Template Workflow — Prompt Cheat Sheet

Pipeline 6 stasiun untuk membuat website template statis siap jual di marketplace.
Gunakan secara berurutan. Output setiap stasiun menjadi input stasiun berikutnya.

---

## 🟦 Stasiun 1 — Planning
**Model:** Claude  
**Tujuan:** Membuat spec ringkas sebelum coding dimulai.

```
Kamu adalah senior frontend developer.

Aku akan membuat website template statis untuk dijual di marketplace.

Detail:
- Nama: [nama template]
- Jenis: [misal: landing page SaaS / portfolio / agency]
- Target pembeli: [misal: freelancer, pemilik bisnis kecil]
- Gaya visual: [misal: modern minimalist, dark elegant]
- Warna utama: [hex code]
- Font: [misal: Inter / Poppins]

Buat spec ringkas berisi: daftar section (beserta urutan dari atas ke bawah), color palette lengkap, dan catatan penting untuk coding. Format output-nya harus siap pakai sebagai prompt di langkah berikutnya.
```

---

## 🟩 Stasiun 2 — Code Generation
**Model:** Qwen3-Coder / DeepSeek  
**Tujuan:** Generate satu file HTML lengkap berdasarkan spec dari Stasiun 1.

```
Kamu adalah senior frontend developer.

Buat satu file HTML lengkap berdasarkan spec ini:
[TEMPELKAN OUTPUT STASIUN 1]

Aturan:
- CSS dan JS internal (tidak ada file terpisah)
- Mobile-first, gunakan Flexbox/Grid
- Gunakan CSS custom properties untuk semua warna dan spacing
- Konten dummy realistis, bukan Lorem Ipsum
- Tambahkan komentar singkat di setiap section

Output: satu blok kode dari <!DOCTYPE html> sampai </html>.
```

---

## 🟨 Stasiun 3 — Browser Preview
**Model:** Tidak ada — kamu sendiri yang melakukan ini.  
**Tujuan:** Melihat tampilan nyata sebelum di-review AI.

Langkah-langkahnya adalah sebagai berikut. Buka file `.html` di browser Chrome atau Firefox, lalu tekan `F12` untuk membuka DevTools dan `Ctrl+Shift+M` untuk masuk ke mode device simulation. Ambil screenshot di tiga ukuran: **375px** (mobile), **768px** (tablet), dan **1440px** (desktop). Catat secara manual masalah visual yang kamu lihat sendiri — ini akan sangat membantu di Stasiun 4.

---

## 🟧 Stasiun 4 — Review
**Model:** Claude  
**Tujuan:** Review visual dan kualitas kode secara terpisah.  
**Cara:** Upload file HTML + semua screenshot ke Claude, lalu kirim prompt berikut.

```
Review website template ini dalam dua bagian.

VISUAL (lihat screenshot): hierarki teks, keterbacaan CTA, spacing, dan masalah di mobile.

KODE (lihat file HTML): konsistensi CSS custom properties, struktur HTML semantik, potensi bug JS, dan kemudahan kustomisasi.

Tulis output sebagai daftar instruksi perbaikan siap pakai.
```

---

## 🟥 Stasiun 5 — Refinement
**Model:** Qwen3-Coder / DeepSeek  
**Tujuan:** Memperbaiki kode berdasarkan instruksi dari Stasiun 4.

```
Perbaiki file HTML berikut sesuai instruksi di bawah.

KODE:
[TEMPELKAN HTML]

INSTRUKSI PERBAIKAN:
[TEMPELKAN OUTPUT STASIUN 4]

Hanya ubah bagian yang disebutkan. Jangan ubah struktur atau konten lainnya. Output: satu file HTML lengkap.
```

---

## 🟪 Stasiun 6 — Packaging
**Model:** Claude  
**Tujuan:** Membuat file kelengkapan paket ZIP siap jual di marketplace.

```
Buatkan kelengkapan file untuk template ini:
- Nama: [nama template]
- Jenis: [jenis]

Yang perlu dibuat:
1. README.txt — deskripsi, fitur, cara pakai, cara kustomisasi
2. CHANGELOG.txt — versi 1.0.0 dengan tanggal hari ini
3. LICENSE.txt — lisensi komersial yang ramah pembeli (MIT-style)

Tulis setiap file secara terpisah dan langsung siap pakai.
```

---

## Struktur ZIP Final

Setelah semua stasiun selesai, susun paket ZIP dengan struktur berikut:

```
template-nama/
├── index.html            ← versi single file (untuk pemula)
├── index-modular.html    ← versi modular (untuk developer)
├── css/
│   └── style.css
├── js/
│   └── script.js
├── README.txt
├── CHANGELOG.txt
└── LICENSE.txt
```

> **Catatan:** Versi modular dibuat di akhir setelah kode final selesai.
> Kirim kode final ke Claude/DeepSeek dengan instruksi:
> *"Pisahkan file HTML ini menjadi index.html, css/style.css, dan js/script.js. Pastikan semua path sudah benar."*

---

*Dibuat untuk workflow template marketplace — Gumroad, projects.co.id, dll.*
