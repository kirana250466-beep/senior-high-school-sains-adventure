# Lab Fisika 11 (nama di Cloudflare: lab-fisika-kelas-11)

Website latihan soal Fisika Kelas 11 (Bab 1: Vektor, Kinematika, Dinamika). Login pakai nama: **Ferdi** = Pengajar, nama lain = Siswa.
Situs ini file statis (tanpa build, tanpa Functions, tanpa npm install di server), jadi tidak ada error "Could not resolve ...".

## Isi paket
- `public/index.html` : seluruh website (satu file)
- `public/_headers` : header keamanan sederhana
- `wrangler.jsonc` : konfigurasi Workers (nama `lab-fisika-kelas-11`, folder aset `./public`)
- `package.json` : skrip `dev`, `deploy`, `deploy:pages`

## 1. Upload ke GitHub
Cara mudah: buat repo baru, klik **Add file > Upload files**, seret SEMUA isi folder ini (termasuk folder `public`), lalu **Commit**.
Cara terminal:
```
git init && git add . && git commit -m "Lab Fisika 11"
git branch -M main
git remote add origin https://github.com/USERNAME/NAMA-REPO.git
git push -u origin main
```

## 2A. Cloudflare Workers (disarankan)
Workers & Pages > **Create** > **Import a repository** > pilih repo.
- Project / Worker name: `lab-fisika-kelas-11` (harus sama dengan `name` di wrangler.jsonc)
- Build command: kosongkan
- Deploy command: `npx wrangler deploy`
- Root directory: `/`
Hasilnya: `https://lab-fisika-kelas-11.<subdomain-kamu>.workers.dev`

**Kalau folder ini dimasukkan ke dalam repo lain** (misalnya repo yang sudah ada), isi Deploy command:
`npx wrangler deploy --config lab-fisika-kelas-11/wrangler.jsonc`
(folder `public` otomatis dibaca relatif terhadap file wrangler.jsonc itu).

## 2B. Cloudflare Pages
Workers & Pages > **Create** > **Pages** > **Connect to Git** > pilih repo.
- Framework preset: None
- Build command: kosongkan
- Build output directory: `public`
Atau tanpa Git: `npm install` lalu `npm run deploy:pages`.
Pakai salah satu saja (Workers atau Pages) agar tidak ada dua situs kembar.

## Jika muncul error
- *Missing entry-point / assets directory*: pastikan folder `public/index.html` ikut ter-upload.
- *Worker name mismatch / project tidak ketemu*: samakan nama proyek di Cloudflare dengan `name` di wrangler.jsonc.
- *wrangler.jsonc not found*: file ada di subfolder, pakai `--config <folder>/wrangler.jsonc`.
- Layar 3D kosong: halaman butuh internet untuk memuat three.js dari cdnjs; tanpa itu otomatis tampil gambar 2D.

## Menambah bab
Edit `public/index.html`: tambahkan daftar soal baru lalu daftarkan di `const BAB=[...]`. Commit, Cloudflare otomatis deploy ulang.
