# 🛡️ Let’s Defend - Phishing Email Analysis

## 📌 1. Pendahuluan
**Tujuan:** Menganalisis email mencurigakan yang mengatasnamakan **PayPal German** untuk menentukan apakah email tersebut merupakan serangan phishing atau korespondensi resmi.

**Metodologi:**
* Investigasi **Return-Path** pada Header Email.
* Analisis struktur **URL & Domain** (TLD Analysis).
* Reputasi pengecekan menggunakan **VirusTotal**.

---

## 🔍 2. Langkah Analisis & Temuan

### A. Investigasi Return-Path
`Return-Path` adalah alamat yang digunakan untuk menerima *bounce message* (pesan gagal kirim). Penyerang sering memalsukan baris "From", namun `Return-Path` sering kali menunjukkan identitas asli server pengirim.

* **Alasan Analisis:** Untuk melihat apakah ada ketidaksesuaian (*mismatch*) antara pengirim yang ditampilkan dengan alamat asli pengirim.
* **Temuan:** Domain pada `Return-Path` berbeda dengan domain resmi PayPal, yang mengindikasikan upaya **Spoofing**.

**Langkah Menampilkan Source Email:**
<br>
<img width="540" alt="Cara Menampilkan Source" src="https://github.com/user-attachments/assets/ba11fb57-ecd8-4fd0-a8ac-65b6631d4375" />
<br>

**Contoh Tampilan Header:**
<br>
<img width="524" alt="Tampilan Header" src="https://github.com/user-attachments/assets/435b890d-901b-489a-8430-0ba38c75f5cb" />
<br>

---

### B. Analisis Domain & TLD
Struktur URL yang dianalisis mengikuti format: `scheme://subdomain.domain.tld/path`.

#### Klasifikasi Top-Level Domain (TLD)
TLD membantu mengidentifikasi kategori atau asal geografis sebuah website:

| TLD | Contoh | Keterangan |
| :--- | :--- | :--- |
| **gTLD** | `.com`, `.org`, `.net` | **Generic**: Tidak terikat wilayah negara tertentu. |
| **ccTLD** | `.id`, `.us`, `.jp` | **Country Code**: Terikat pada identitas negara tertentu. |
| **sTLD** | `.edu`, `.gov` | **Sponsored**: Khusus untuk tujuan institusi resmi/tertentu. |

#### Temuan Domain dalam Email:
Dengan metode *hovering* (mengarahkan kursor tanpa mengklik), ditemukan URL tujuan:
> **Domain:** `storage.googleapis.com`

**Analisis Risiko:** Walaupun domain `googleapis.com` adalah legal (milik Google), penggunaannya dalam konteks ini mencurigakan karena sering dimanfaatkan penyerang untuk menyimpan halaman phishing agar terlihat "resmi".

<br>
<img width="519" alt="Hover Link Analysis" src="https://github.com/user-attachments/assets/eadb1a43-d4f9-4cc1-a632-90b94edf3174" />
<br>

---

### C. Validasi dengan VirusTotal
Langkah validasi akhir dilakukan dengan memindai *Base Domain* pada platform **VirusTotal**.

* **Mekanisme:** VirusTotal membandingkan hash atau URL dengan database ancaman global (malicious signatures).
* **Hasil:** Jika hash atau domain ditemukan dalam database sebagai *malicious*, maka indikator tersebut dianggap berbahaya.

<br>
<img width="1338" alt="VirusTotal Scan" src="https://github.com/user-attachments/assets/becff5c6-285d-460f-84ce-2a6206b65c4b" />
<br>

---

## 🏆 3. Kesimpulan
Berdasarkan investigasi pada ketidaksesuaian `Return-Path`, analisis domain yang mencurigakan, dan hasil verifikasi pada VirusTotal, email ini diklasifikasikan sebagai **PHISHING**.

---
*Dokumentasi ini dibuat sebagai bagian dari pembelajaran keamanan siber di platform Let's Defend.*
