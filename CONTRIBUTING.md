# Contributing to Sistem Informasi Management TPQ Baitus Shuffah

Terima kasih atas minat Anda untuk berkontribusi pada project ini! 🎉

## 🤝 Cara Berkontribusi

### 1. Fork Repository
- Fork repository ini ke akun GitHub Anda
- Clone fork tersebut ke local machine

### 2. Setup Development Environment
```bash
git clone https://github.com/YOUR_USERNAME/sistem-informasi-management-tpq-baitus-shuffah.git
cd sistem-informasi-management-tpq-baitus-shuffah
# Install dependencies sesuai teknologi yang digunakan
```

### 3. Buat Branch Baru
```bash
git checkout -b feature/nama-fitur-anda
# atau
git checkout -b fix/nama-bug-yang-diperbaiki
```

### 4. Coding Guidelines

#### Penamaan Branch
- `feature/` - untuk fitur baru
- `fix/` - untuk perbaikan bug
- `docs/` - untuk update dokumentasi
- `refactor/` - untuk refactoring code

#### Commit Message Format
```
type(scope): description

[optional body]

[optional footer]
```

**Types:**
- `feat`: fitur baru
- `fix`: perbaikan bug
- `docs`: perubahan dokumentasi
- `style`: formatting, missing semicolons, etc
- `refactor`: refactoring code
- `test`: menambah atau memperbaiki tests
- `chore`: maintenance tasks

**Contoh:**
```
feat(auth): add login functionality for ustadz role

- Implement JWT authentication
- Add role-based access control
- Create login form validation

Closes #123
```

### 5. Testing
- Pastikan semua test existing masih pass
- Tambahkan test untuk fitur baru
- Test coverage minimal 80%

### 6. Pull Request
1. Push branch Anda ke fork
2. Buat Pull Request ke repository utama
3. Isi template PR dengan lengkap
4. Tunggu review dari maintainer

## 📋 Development Standards

### Code Style
- Gunakan indentasi 2 atau 4 spasi (konsisten)
- Nama variabel dan function menggunakan camelCase
- Nama class menggunakan PascalCase
- Nama file menggunakan kebab-case
- Komentar dalam Bahasa Indonesia untuk business logic

### Database
- Nama tabel menggunakan snake_case
- Nama kolom menggunakan snake_case
- Gunakan migration untuk perubahan database
- Selalu backup sebelum migration

### Security
- Validasi semua input user
- Gunakan prepared statements
- Implement proper authentication
- Sanitize output data

## 🐛 Melaporkan Bug

### Sebelum Melaporkan
- Cek apakah bug sudah dilaporkan di Issues
- Pastikan Anda menggunakan versi terbaru
- Coba reproduce bug di environment yang bersih

### Format Laporan Bug
```markdown
**Deskripsi Bug**
Penjelasan singkat tentang bug

**Langkah Reproduce**
1. Buka halaman...
2. Klik tombol...
3. Isi form dengan...
4. Lihat error

**Expected Behavior**
Apa yang seharusnya terjadi

**Actual Behavior**
Apa yang benar-benar terjadi

**Screenshots**
Jika applicable, tambahkan screenshots

**Environment:**
- OS: [e.g. Windows 10]
- Browser: [e.g. Chrome 91]
- Version: [e.g. v1.2.0]
```

## 💡 Mengusulkan Fitur

### Format Usulan Fitur
```markdown
**Deskripsi Fitur**
Penjelasan detail fitur yang diusulkan

**Problem yang Diselesaikan**
Masalah apa yang akan diselesaikan fitur ini

**Solusi yang Diusulkan**
Bagaimana fitur ini akan menyelesaikan masalah

**Alternatif yang Dipertimbangkan**
Solusi alternatif lain yang sudah dipertimbangkan

**Mockup/Wireframe**
Jika ada, lampirkan mockup atau wireframe
```

## 📞 Komunikasi

- **GitHub Issues**: Untuk bug reports dan feature requests
- **GitHub Discussions**: Untuk diskusi umum
- **Email**: novirianarosita13@gmail.com untuk hal urgent

## 📄 License

Dengan berkontribusi, Anda setuju bahwa kontribusi Anda akan dilisensikan di bawah MIT License yang sama dengan project ini.

---

Terima kasih telah berkontribusi! 🙏
