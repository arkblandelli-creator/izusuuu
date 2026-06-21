# 📱 Cara Jadiin Izusu ai Bisa Dibuka di HP (Gratis)

## 🎯 Goal
Build website → Upload ke internet → Dapet link → Buka di HP

---

## ✅ STEP 1: Build Website (Di Komputer/Laptop)

Buka **Terminal** (CMD/PowerShell/Terminal):

```bash
cd isuzu-ai
npm install
npm run build
```

Tunggu sampai selesai. Nanti muncul folder baru namanya **`dist/`**.

**Isi folder `dist/` inilah website kamu yang siap upload.**

---

## ✅ STEP 2: Upload ke Internet (2 Cara, Pilih Satu)

### 🔥 CARA A: Netlify Drop (Paling Gampang, Tanpa Daftar)

1. Buka browser → **https://app.netlify.com/drop**
2. Klik tombol **"Deploy manually"** atau langsung drag folder
3. **Drag & drop folder `dist/`** ke halaman Netlify
4. Tunggu 30 detik
5. Dapet link contoh: `https://isuzu-ai-abc123.netlify.app`

**Link itu langsung bisa dibuka di HP!** 📲

Kalau mau ganti nama jadi lebih pendek:
- Klik **Site settings** → **Site name** → ganti jadi `isuzu-ai` → URL jadi `https://isuzu-ai.netlify.app`

---

### 🌐 CARA B: Cloudflare Pages (Gratis, Cepat, Tanpa Iklan)

1. Buka **https://dash.cloudflare.com** → daftar pakai email (gratis)
2. Kiri bawah → **Workers & Pages** → **Create application** → **Pages** → **Upload assets**
3. Klik **"Get started"** → pilih **"Direct upload"**
4. Kasih nama project: `isuzu-ai` → klik **Create project**
5. Klik **"Upload your folder"** → pilih folder `dist/` → klik **Deploy**
6. Dapet link: `https://isuzu-ai-xxx.pages.dev`

---

## ✅ STEP 3: Buka di HP

1. Copy link dari Step 2 (contoh: `https://isuzu-ai.netlify.app`)
2. Kirim ke WhatsApp/Telegram diri sendiri, atau ketik langsung di browser HP
3. Buka pakai **Chrome** atau **Safari** di HP
4. **Selesai!** 🎉

---

## ⚠️ Kalau Chat Tidak Respon di HP

Ini biasanya karena API yang dipakai (ChatGPT/Claude/Gemini) **blok** request dari website gratisan.

**Cek console:**
- Di PC: tekan **F12** → tab **Console** → lihat ada tulisan merah `CORS` atau `blocked`
- Di HP Chrome: ketik di address bar `chrome://inspect` → lihat error

**Solusi sementara (testing):**
- Install extension **"CORS Unblock"** di Chrome (cuma works di PC sendiri, bukan untuk pengunjung lain)

**Solusi beneran (untuk semua orang):**
Butuh backend proxy. Kalau butuh, bilang saja nanti saya buatkan versi yang pakai Vercel (lebih anti-CORS).

---

## 📦 Ringkasan Perintah

```bash
cd isuzu-ai
npm install
npm run build
# Buka https://app.netlify.com/drop → drag folder dist/
```

**3 langkah. Jadi.**
