# 🚀 Deploy Izusu ai ke Netlify (Website Beneran Jalan, Bukan Cuma Tampilan)

## Kenapa Sebelumnya Cuma Tampilan Doang?

Chat AI butuh **backend proxy** supaya nggak kena blok sama browser (CORS). Sekarang sudah ada backend di `/api/chat` yang jalan di server.

Netlify bakal otomatis jalanin backend ini pakai **Netlify Functions**.

---

## ⚠️ Penting: Harus Pakai GitHub (Bisa dari Web, Nggak Perlu Terminal)

Karena website ini punya backend (API route), **Netlify Drop (drag & drop folder) nggak bisa**. Harus deploy dari **GitHub repository**.

Tapi tenang, bisa semua lewat web browser. **Nggak perlu ketik command terminal** kalau nggak mau.

---

## 📋 Langkah 1: Upload Kode ke GitHub (Lewat Web Browser)

### Opsi A: Pakai GitHub Web (Drag & Drop Folder)

1. Buka https://github.com/new
2. Kasih nama repository: `isuzu-ai`
3. Pilih **Public**
4. Klik **Create repository**
5. Nanti muncul halaman "Quick setup"
6. Klik yang **"uploading an existing file"**
7. Klik **"choose your files"** atau **drag & drop semua file/folder** dari folder `isuzu-ai` (KECUALI `node_modules` dan `.next`)
8. Tunggu upload selesai → scroll bawah → klik **Commit changes**

> Catatan: Kalau upload file satu per satu ribet, pakai Opsi B (GitHub Desktop) lebih gampang.

### Opsi B: Pakai GitHub Desktop (Aplikasi GUI, Nggak Perlu Terminal)

1. Download https://desktop.github.com/ → install
2. Buka GitHub Desktop → sign in akun GitHub
3. Klik **File → Add local repository** → pilih folder `isuzu-ai`
4. Klik **"create a repository"** → kasih nama `isuzu-ai` → **Create repository**
5. Klik **Publish repository** (pilih Public) → **Publish**

---

## 📋 Langkah 2: Connect ke Netlify (Lewat Web Dashboard)

1. Buka https://app.netlify.com/ → sign up/login (bisa pakai akun GitHub langsung)
2. Klik **"Add new site"** → **"Import an existing project"**
3. Pilih **GitHub**
4. Authorize Netlify (klik ijo)
5. Cari repository `isuzu-ai` → klik **Import**
6. **Build settings:** Netlify biasanya auto-detect Next.js. Pastikan:
   - Build command: `npm run build`
   - Publish directory: `.next` atau biarkan auto-detect
7. Klik **Deploy site**

---

## 📋 Langkah 3: Tunggu & Buka di HP

- Netlify bakal build ~2-3 menit (bisa ditonton progress di dashboard)
- Setelah jadi, klik link yang dikasih (misal: `https://isuzu-ai-xxx.netlify.app`)
- **Copy link → kirim ke WhatsApp diri sendiri → buka di HP**
- Coba chat: ketik "halo" → harusnya AI bales beneran (bukan error)

---

## ⚠️ Kalau Build Error di Netlify

Biasanya karena Node.js version. Perbaiki lewat Netlify dashboard:

1. Buka site → **Site configuration** → **Build & deploy** → **Environment variables**
2. Klik **Add variable**:
   - Key: `NODE_VERSION`
   - Value: `18.20.0`
3. Klik **Deploys** → **Trigger deploy** → **Clear cache and deploy site**

Atau kalau ada error tentang Next.js Runtime, di file `netlify.toml` sudah saya set plugin Next.js. Netlify seharusnya auto-detect.

---

## 🔧 Kenapa Nggak Bisa Drag & Drop Langsung?

Website ini ada **backend** (file `app/api/chat/route.ts`) yang jalan di server. Kalau drag & drop folder build (static), backend nggak ikut jalan. Makanya harus deploy dari GitHub supaya Netlify bisa build ulang dan jalankan backend-nya.

---

## 📱 Test dari HP

Buka link Netlify di Chrome/Safari HP. Chat harusnya bisa bales beneran sekarang karena request lewat server Netlify dulu, baru ke API AI. Nggak kena blok CORS lagi.
