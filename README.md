# Web Dummy LLM · Chatbot Kantin (P06 KSI)

Tugas Keamanan Sistem Informasi (PMI 1522) · P06 Risiko AI/LLM dan Prompt Injection · Kasus **LIVE-1** (prompt injection langsung).

- `24781052-kantin-voucher-rentan.html` — keluaran model dipercaya penuh; baris `AKSI` dari model langsung dijalankan.
- `24781052-kantin-voucher-aman.html` — kontrol di luar model: pemisahan peran + minimisasi, allowlist tool (least privilege), validasi keluaran.
- `index.html` — halaman pembuka berisi tautan ke kedua versi.

Semua data sintetis. API key **tidak ada di kode**: diisi lewat kolom di halaman dan disimpan paling jauh di `sessionStorage`.

## Menjalankan
Buka file HTML di browser (atau lewat URL Netlify), isi API key Google AI Studio milik sendiri, pilih model, lalu klik **Jalankan payload ×3 & catat ke log** dan **Ekspor log**.

## Deploy & git
```bash
git init
git add .
git commit -m "feat: web dummy LLM P06 kantin voucher (rentan dan aman)"
git branch -M main
git remote add origin https://github.com/<username>/<nama-repo>.git
git push -u origin main
```
Netlify: login, lalu *Add new site → Import an existing project* (pilih repo ini) atau seret folder ini ke Netlify Drop saat sudah login.
