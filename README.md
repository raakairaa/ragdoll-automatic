# ⚡ Ragdoll Toggle + Proximity + Gameplay Features

README ini menjelaskan fungsi, alur kerja, kebutuhan environment, dan cara memakai script **Ragdoll Toggle + Proximity + Gameplay Features** secara jelas, runtut, dan mudah dibaca.

---

## 📌 Gambaran Umum

Script ini adalah sistem ragdoll berbasis GUI untuk Roblox yang dirancang untuk:

* mengaktifkan dan menonaktifkan ragdoll secara manual,
* memicu ragdoll otomatis saat pemain lain berada terlalu dekat,
* menyediakan mode limp untuk membuat tubuh tampak lemas tanpa full ragdoll,
* menampilkan bar timer pemulihan,
* menonaktifkan animasi berjalan saat ragdoll,
* mengizinkan bangun kembali lewat tombol jump,
* menyertakan efek suara saat jatuh,
* serta menambahkan sistem error logging yang mencoba menyalin error ke clipboard.

Script ini dibuat agar terasa seperti paket fitur lengkap, bukan hanya ragdoll biasa. Ada GUI, animasi transisi, pengaturan jarak proximity, dan mekanisme pemulihan otomatis.

---

## 🎯 Tujuan Script

Script ini dibuat untuk memberi pengalaman gameplay yang lebih hidup saat karakter jatuh, terkena efek ragdoll, atau masuk ke mode lemas. Fokus utamanya adalah:

1. **Kontrol manual** — pemain bisa toggle ragdoll sendiri.
2. **Kontrol otomatis** — ragdoll bisa aktif bila ada pemain lain terlalu dekat.
3. **Kontrol visual** — GUI memiliki tombol, slider, dan animasi transisi.
4. **Kontrol gerak** — animasi berjalan dihentikan agar ragdoll terlihat natural.
5. **Kontrol pemulihan** — karakter bisa bangun otomatis atau lewat jump.

---

## 🧩 Fitur Utama

### 1) Toggle Ragdoll

Tombol utama untuk menghidupkan atau mematikan ragdoll secara manual.

Saat aktif:

* Motor6D pada karakter diubah menjadi constraint fisik,
* tubuh jatuh dan bergerak secara fisik,
* animasi default dimatikan,
* status tombol berubah menjadi **Unragdoll**.

Saat dimatikan:

* constraint ragdoll dihapus,
* Motor6D dipulihkan,
* karakter kembali normal,
* animasi dan kontrol gerak dipulihkan.

---

### 2) Proximity Ragdoll

Script memantau jarak antar pemain. Jika pemain lain berada di dalam radius tertentu, karakter akan otomatis jatuh ke ragdoll.

Fitur ini bisa dinyalakan atau dimatikan lewat tombol **Proximity**.

---

### 3) Sensitivity Slider

Slider digunakan untuk mengatur jarak proximity.

Rentang jarak:

* **Minimum:** 1.0 stud
* **Maximum:** 10.0 stud

Label akan menampilkan nilai jarak yang sedang dipakai, misalnya:

`Proximity: 3.5 stud`

---

### 4) Recovery Timer Bar

Saat ragdoll otomatis aktif, GUI menampilkan bar pemulihan.

Fungsinya:

* memberi tahu bahwa karakter akan bangun dalam beberapa detik,
* memperlihatkan progress pemulihan secara visual,
* membantu pemain memahami status karakter.

---

### 5) Limp Mode

Mode ini membuat sebagian sendi karakter menjadi lebih lemas tanpa mengubah seluruh tubuh menjadi ragdoll penuh.

Cocok untuk efek:

* cedera,
* limbung,
* tubuh tidak stabil,
* animasi fisik yang lebih ringan daripada ragdoll penuh.

---

### 6) Auto Recovery

Jika ragdoll dipicu otomatis oleh proximity, script bisa memulihkan karakter sendiri setelah waktu tertentu.

Ini membuat efek jatuh terasa sementara dan tidak mengunci pemain terlalu lama.

---

### 7) Bangun Pakai Tombol Jump

Saat karakter sedang ragdoll, menekan tombol lompat akan memanggil pemulihan.

Ini berguna untuk:

* mobile,
* keyboard,
* kontrol yang lebih cepat,
* membangun ulang gameplay yang responsif.

---

### 8) Efek Suara Saat Jatuh

Script mencoba memutar suara jatuh dari URL eksternal.

Karena audio eksternal bergantung pada support environment, fitur ini memakai mekanisme:

* download audio,
* simpan file,
* load sebagai asset custom,
* putar beberapa kali agar efek suara lebih kuat.

---

### 9) Auto Copy Error ke Clipboard

Jika terjadi error, script akan:

* membuat laporan error,
* menambahkan waktu kejadian,
* mencoba menyalin error ke clipboard,
* lalu menampilkan hasilnya di output.

Fitur ini sangat membantu saat debugging.

---

### 10) GUI Minimizer / Expander

GUI bisa diperkecil dan diperbesar tanpa menghapus state fitur.

Ini berguna agar tampilan tidak mengganggu gameplay saat tidak dibutuhkan.

---

## 🧠 Cara Kerja Script

Script berjalan dengan urutan logika seperti ini:

1. **Membuat GUI**

   * frame utama,
   * tombol toggle ragdoll,
   * tombol proximity,
   * tombol limp mode,
   * slider jarak,
   * bar timer pemulihan.

2. **Menyimpan state karakter**

   * WalkSpeed,
   * JumpPower,
   * JumpHeight,
   * AutoRotate,
   * status Animate.

3. **Mengubah motor ke constraint fisik**

   * Motor6D dilepas,
   * Attachment ditambahkan,
   * BallSocketConstraint dibangun,
   * tubuh jadi ragdoll.

4. **Memonitor proximity**

   * setiap Heartbeat, script cek pemain lain,
   * jika terlalu dekat, ragdoll otomatis aktif.

5. **Mengelola recovery**

   * timer tampil,
   * status cooldown dijaga,
   * karakter dipulihkan setelah waktu tertentu.

6. **Mendeteksi respawn**

   * saat karakter respawn, semua state di-reset,
   * GUI dan fitur tetap konsisten.

---

## 🏗️ Struktur Komponen

### A. Error Handler

Bagian ini menangani error secara aman dengan `xpcall` dan traceback.

### B. Audio System

Bagian ini mengunduh dan memutar suara jatuh.

### C. Tween Helper

Bagian ini mengatur animasi warna dan ukuran GUI.

### D. GUI Builder

Bagian ini membuat semua elemen tampilan.

### E. State Manager

Bagian ini menyimpan status seperti:

* ragdoll aktif atau tidak,
* limp aktif atau tidak,
* proximity aktif atau tidak,
* cooldown,
* token untuk mencegah thread lama bertabrakan.

### F. Physics Controller

Bagian ini mengganti Motor6D menjadi BallSocketConstraint dan mengembalikannya saat pemulihan.

### G. Proximity Watcher

Bagian ini mengecek kedekatan antar pemain secara real-time.

---

## 🔧 Kebutuhan Environment

Script ini membutuhkan environment yang mendukung fitur Roblox dan beberapa fungsi tambahan dari executor tertentu.

### Wajib tersedia

* `game:GetService(...)`
* `TweenService`
* `RunService`
* `UserInputService`
* `Humanoid`
* `Motor6D`
* `BallSocketConstraint`

### Untuk fitur tambahan audio/clipboard

Tergantung environment, fitur berikut bisa tersedia atau tidak:

* `setclipboard` / `toclipboard`
* `writefile`
* `getcustomasset` / `getsynasset`
* `isfile`
* `game:HttpGet` atau request library yang tersedia di executor

Jika fungsi-fungsi itu tidak tersedia, script tetap bisa berjalan, tetapi fitur tertentu mungkin tidak aktif.

---

## 🧪 Status Fitur Berdasarkan Environment

| Fitur                | Status              |
| -------------------- | ------------------- |
| GUI utama            | Wajib               |
| Toggle ragdoll       | Wajib               |
| Proximity ragdoll    | Wajib               |
| Limp mode            | Wajib               |
| Timer recovery       | Wajib               |
| Jump to get up       | Wajib               |
| Smooth tween         | Wajib               |
| Auto copy error      | Tergantung executor |
| Audio eksternal      | Tergantung executor |
| Custom asset loading | Tergantung executor |

---

## 🕹️ Cara Menggunakan

1. Tempel script ke environment yang sesuai.
2. Jalankan script.
3. GUI akan muncul di layar.
4. Gunakan tombol berikut:

   * **Toggle Ragdoll** untuk ragdoll manual,
   * **Proximity: ON/OFF** untuk aktivasi otomatis,
   * **Limp Mode: ON/OFF** untuk mode lemas,
   * slider untuk mengubah jarak deteksi.
5. Saat ragdoll aktif, tekan jump untuk bangun.

---

## 🧷 Penjelasan Tombol GUI

### Toggle Ragdoll

Mengubah karakter antara normal dan ragdoll.

### Proximity: ON/OFF

Menghidupkan atau mematikan deteksi jarak dekat.

### Limp Mode: ON/OFF

Mengaktifkan mode tubuh lemas tanpa full ragdoll.

### Tombol Minimize

Mengecilkan atau memperbesar tampilan GUI.

---

## 🧭 Alur Penggunaan yang Disarankan

Untuk hasil paling nyaman, gunakan urutan seperti ini:

1. Buka GUI.
2. Atur proximity sesuai kebutuhan.
3. Nyalakan proximity bila ingin efek otomatis.
4. Gunakan limp mode bila hanya ingin efek jatuh ringan.
5. Gunakan ragdoll manual saat dibutuhkan.
6. Tekan jump untuk bangun cepat.

---

## ⚠️ Catatan Penting

* Script ini sangat bergantung pada struktur karakter Roblox yang normal.
* Jika avatar memakai struktur tidak standar, beberapa bagian motor/joint bisa berbeda.
* Audio eksternal tidak selalu berhasil di semua executor.
* Beberapa environment mungkin membatasi clipboard, file access, atau request HTTP.
* Jika ada error, script mencoba memberi laporan yang lebih mudah dibaca.

---

## 🛠️ Troubleshooting

### 1) GUI tidak muncul

Kemungkinan penyebab:

* `PlayerGui` belum siap,
* script dijalankan terlalu cepat,
* environment memblokir pembuatan GUI.

### 2) Ragdoll tidak aktif

Kemungkinan penyebab:

* karakter belum siap,
* Humanoid tidak ditemukan,
* struktur motor berbeda dari normal.

### 3) Audio tidak terdengar

Kemungkinan penyebab:

* executor tidak mendukung `writefile` atau `getcustomasset`,
* URL audio tidak bisa diakses,
* asset custom gagal dibuat.

### 4) Error tidak tercopy ke clipboard

Kemungkinan penyebab:

* clipboard function tidak tersedia,
* environment memblokir akses clipboard.

### 5) Proximity terlalu sensitif atau terlalu jauh

Solusi:

* geser slider ke nilai yang lebih cocok,
* cek apakah pemain lain benar-benar berada di radius deteksi.

---

## 🧾 Ringkasan Fungsi Inti

Script ini adalah sistem ragdoll lengkap dengan fitur:

* kontrol manual,
* kontrol otomatis berbasis jarak,
* mode limp,
* bar pemulihan,
* bangun lewat jump,
* animasi GUI halus,
* suara jatuh,
* dan logging error.

Secara sederhana, script ini membuat karakter Roblox terasa lebih hidup, lebih dinamis, dan lebih interaktif saat jatuh atau masuk kondisi fisik tertentu.

---

## 📎 Catatan Teknis

Script asli menggunakan beberapa gaya penulisan modern. Untuk environment Lua 5.1 seperti Prometheus, bagian-bagian tertentu perlu ditulis ulang agar parser tidak error. Karena itu, versi yang kompatibel biasanya memakai:

* `unpack` вместо `table.unpack`,
* `delay` / `spawn` вместо `task.delay` / `task.spawn`,
* `type(...)` вместо `typeof(...)`,
* `v = v + 1` вместо `v += 1`,
* `if ... then ... return end` вместо `continue`.

---

## ✅ Kesimpulan

README ini menjelaskan bahwa script bukan hanya ragdoll biasa, tetapi sebuah sistem fisika karakter dengan lapisan fitur tambahan yang mencakup UI, kontrol, pemulihan, audio, dan error handling. Dengan pemahaman ini, script akan lebih mudah dipakai, dimodifikasi, dan didiagnosis bila terjadi error.

---

**Versi README:** 1.0
**Bahasa:** Indonesia
**Target:** Lua 5.1 / lingkungan kompatibel Prometheus
omatic
