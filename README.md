# 🏫 Website Pengaduan Sarana Sekolah  
(Node.js, Express, MongoDB)

Website Pengaduan Sarana Sekolah adalah aplikasi berbasis web yang digunakan untuk menampung laporan kerusakan fasilitas sekolah seperti ruang kelas, laboratorium, toilet, dan sarana lainnya secara online.

Aplikasi ini dibangun menggunakan **Node.js**, **Express.js**, dan **MongoDB** dengan arsitektur REST API.

---

## 🎯 Tujuan Sistem
- Memudahkan siswa/guru dalam menyampaikan pengaduan sarana sekolah
- Membantu admin dalam memantau dan menindaklanjuti pengaduan
- Menyediakan bukti pengaduan berupa gambar atau video
- Mengelola pengaduan secara terstruktur

---

## 👤 Role Pengguna

### User (Siswa / Guru)
- Login
- Membuat pengaduan
- Mengunggah bukti (gambar / video)
- Melihat status pengaduan

### Admin
- Melihat semua pengaduan
- Mengubah status pengaduan
- Memberikan tanggapan
- Mengelola data lokasi

---

## 🛠️ Teknologi yang Digunakan
- Node.js
- Express.js
- MongoDB
- Mongoose
- JSON Web Token (JWT)
- HTML, CSS, JavaScript

Library pendukung:
- bcrypt
- multer
- dotenv
- cors

---

## 📁 Struktur Folder Project

pengaduan-sarana-sekolah/
├── src/
│   ├── config/
│   │   └── db.js
│   ├── models/
│   │   ├── User.js
│   │   ├── Lokasi.js
│   │   └── Pengaduan.js
│   ├── controllers/
│   ├── routes/
│   ├── middlewares/
│   ├── public/
│   │   └── uploads/
│   │       ├── images/
│   │       └── videos/
│   ├── views/
│   ├── app.js
│   └── server.js
│
├── .env
├── package.json
└── README.md

---

## 🚀 Cara Menjalankan Project

1. Install dependency
npm install

2. Jalankan server
npm run dev

Aplikasi berjalan di:
http://localhost:5000

---

## 📄 Lisensi
Project ini dibuat untuk keperluan pembelajaran.
