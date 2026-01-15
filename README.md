# 🏫 Website Pengaduan Sarana Sekolah  
(Node.js, Express, MongoDB)

Website Pengaduan Sarana Sekolah adalah aplikasi berbasis web untuk menampung dan mengelola laporan kerusakan fasilitas sekolah seperti ruang kelas, laboratorium, toilet, dan sarana lainnya secara online.

---

## 🎯 Tujuan
- Mempermudah siswa/guru dalam menyampaikan pengaduan
- Membantu admin menindaklanjuti pengaduan
- Menyediakan bukti pengaduan berupa gambar atau video

---

## 🛠️ Teknologi
- Node.js
- Express.js
- MongoDB + Mongoose
- JWT Authentication
- Multer (Upload File)

---

## 📁 Struktur Folder
```
pengaduan-sarana-sekolah/
├── src/
│   ├── config/db.js
│   ├── models/
│   │   ├── User.js
│   │   ├── Lokasi.js
│   │   └── Pengaduan.js
│   ├── middlewares/
│   │   ├── authMiddleware.js
│   │   └── uploadMiddleware.js
│   ├── controllers/pengaduanController.js
│   ├── routes/pengaduanRoutes.js
│   ├── app.js
│   └── server.js
├── .env
├── package.json
└── README.md
```

---

## 🚀 Cara Membuat Project

### 1️⃣ Inisialisasi
```bash
npm init -y
npm install express mongoose dotenv bcrypt jsonwebtoken multer cors
npm install nodemon --save-dev
```

---

### 2️⃣ Konfigurasi `.env`
```env
PORT=5000
MONGO_URI=your_mongodb_uri
JWT_SECRET=secretkey
```

---

## 🔌 Koneksi Database
**src/config/db.js**
```js
const mongoose = require("mongoose");

const connectDB = async () => {
  try {
    await mongoose.connect(process.env.MONGO_URI);
    console.log("MongoDB Connected");
  } catch (err) {
    console.error(err);
    process.exit(1);
  }
};

module.exports = connectDB;
```

---

## 👤 Model User
**src/models/User.js**
```js
const mongoose = require("mongoose");

const UserSchema = new mongoose.Schema({
  nama: String,
  email: { type: String, unique: true },
  password: String,
  role: { type: String, default: "user" }
}, { timestamps: true });

module.exports = mongoose.model("User", UserSchema);
```

---

## 📍 Model Lokasi
**src/models/Lokasi.js**
```js
const mongoose = require("mongoose");

const LokasiSchema = new mongoose.Schema({
  namaLokasi: String
});

module.exports = mongoose.model("Lokasi", LokasiSchema);
```

---

## 📝 Model Pengaduan
**src/models/Pengaduan.js**
```js
const mongoose = require("mongoose");

const PengaduanSchema = new mongoose.Schema({
  userId: { type: mongoose.Schema.Types.ObjectId, ref: "User" },
  judul: String,
  deskripsi: String,
  lokasiId: { type: mongoose.Schema.Types.ObjectId, ref: "Lokasi" },
  bukti: String,
  tipeBukti: { type: String, enum: ["gambar", "video"] },
  status: { type: String, default: "diajukan" },
  tanggapan: String
}, { timestamps: true });

module.exports = mongoose.model("Pengaduan", PengaduanSchema);
```

---

## 📤 Upload Bukti
**src/middlewares/uploadMiddleware.js**
```js
const multer = require("multer");

const storage = multer.diskStorage({
  destination: "src/public/uploads",
  filename: (req, file, cb) => cb(null, Date.now() + "-" + file.originalname)
});

module.exports = multer({ storage });
```

---

## 🧠 Controller Pengaduan
**src/controllers/pengaduanController.js**
```js
const Pengaduan = require("../models/Pengaduan");

exports.createPengaduan = async (req, res) => {
  const pengaduan = await Pengaduan.create({
    userId: req.user.id,
    judul: req.body.judul,
    deskripsi: req.body.deskripsi,
    lokasiId: req.body.lokasiId,
    bukti: req.file?.filename
  });
  res.json(pengaduan);
};
```

---

## 🛣️ Route Pengaduan
**src/routes/pengaduanRoutes.js**
```js
const express = require("express");
const router = express.Router();
const upload = require("../middlewares/uploadMiddleware");
const { createPengaduan } = require("../controllers/pengaduanController");

router.post("/", upload.single("bukti"), createPengaduan);

module.exports = router;
```

---

## ▶️ Menjalankan Aplikasi
```bash
npm run dev
```

Buka browser:
```
http://localhost:5000
```

---

## 📄 Lisensi
Digunakan untuk keperluan pembelajaran.
