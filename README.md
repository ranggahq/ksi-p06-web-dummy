# Web Dummy LLM · Chatbot Kantin Koperasi (P06 KSI)

Tugas Keamanan Sistem Informasi (PMI 1522) · P06 Risiko AI/LLM dan Prompt Injection · Kasus **LIVE-1** (Prompt Injection Langsung).

- **Nama**: Rangga Hazirathul Qudsiah
- **NPM**: 24781052
- **Program Studi**: Keamanan Sistem Informasi / Informatika, Politeknik Negeri Lampung

---

## 📁 Struktur Berkas

- `index.html` — Halaman beranda portal perbandingan dan panduan pengujian.
- `24781052-kantin-voucher-rentan.html` — **Versi RENTAN**: Masukan pengguna digabung dengan instruksi sistem, keluaran model dipercaya penuh, dan aksi voucher dieksekusi tanpa otorisasi kode.
- `24781052-kantin-voucher-aman.html` — **Versi AMAN**: Menerapkan arsitektur *Defense-in-Depth* dengan kontrol di luar model (pemisahan peran/kanal, batasan least privilege / allowlist tool ketat, dan validasi keluaran).
- `netlify.toml` — Konfigurasi deploy Netlify.

Semua data menu & voucher bersifat sintetis (dummy). API key **tidak disimpan di kode sumber**: diisi secara dinamis melalui antarmuka web dan hanya disimpan di `sessionStorage` peramban pengguna.

---

## 🛡️ Model LLM yang Didukung & Optimasi Kuota

Untuk menghindari habisnya kuota token API Google AI Studio (HTTP 429 Too Many Requests / Resource Exhausted):
1. **Model Resmi yang Direkomendasikan**:
   - `gemini-1.5-flash` (Hemat token, kuota 15 RPM / 1M TPM)
   - `gemini-1.5-flash-8b` (Sangat ringan & cepat)
   - `gemini-2.0-flash` & `gemini-2.0-flash-lite`
2. **Optimasi Konsumsi Token**:
   - `maxOutputTokens: 250` diatur pada setiap permintaan untuk membatasi panjang respons agar kuota API tetap hemat.
3. **Penanganan Rate Limit**:
   - Fitur eksekusi beruntun (run &times;3) kini dilengkapi jeda otomatis & status hitung mundur agar tidak menabrak batas limit per detik/menit.
4. **Mode Simulasi / Mock Tester (Offline)**:
   - Tersedia opsi centang *Mode Simulasi* pada halaman web untuk menguji sistem secara langsung tanpa perlu memasukkan API Key atau saat kuota Google AI Studio habis.

---

## 🚀 Panduan Pengujian

1. Buka `index.html` di browser atau melalui tautan deploy Netlify.
2. Masuk ke halaman **Versi RENTAN**:
   - Masukkan API Key Google AI Studio Anda (atau centang Mode Simulasi).
   - Klik **"Isi payload serangan"**.
   - Klik **"Jalankan payload &times;3 & catat ke log"**.
   - Sistem akan mendeteksi pelanggaran kebijakan (terbit voucher diskon 100%).
   - Klik **"Ekspor log"** untuk mengunduh `24781052-LIVE-1-rentan-log.json`.
3. Masuk ke halaman **Versi AMAN**:
   - Masukkan API Key Google AI Studio Anda (atau centang Mode Simulasi).
   - Klik **"Isi payload serangan"** (payload yang sama).
   - Klik **"Jalankan payload &times;3 & catat ke log"**.
   - Sistem berhasil menahan serangan: tool voucher ditolak oleh allowlist kode aplikasi dan teks disanitasi.
   - Klik **"Ekspor log"** untuk mengunduh `24781052-LIVE-1-aman-log.json`.

---

## 📦 Deployment & Git

```bash
git add .
git commit -m "fix: optimasi model gemini, penanganan kuota token & mitigasi prompt injection"
git push origin main
```
Deploy ke Netlify dapat dilakukan dengan menghubungkan repositori GitHub ini ke Netlify (*Continuous Deployment*) atau melalui Netlify Drop.
