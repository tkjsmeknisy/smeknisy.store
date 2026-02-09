# PWA Wrapper - Google Apps Script ke PWA

Aplikasi ini adalah wrapper PWA (Progressive Web App) yang mengubah Google Apps Script menjadi aplikasi mobile yang dapat diinstal di smartphone dengan tampilan native dan performa yang dioptimalkan.

## 🚀 Fitur Utama

- ✅ **PWA Installable** - Dapat diinstall di smartphone seperti aplikasi native
- ✅ **Smart Caching** - Loading super cepat setelah akses pertama (1.5 detik vs 3+ detik)
- ✅ **Splash Screen** - Loading screen yang menarik dengan animasi
- ✅ **Offline Ready** - Service Worker untuk caching optimal
- ✅ **Responsive Design** - Tampilan sempurna di semua device
- ✅ **Fast Loading** - Preconnect dan DNS prefetch untuk Google servers

## 📁 Struktur File

```
PWA Wraper/
├── index.html          # File utama aplikasi
├── manifest.json       # Konfigurasi PWA
├── sw.js              # Service Worker untuk caching
├── icons/
│   └── icon.svg       # Logo aplikasi
└── README.md          # Dokumentasi ini
```

## 🛠️ Cara Kustomisasi

### 1. Mengganti URL Google Apps Script

Edit file `index.html` pada baris 208:

```javascript
frame.src = "https://script.google.com/macros/s/SCRIPT_ID_ANDA/exec";
```

**Cara mendapatkan URL:**
1. Buka Google Apps Script project Anda
2. Klik **Deploy** → **New Deployment**
3. Pilih type: **Web app**
4. Execute as: **Me**
5. Who has access: **Anyone**
6. Copy URL yang diberikan

### 2. Mengganti Nama Aplikasi

Edit file `manifest.json`:

```json
{
  "name": "Nama Aplikasi Anda",           // Nama lengkap
  "short_name": "NamaApp",                // Nama pendek (max 12 karakter)
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#ffffff"
}
```

Dan di `index.html` baris 6:

```html
<title>Nama Aplikasi Anda</title>
```

### 3. Mengganti Logo/Icon

1. **Ganti file** `icons/icon.svg` dengan logo Anda
2. **Format yang didukung:** SVG, PNG, ICO
3. **Ukuran recommended:** 512x512px minimum

**Jika menggunakan PNG/ICO, edit `manifest.json`:**

```json
"icons": [
  {
    "src": "icons/icon.png",
    "sizes": "192x192 512x512",
    "type": "image/png"
  }
]
```

### 4. Kustomisasi Tema Warna

Edit di `index.html` dan `manifest.json`:

```css
/* index.html - ubah warna tema */
background: #ffffff;        /* Background utama */
color: #333333;            /* Warna teks */
border-top: 3px solid #007acc;  /* Warna accent */
```

```json
/* manifest.json */
"background_color": "#ffffff",  /* Warna background */
"theme_color": "#007acc"       /* Warna theme bar */
```

### 5. Kustomisasi Pesan Loading

Edit array `firstLoadMessages` dan `cachedLoadMessages` di `index.html` baris 119-135:

```javascript
const firstLoadMessages = [
  "Loading aplikasi...",
  "Tunggu sebentar...", 
  "Hampir siap...",
  // tambah pesan lain
];

const cachedLoadMessages = [
  "Loading dari cache...",
  "Hampir siap...",
  // pesan untuk loading yang sudah cached
];
```

## 🌐 Cara Deploy

### Option 1: GitHub Pages (Gratis)

1. **Push ke GitHub:**
   ```bash
   git add .
   git commit -m "Setup PWA wrapper"
   git push origin main
   ```

2. **Enable GitHub Pages:**
   - Buka repository di GitHub
   - Settings → Pages
   - Source: Deploy from branch → main
   - Folder: / (root)
   - Save

3. **Akses aplikasi:**
   `https://username.github.io/repository-name`

### Option 2: Netlify (Gratis)

1. Buka [netlify.com](https://netlify.com)
2. Drag & drop folder project ke Netlify
3. Aplikasi otomatis deploy dan dapat URL

### Option 3: Vercel (Gratis)

1. Install Vercel CLI: `npm i -g vercel`
2. Jalankan: `vercel` di folder project
3. Follow setup instructions

### Option 4: Web Server Sendiri

Upload semua file ke web hosting dengan support HTTPS (required untuk PWA).

## 📱 Cara Install di Smartphone

### Android:
1. Buka aplikasi di Chrome
2. Klik menu ⋮ → **Add to Home screen**
3. Confirm install

### iPhone:
1. Buka di Safari
2. Klik Share button 📤
3. **Add to Home Screen**

### Desktop:
1. Buka di Chrome/Edge
2. Lihat icon ⊕ di address bar
3. Klik **Install**

## ⚡ Optimasi Performa

Aplikasi sudah dioptimalkan dengan:

### Smart Caching Strategy:
- **First load:** ~3 detik dengan download semua resource
- **Subsequent loads:** ~1.5 detik dengan cache
- **Apps Script:** Network-first dengan cache fallback
- **Static resources:** Cache-first untuk speed maksimal

### Network Optimizations:
- Preconnect ke Google servers
- DNS prefetch untuk faster resolution
- Eager iframe loading

## 🔧 Troubleshooting

### Aplikasi tidak load:
1. Pastikan URL Google Apps Script benar
2. Cek Apps Script deployment settings
3. Pastikan "Who has access" set ke "Anyone"

### PWA tidak bisa diinstall:
1. Pastikan menggunakan HTTPS
2. Cek `manifest.json` syntax
3. Pastikan icon file ada dan accessible

### Loading lambat:
1. Cek koneksi internet
2. Clear browser cache
3. Tunggu beberapa akses untuk cache terbentuk

### Cache tidak bekerja:
1. Pastikan Service Worker registered
2. Cek di Developer Tools → Application → Service Workers
3. Hard refresh (Ctrl+Shift+R) untuk reset cache

## 📝 Lisensi

Free to use, modify, and distribute. No warranty provided.

## 🤝 Kontribusi

Feel free to fork, modify, dan submit pull requests untuk improvements!

---

**Dibuat dengan ❤️ untuk mengubah Google Apps Script menjadi PWA yang keren!**