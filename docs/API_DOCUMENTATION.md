# API Documentation - TPQ Baitus Shuffah Management System

## 📋 Overview

RESTful API untuk Sistem Informasi Management TPQ Baitus Shuffah yang menyediakan endpoints untuk manajemen santri, ustadz, kelas, absensi, nilai, dan pembayaran.

## 🔐 Authentication

### JWT Authentication
```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
    "token_type": "bearer",
    "expires_in": 3600,
    "user": {
      "id": 1,
      "username": "admin",
      "email": "admin@tpq.com",
      "role": "admin"
    }
  }
}
```

### Authorization Header
```http
Authorization: Bearer {token}
```

## 👥 User Management

### Get Current User
```http
GET /api/user
Authorization: Bearer {token}
```

### Update Profile
```http
PUT /api/user/profile
Authorization: Bearer {token}
Content-Type: application/json

{
  "nama_lengkap": "Ahmad Fauzi",
  "no_hp": "081234567890",
  "alamat": "Jl. Masjid No. 123"
}
```

## 🎓 Santri Management

### Get All Santri
```http
GET /api/santri?page=1&limit=10&search=ahmad&kelas_id=1&status=aktif
Authorization: Bearer {token}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "current_page": 1,
    "data": [
      {
        "id": 1,
        "nis": "001001",
        "nama_lengkap": "Ahmad Fauzi",
        "nama_panggilan": "Ahmad",
        "jenis_kelamin": "L",
        "tanggal_lahir": "2015-05-15",
        "alamat": "Jl. Masjid No. 123",
        "no_hp": "081234567890",
        "status": "aktif",
        "kelas": {
          "id": 1,
          "nama_kelas": "Iqro 1A",
          "tingkat": "iqro_1"
        },
        "wali_santri": {
          "id": 1,
          "nama_lengkap": "Budi Santoso",
          "hubungan": "ayah",
          "no_hp": "081234567891"
        }
      }
    ],
    "total": 50,
    "per_page": 10,
    "last_page": 5
  }
}
```

### Create Santri
```http
POST /api/santri
Authorization: Bearer {token}
Content-Type: application/json

{
  "nis": "001002",
  "nama_lengkap": "Fatimah Zahra",
  "nama_panggilan": "Fatimah",
  "jenis_kelamin": "P",
  "tempat_lahir": "Jakarta",
  "tanggal_lahir": "2016-03-20",
  "alamat": "Jl. Pondok No. 456",
  "no_hp": "081234567892",
  "kelas_id": 2,
  "wali_santri_id": 2,
  "tanggal_masuk": "2025-01-01"
}
```

### Get Santri by ID
```http
GET /api/santri/{id}
Authorization: Bearer {token}
```

### Update Santri
```http
PUT /api/santri/{id}
Authorization: Bearer {token}
Content-Type: application/json

{
  "nama_lengkap": "Ahmad Fauzi Updated",
  "alamat": "Jl. Masjid Baru No. 123",
  "kelas_id": 3
}
```

### Delete Santri
```http
DELETE /api/santri/{id}
Authorization: Bearer {token}
```

## 👨‍🏫 Ustadz Management

### Get All Ustadz
```http
GET /api/ustadz?page=1&limit=10&search=ahmad&status=aktif
Authorization: Bearer {token}
```

### Create Ustadz
```http
POST /api/ustadz
Authorization: Bearer {token}
Content-Type: application/json

{
  "nip": "UST001",
  "nama_lengkap": "Ustadz Ahmad",
  "jenis_kelamin": "L",
  "tempat_lahir": "Bandung",
  "tanggal_lahir": "1985-08-15",
  "alamat": "Jl. Pesantren No. 789",
  "no_hp": "081234567893",
  "email": "ustadz.ahmad@tpq.com",
  "pendidikan_terakhir": "S1 Pendidikan Agama Islam",
  "spesialisasi": "Tahfidz, Tajwid",
  "tanggal_bergabung": "2025-01-01"
}
```

## 📚 Kelas Management

### Get All Kelas
```http
GET /api/kelas?tingkat=iqro_1&status=aktif
Authorization: Bearer {token}
```

### Create Kelas
```http
POST /api/kelas
Authorization: Bearer {token}
Content-Type: application/json

{
  "nama_kelas": "Iqro 1A",
  "tingkat": "iqro_1",
  "ustadz_id": 1,
  "kapasitas_maksimal": 15,
  "ruangan": "Ruang A1",
  "deskripsi": "Kelas untuk pemula belajar Iqro 1"
}
```

## 📅 Jadwal Management

### Get Jadwal by Kelas
```http
GET /api/jadwal?kelas_id=1&hari=senin
Authorization: Bearer {token}
```

### Create Jadwal
```http
POST /api/jadwal
Authorization: Bearer {token}
Content-Type: application/json

{
  "kelas_id": 1,
  "ustadz_id": 1,
  "hari": "senin",
  "jam_mulai": "08:00",
  "jam_selesai": "09:30",
  "ruangan": "Ruang A1"
}
```

## ✅ Absensi Management

### Get Absensi
```http
GET /api/absensi?tanggal=2025-01-15&kelas_id=1&santri_id=1
Authorization: Bearer {token}
```

### Record Absensi
```http
POST /api/absensi
Authorization: Bearer {token}
Content-Type: application/json

{
  "santri_id": 1,
  "kelas_id": 1,
  "tanggal": "2025-01-15",
  "status": "hadir",
  "waktu_masuk": "08:00",
  "waktu_keluar": "09:30",
  "keterangan": ""
}
```

### Bulk Absensi
```http
POST /api/absensi/bulk
Authorization: Bearer {token}
Content-Type: application/json

{
  "kelas_id": 1,
  "tanggal": "2025-01-15",
  "absensi": [
    {
      "santri_id": 1,
      "status": "hadir",
      "waktu_masuk": "08:00"
    },
    {
      "santri_id": 2,
      "status": "izin",
      "keterangan": "Sakit"
    }
  ]
}
```

## 📊 Nilai Management

### Get Nilai Santri
```http
GET /api/nilai?santri_id=1&materi_id=1&jenis_penilaian=bacaan
Authorization: Bearer {token}
```

### Input Nilai
```http
POST /api/nilai
Authorization: Bearer {token}
Content-Type: application/json

{
  "santri_id": 1,
  "kelas_id": 1,
  "materi_id": 1,
  "tanggal_penilaian": "2025-01-15",
  "jenis_penilaian": "bacaan",
  "nilai_angka": 85.5,
  "nilai_huruf": "B",
  "catatan": "Bacaan sudah lancar, perlu perbaikan tajwid"
}
```

## 💰 Pembayaran Management

### Get Pembayaran
```http
GET /api/pembayaran?santri_id=1&periode=2025-01&status=lunas
Authorization: Bearer {token}
```

### Process Pembayaran
```http
POST /api/pembayaran
Authorization: Bearer {token}
Content-Type: application/json

{
  "santri_id": 1,
  "jenis_pembayaran_id": 1,
  "periode_pembayaran": "2025-01",
  "nominal": 50000,
  "metode_pembayaran": "transfer",
  "bukti_pembayaran": "bukti_transfer.jpg",
  "keterangan": "Pembayaran SPP Januari 2025"
}
```

### Generate Invoice
```http
POST /api/pembayaran/{id}/invoice
Authorization: Bearer {token}
```

## 📈 Reporting

### Dashboard Statistics
```http
GET /api/dashboard/stats
Authorization: Bearer {token}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "total_santri": 150,
    "total_ustadz": 8,
    "total_kelas": 12,
    "santri_aktif": 145,
    "pembayaran_bulan_ini": 7250000,
    "tingkat_kehadiran": 92.5,
    "santri_per_tingkat": {
      "iqro_1": 25,
      "iqro_2": 30,
      "iqro_3": 28,
      "iqro_4": 22,
      "iqro_5": 20,
      "iqro_6": 15,
      "quran": 5
    }
  }
}
```

### Laporan Absensi
```http
GET /api/reports/absensi?start_date=2025-01-01&end_date=2025-01-31&kelas_id=1&format=pdf
Authorization: Bearer {token}
```

### Laporan Pembayaran
```http
GET /api/reports/pembayaran?periode=2025-01&status=all&format=excel
Authorization: Bearer {token}
```

## 🔔 Notifications

### Send WhatsApp Notification
```http
POST /api/notifications/whatsapp
Authorization: Bearer {token}
Content-Type: application/json

{
  "recipient": "081234567890",
  "template": "payment_reminder",
  "data": {
    "nama_santri": "Ahmad Fauzi",
    "bulan": "Januari 2025",
    "nominal": "Rp 50.000"
  }
}
```

## 📱 Mobile API Endpoints

### Sync Data for Offline
```http
GET /api/mobile/sync?last_sync=2025-01-15T10:30:00Z
Authorization: Bearer {token}
```

### Upload Offline Data
```http
POST /api/mobile/upload
Authorization: Bearer {token}
Content-Type: application/json

{
  "absensi": [...],
  "nilai": [...],
  "timestamp": "2025-01-15T15:30:00Z"
}
```

## ❌ Error Responses

### Validation Error (422)
```json
{
  "success": false,
  "message": "Validation failed",
  "errors": {
    "nama_lengkap": ["Nama lengkap wajib diisi"],
    "email": ["Format email tidak valid"]
  }
}
```

### Unauthorized (401)
```json
{
  "success": false,
  "message": "Unauthorized",
  "error": "Token tidak valid atau sudah expired"
}
```

### Not Found (404)
```json
{
  "success": false,
  "message": "Data tidak ditemukan",
  "error": "Santri dengan ID 999 tidak ditemukan"
}
```

### Server Error (500)
```json
{
  "success": false,
  "message": "Internal server error",
  "error": "Terjadi kesalahan pada server"
}
```

## 📊 Rate Limiting

- **Default**: 60 requests per minute per IP
- **Authenticated**: 100 requests per minute per user
- **Admin**: 200 requests per minute

## 🔧 API Versioning

Current version: `v1`

Base URL: `https://api.tpq-baitus-shuffah.com/api/v1`

---

**Note**: API documentation akan terus diupdate seiring dengan development progress.
