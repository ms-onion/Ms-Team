# Struktur Web Ms Team

Dokumen ini menjelaskan struktur proyek website Ms Team di `/root/ms`.

## Ringkasan

Website ini adalah web statis berbasis HTML, CSS, dan JavaScript. File utama berada di folder `public/`, sedangkan `server.js` dipakai sebagai server lokal Node.js untuk menyajikan file statis tersebut.

Nama paket proyek: `ms-team-identity`

## Struktur Folder

```text
/root/ms
├── .gitignore
├── README.md
├── STRUKTUR_WEB.md
├── package.json
├── package-lock.json
├── server.js
├── vercel.json
├── node_modules/
└── public/
    ├── index.html
    ├── styles.css
    ├── script.js
    └── assets/
        ├── MsTeam.png
        ├── Ms1397.png
        ├── Ms3000.png
        ├── MsOnion.png
        ├── MsXDROID.png
        └── tools/
            ├── burpsuite.svg
            ├── ffuf.png
            ├── ffuf.svg
            ├── gobuster.svg
            ├── hashcat.svg
            ├── hydra.svg
            ├── johntheripper.ico
            ├── johntheripper.svg
            ├── metasploit.svg
            ├── nikto.ico
            ├── nikto.svg
            ├── nmap.png
            ├── nmap.svg
            ├── paramspider.svg
            ├── sqlmap.ico
            ├── sqlmap.svg
            ├── subfinder.png
            ├── subfinder.svg
            ├── wireshark.svg
            ├── wpscan.png
            └── wpscan.svg
```

## File Root

### `server.js`

Server lokal berbasis modul bawaan Node.js:

- Menggunakan `http`, `fs`, dan `path`.
- Listen di `0.0.0.0:7634`.
- Menyajikan file dari folder `public/`.
- Route `/` diarahkan ke `public/index.html`.
- Route `/health` mengembalikan JSON status server.
- Memiliki daftar MIME type untuk HTML, CSS, JS, JSON, PNG, JPG, SVG, ICO, dan WebP.
- Memiliki proteksi path traversal lewat normalisasi path dan pengecekan agar file tetap berada di dalam `PUBLIC_DIR`.

### `package.json`

Konfigurasi paket Node.js:

- `npm start` menjalankan `node server.js`.
- `npm run dev` juga menjalankan `node server.js`.
- Dev dependency berisi `postcss` dan `cssnano`.

### `vercel.json`

Konfigurasi deployment Vercel:

- File di `public/**/*` dibuild sebagai static asset.
- Semua route diarahkan ke `/public/$1`.
- Asset di `/assets/` diberi cache panjang.
- `styles.css` dan `script.js` diberi cache 1 hari.

### `.gitignore`

Saat ini mengabaikan:

```text
node_modules/
```

## Folder `public/`

Folder ini adalah inti website. Semua file yang dilihat browser berasal dari sini.

### `public/index.html`

Halaman utama website. Struktur halaman:

- `header.topbar`: navigasi sticky dengan logo dan menu.
- `section.hero`: hero utama berisi headline, deskripsi, callsign, tombol aksi, domain, email, dan visual logo.
- `section#focus`: fokus utama tim, yaitu secure development, penetration testing, dan cyber automation.
- `section#tools`: daftar tools cyber security.
- `section#vision`: visi dan misi tim.
- `section#stack`: operating system dan bahasa pemrograman.
- `section#members`: kartu anggota tim.
- `section#contact`: kontak email.
- `footer`: copyright dan tahun dinamis.

File ini memuat:

- Google Fonts: Chakra Petch dan Orbitron.
- CSS dari `/styles.css`.
- JavaScript dari `/script.js`.
- Gambar dari `/assets/`.

### `public/styles.css`

File styling utama. Bagian penting:

- Variabel warna di `:root`.
- Background gelap dengan aksen merah.
- Efek grid dan scanline.
- Layout responsive untuk desktop, tablet, dan mobile.
- Styling topbar, hero, panel, tool card, member card, contact, dan footer.
- Animasi `spin`, `spin-reverse`, dan `bob`.
- Reveal animation untuk elemen `.reveal`.
- Media query untuk layar `960px`, `768px`, `640px`, dan `420px`.
- Dukungan `prefers-reduced-motion`.

### `public/script.js`

JavaScript kecil untuk interaktivitas:

- Mengisi tahun footer secara otomatis memakai `new Date().getFullYear()`.
- Mengaktifkan reveal animation dengan `IntersectionObserver`.
- Mengganti teks callsign secara berkala:
  - `DEFENSE`
  - `OFFENSE`
  - `RESEARCH`
  - `AUTOMATION`
- Menonaktifkan sebagian animasi pada perangkat kecil atau saat user memilih reduced motion.

## Folder `public/assets/`

Berisi asset gambar utama:

- `MsTeam.png`: logo/emblem utama website.
- `Ms1397.png`: gambar anggota Ms 1397.
- `Ms3000.png`: gambar anggota Ms 3000.
- `MsOnion.png`: gambar anggota Ms Onion.
- `MsXDROID.png`: gambar anggota Ms XDROID.

## Folder `public/assets/tools/`

Berisi icon tools cyber security yang ditampilkan di section `Cyber Security Tools`.

Tools yang ditampilkan di halaman:

- Metasploit
- SQLMap
- Nmap
- Nikto
- WPScan
- Burp Suite
- Hydra
- John the Ripper
- ParamSpider
- Subfinder
- Wireshark
- Gobuster
- FFUF
- Hashcat

Beberapa tools punya lebih dari satu format file, misalnya `.svg`, `.png`, atau `.ico`. Halaman memakai format yang ditentukan langsung di `index.html`.

## Alur Kerja Website

1. User membuka `http://localhost:7634`.
2. `server.js` menerima request `/`.
3. Request `/` diarahkan ke `public/index.html`.
4. Browser memuat `styles.css`, `script.js`, font Google, dan asset gambar.
5. CSS mengatur tampilan visual dan responsive layout.
6. JavaScript mengaktifkan reveal animation, tahun footer otomatis, dan rotasi callsign.

## Cara Menjalankan Lokal

```bash
npm install
npm start
```

Lalu buka:

```text
http://localhost:7634
```

Health check tersedia di:

```text
http://localhost:7634/health
```

## Catatan Pengembangan

- Untuk mengubah konten halaman, edit `public/index.html`.
- Untuk mengubah tampilan, edit `public/styles.css`.
- Untuk mengubah animasi/interaksi kecil, edit `public/script.js`.
- Untuk menambah gambar anggota atau logo tools, simpan file di `public/assets/` atau `public/assets/tools/`, lalu referensikan dari HTML.
- Untuk mengubah port lokal, edit konstanta `PORT` di `server.js`.
