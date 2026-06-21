# 🚀 Deploy Izusu ai ke Netlify (Gratis)

Ini adalah panduan lengkap agar Izusu ai bisa diakses dari HP dan semua orang di internet.

---

## 📋 Pilih Cara Deploy (3 Pilihan)

### **CARA 1: Netlify Drop (Paling Gampang, Cuma Drag & Drop)**

Cocok kalau kamu mau cepat tanpa repot command line.

#### Step 1: Build project di lokal
```bash
cd isuzu-ai
npm install
npm run build
```

> Hasil build akan ada di folder `dist/` (bukan `.next/` karena sudah di-set static export).

#### Step 2: Buka Netlify Drop
1. Buka browser → https://app.netlify.com/drop
2. Kamu akan lihat halaman dengan area drag & drop besar
3. **Drag folder `dist/`** dari file manager kamu ke browser
4. Netlify akan otomatis upload dan deploy
5. Tunggu ~30 detik, lalu klik link yang muncul (misal: `https://isuzu-ai-abc123.netlify.app`)

✅ **Selesai!** Website sudah live dan bisa dibuka dari HP mana saja.

---

### **CARA 2: Netlify CLI (Lewat Terminal)**

Cocok kalau kamu sudah nyaman pakai command line.

#### Step 1: Install Netlify CLI
```bash
npm install -g netlify-cli
```

#### Step 2: Login ke Netlify
```bash
netlify login
```
> Buka browser yang muncul dan authorize.

#### Step 3: Build & Deploy
```bash
cd isuzu-ai
npm install
npm run build
netlify deploy --prod --dir=dist
```

> Hasil: `https://isuzu-ai-xxx.netlify.app`

Kalau mau ganti nama domain, buka dashboard Netlify → Site Settings → Change site name.

---

### **CARA 3: GitHub + Netlify (Auto Deploy, Paling Profesional)**

Cocok untuk development jangka panjang. Setiap kali push ke GitHub, website otomatis update.

#### Step 1: Push ke GitHub
1. Buat repository baru di https://github.com/new (misal: `isuzu-ai`)
2. Di terminal:
```bash
cd isuzu-ai
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/USERNAME/isuzu-ai.git
git push -u origin main
```
> Ganti `USERNAME` dengan username GitHub kamu.

#### Step 2: Connect ke Netlify
1. Buka https://app.netlify.com/
2. Klik **"Add new site"** → **"Import an existing project"**
3. Pilih **GitHub** → Authorize Netlify → Pilih repository `isuzu-ai`
4. **Build settings:**
   - Build command: `npm run build`
   - Publish directory: `dist`
5. Klik **"Deploy site"**

⏱️ Tunggu ~2 menit. Netlify otomatis build dan deploy.

#### Keuntungan Cara 3:
- Setiap kali kamu push kode baru → otomatis deploy ulang
- Bisa pakai branch preview (pull request = preview URL)
- Bisa ganti custom domain gratis (`.netlify.app` bisa diubah)

---

## 🌍 Ganti Domain Jadi Lebih Pendek

Netlify kasih domain random. Mau ganti?

1. Buka https://app.netlify.com → pilih site kamu
2. Go to **Site configuration** → **Site name**
3. Ganti jadi `isuzu-ai` → URL jadi `https://isuzu-ai.netlify.app`

Atau beli domain custom (misal: `isuzuai.com`) dan connect di **Domain management**.

---

## ⚠️ Catatan Penting: CORS (Cross-Origin)

Izusu ai fetch langsung ke API eksternal dari browser:
- `https://api-nanzz.my.id/...` (ChatGPT)
- `https://api.xvortex.my.id/...` (Claude, Gemini)

**Masalah:** Kalau server API tidak mengizinkan request dari domain Netlify kamu, akan muncul error CORS di console dan chat tidak bisa jalan.

### Solusi jika CORS error:

**Opsi A: Pakai browser extension (hanya untuk testing)**
- Install "CORS Unblock" extension di Chrome/Edge
- Hanya works di browser kamu, tidak untuk pengunjung lain

**Opsi B: Tambah Netlify Function sebagai proxy (untuk production)**

Ini cara yang benar untuk production. Buat file `netlify/functions/proxy.ts`:

```typescript
// netlify/functions/proxy.ts
export default async (req: Request) => {
  const url = new URL(req.url);
  const target = url.searchParams.get('url');
  if (!target) return new Response('Missing url', { status: 400 });

  const response = await fetch(target, {
    method: req.method,
    headers: {
      'Content-Type': 'application/json',
    },
    body: req.body,
  });

  return new Response(response.body, {
    status: response.status,
    headers: {
      'Access-Control-Allow-Origin': '*',
    },
  });
};
```

Lalu ubah `app/lib/api.ts` agar fetch lewat proxy Netlify:

```typescript
// Ganti baris fetch langsung jadi:
const proxyUrl = `/.netlify/functions/proxy?url=${encodeURIComponent(url)}`;
const response = await fetch(proxyUrl, ...);
```

Tapi ini menambah kompleksitas. Untuk saat ini, coba deploy dulu dan lihat apakah API eksternal sudah support CORS. Kalau tidak, baru implement proxy.

**Opsi C: Deploy ke Vercel (lebih gampang untuk proxy)**
Kalau CORS jadi masalah besar, deploy ke Vercel lebih mudah karena Next.js API Routes otomatis jadi serverless functions. Tapi Netlify juga support functions.

---

## 📱 Test dari HP

Setelah deploy:
1. Buka Chrome/Safari di HP
2. Masukkan URL Netlify kamu (misal: `https://isuzu-ai.netlify.app`)
3. Pastikan HP dan laptop pakai jaringan internet yang sama (bukan localhost)

---

## 🔧 Troubleshooting

| Masalah | Solusi |
|---------|--------|
| `404` saat refresh page | Sudah di-handle `netlify.toml` (redirects ke index.html) |
| Gambar avatar tidak muncul | Cek URL `https://files.catbox.moe/siay6e.jpg` masih aktif |
| Chat tidak respon | Buka DevTools → Console → cek error CORS |
| Build error | Pastikan `NODE_VERSION` di Netlify ≥ 18 |
| Font tidak loading | Font dari Google CDN, pastikan internet aktif |

---

## 📦 Summary Cara Termudah (Cepat)

```bash
cd isuzu-ai
npm install
npm run build
# Lalu buka https://app.netlify.com/drop → drag folder dist/
```

🎉 **Website Izusu ai sudah live di internet!**
