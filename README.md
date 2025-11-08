# Implementasi Algoritma Round Robin  
### Sistem Multi-Agent dan Multi-Client untuk Load Balancing Dinamis  

Repositori ini berisi implementasi lengkap **algoritma Round Robin** untuk mendistribusikan beban permintaan antar dua server backend (Agent-1 dan Agent-2) di jaringan lokal (LAN). Proyek ini dikembangkan sebagai bagian dari penelitian dan praktikum **Jaringan Komputer & Sistem Terdistribusi** di Universitas Sulawesi Barat.

---

## 🧩 Tujuan Proyek
🎯 Menerapkan **algoritma Round Robin** untuk membagi beban permintaan antar backend server.  
🎯 Menguji performa load balancing dengan **dua pendekatan berbeda**:
- **Python Flask Load Balancer**
- **NGINX Reverse Proxy**  
🎯 Menganalisis waktu respons rata-rata dan distribusi beban antar agent.

---

## 🏗️ Arsitektur Sistem

| Komponen | Perangkat | IP Address | Port | Peran |
|:----------|:-----------|:------------|:------|:-------|
| 🖥️ **Agent-1** | Windows Laptop | `192.168.1.70` | `5001` | Server backend 1 (Flask + HTML) |
| 💻 **Agent-2** | Ubuntu Laptop | `192.168.1.72` | `5002` | Server backend 2 (Flask + HTML) |
| ⚙️ **Load Balancer** | Ubuntu Laptop | `192.168.1.72` | `8000` | Load Balancer (Python / NGINX) |

**Alur sistem:**  
```
Client → Load Balancer (Ubuntu:8000)
          ↳ Agent-1 (Windows:5001)
          ↳ Agent-2 (Ubuntu:5002)
```

---

## 📘 File Notebook Utama

Berikut tiga file `.ipynb` utama yang berisi kode dan panduan lengkap proyek ini:

| 🧾 No | 📁 File | 📖 Deskripsi | 🔗 Akses |
|:--:|:--|:--|:--|
| 1️⃣ | **`panduan_roundrobin_python_flask`** | Panduan lengkap konfigurasi Python Flask (Load Balancer) sebagai Load Balancer manual. | [📘Lihat](https://github.com/WiwiNopiana123/Load-Balancer-System/blob/main/panduan_roundrobin_python_flask.ipynb) |
| 2️⃣ | **`panduan_roundrobin_html`** | Panduan lengkap konfigurasi Load Blancer manual dengan .html + Python Flask | [📘Lihat](https://github.com/WiwiNopiana123/Load-Balancer-System/blob/main/panduan_roundrobin_html.ipynb) |
| 3️⃣ | **`panduan_roundrobin_nginx`** | Panduan lengkap konfigurasi NGINX sebagai Load Balancer otomatis. | [📘Lihat](https://github.com/WiwiNopiana123/Load-Balancer-System/blob/main//panduan_roundrobin_nginx.ipynb) |

---

## 🧠 Fitur Utama

✅ **Load Balancing Dinamis** — pembagian request secara bergantian antar agent.  
✅ **2 Mode Implementasi:** Flask & NGINX.  
✅ **Web Visual HTML** untuk membedakan backend aktif (Agent-1 biru, Agent-2 hijau).  
✅ **Logging Otomatis** dalam `lb_log.csv`.  
✅ **Analisis Statistik** (rata-rata & deviasi standar waktu respons).  
✅ **Uji Beban Otomatis**: 50, 100, dan 200 request.

---

## 📊 Ringkasan Hasil Uji

| Jumlah Request | Rata-rata (ms) | Deviasi Std (ms) | Keterangan |
|:---------------:|:---------------:|:----------------:|:------------|
| 50 | 110 | 8 | Stabil pada beban ringan |
| 100 | 165 | 11 | Sedikit peningkatan waktu respons |
| 200 | 290 | 17 | Tetap di bawah 300 ms (kategori baik) |

🧾 Sistem tetap **stabil dan seimbang** pada pembagian beban dua server di jaringan lokal.

---

## ⚙️ Struktur Proyek

```
loadbalancer/
│
├── roundrobin-python.ipynb
├── petunjuk_roundrobin_dua_komputer.ipynb
├── panduan_nginx_roundrobin.ipynb
├── README.md
└── lb_log.csv   ← hasil log pengujian
```

## 🧩 Versi Implementasi

| Versi | Teknologi | Load Balancer | File Panduan |
|:------|:-----------|:----------------|:---------------|
| 🧠 **Versi 1** | Python Flask | `load_balancer.py` (Manual) | [`panduan_roundrobin_python_flask`](https://github.com/WiwiNopiana123/Load-Balancer-System/blob/main/panduan_roundrobin_python_flask.ipynb) |
| ⚙️ **Versi 2** | NGINX Reverse Proxy | `nginx.service` (Otomatis) | [`panduan_roundrobin_nginx.ipynb`](https://github.com/WiwiNopiana123/Load-Balancer-System/blob/main//panduan_roundrobin_nginx.ipynb) |

---

## 🧩 Cara Membedakan Flask Load Balancer vs NGINX Load Balancer

| Ciri | Flask LB Aktif | NGINX LB Aktif |
|:------|:----------------|:----------------|
| Port 8000 dikelola oleh | `python3` | `nginx` |
| Header HTTP | `Server: Werkzeug` | `Server: nginx` |
| Log aktivitas | Ditampilkan di terminal | `/var/log/nginx/roundrobin_access.log` |
| Perlu menjalankan `load_balancer.py` | ✅ Ya | ❌ Tidak perlu |
| Dijalankan via `systemctl` | ❌ Tidak | ✅ Ya |

🔍 **Cek cepat di terminal Ubuntu:**
```bash
sudo lsof -i :8000
systemctl status nginx
curl -I http://192.168.1.72:8000/
```
Jika muncul `Server: nginx` → artinya sistem aktif menggunakan **NGINX** sebagai Load Balancer.

---

## 👨‍💻 Penulis

**Wiwi Nopiana**  
📘 *Implementasi Algoritma Round Robin dalam Sistem Multi-Agent dan Multi-Client untuk Load Balancing Dinamis pada Jaringan Lokal*  
Supervised by **Muh. Fuad Mansyur** & **Wawan Firgiawan**

---

📍 **Repository GitHub:**  
👉 [WiwiNopiana123/Load-Balancer-System](https://github.com/WiwiNopiana123/Load-Balancer-System)

⭐ Jangan lupa beri bintang jika repositori ini bermanfaat 🙌  
🧠 *"Simple architecture, powerful balance."* ⚖️
