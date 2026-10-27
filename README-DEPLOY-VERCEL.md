# PPPK Rehabilitasi Sosial — Permindokditanak 2026

Folder ini disiapkan untuk deploy frontend loader di Vercel dengan nama proyek/repository `pppkrehsos-permindokditanak2026`.

## Isi folder
- `index.html` — halaman loader hijau toska yang memuat aplikasi Google Apps Script di iframe.
- `Code.gs` — backend Google Apps Script untuk menyimpan data ke Google Sheets/Drive.
- `Index.html` — antarmuka formulir yang dipakai oleh Google Apps Script.
- `vercel.json` — konfigurasi static deployment Vercel.

## Penting: Vercel dan Google Apps Script
Vercel hanya menyajikan `index.html` sebagai halaman awal/loader. File `Code.gs` **tidak dijalankan oleh Vercel**. Formulir tetap berjalan di Google Apps Script dan menyimpan data melalui deployment Apps Script yang URL-nya tertanam pada loader.

URL Apps Script saat ini di `index.html`:
`https://script.google.com/macros/s/AKfycbxDUrAIgNBBgVWuluERf6zaUnAhVc2T3qf4KCbkxxXYdfvTNmb8NSt5VA9vVFDYuzhrMQ/exec`

## Langkah deploy
1. Pastikan proyek Google Apps Script berisi `Code.gs` dan file HTML bernama `Index` (isi dari `Index.html`).
2. Di Apps Script, jalankan `setupApp()` satu kali dan selesaikan otorisasi yang diminta.
3. Deploy > New deployment > Web app. Atur **Execute as** sesuai tata kelola organisasi dan akses sesuai kebijakan data. Setelah memperbarui kode, buat versi deployment baru atau edit deployment yang ada.
4. Uji form secara internal dan pastikan pengiriman masuk ke spreadsheet serta lampiran BNBA masuk ke folder Drive.
5. Unggah seluruh isi folder ini ke repository GitHub bernama `pppkrehsos-permindokditanak2026`.
6. Di Vercel, pilih **Add New > Project**, impor repository tersebut, gunakan Framework Preset **Other**, biarkan Build Command dan Output Directory kosong/default (static HTML), lalu Deploy.
7. Setelah deploy, buka URL Vercel. Loader akan menampilkan aplikasi Apps Script melalui iframe. Jika iframe tidak dapat dimuat oleh kebijakan browser atau deployment, gunakan tautan **Buka aplikasi langsung** pada halaman fallback.

## Catatan keamanan
Data NIP dan data anak adalah data pribadi. Batasi akses deployment Apps Script, spreadsheet, dan folder Drive kepada pihak berwenang. Jangan gunakan akses publik kecuali memang telah disetujui dan sesuai kebijakan pengelolaan data.

## Jika URL Apps Script berubah
Perbarui URL `/exec` di dua tempat pada `index.html`: atribut `src` iframe dan tautan fallback `href`, kemudian commit/push agar Vercel redeploy.
