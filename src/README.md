# Source Code Directory

Folder ini berisi source code utama aplikasi Sistem Informasi Management TPQ Baitus Shuffah.

## 📁 Struktur yang Direncanakan

### Backend (contoh untuk Laravel)
```
src/
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── AuthController.php
│   │   │   ├── SantriController.php
│   │   │   ├── UstadzController.php
│   │   │   ├── KelasController.php
│   │   │   ├── AbsensiController.php
│   │   │   ├── NilaiController.php
│   │   │   └── PembayaranController.php
│   │   ├── Middleware/
│   │   └── Requests/
│   ├── Models/
│   │   ├── User.php
│   │   ├── Santri.php
│   │   ├── Ustadz.php
│   │   ├── WaliSantri.php
│   │   ├── Kelas.php
│   │   ├── Jadwal.php
│   │   ├── Absensi.php
│   │   ├── Nilai.php
│   │   └── Pembayaran.php
│   └── Services/
├── resources/
│   ├── views/
│   ├── js/
│   └── css/
└── routes/
    ├── web.php
    └── api.php
```

### Frontend (contoh untuk React/Vue)
```
src/
├── components/
│   ├── common/
│   ├── auth/
│   ├── dashboard/
│   ├── santri/
│   ├── ustadz/
│   ├── kelas/
│   ├── absensi/
│   ├── nilai/
│   └── pembayaran/
├── pages/
├── services/
├── utils/
└── assets/
```

## 🚀 Getting Started

1. Pilih technology stack yang akan digunakan
2. Setup development environment sesuai INSTALLATION.md
3. Mulai implementasi sesuai roadmap di README.md

## 📝 Coding Standards

- Ikuti PSR-12 untuk PHP atau ESLint untuk JavaScript
- Gunakan meaningful naming conventions
- Tambahkan comments untuk business logic
- Write unit tests untuk setiap feature

---

**Note**: Struktur ini akan dibuat seiring dengan development progress.
