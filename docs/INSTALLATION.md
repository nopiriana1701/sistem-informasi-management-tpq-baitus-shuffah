# Panduan Instalasi Sistem Informasi Management TPQ Baitus Shuffah

## 📋 Prerequisites

### Sistem Requirements
- **OS**: Windows 10/11, macOS 10.15+, atau Linux Ubuntu 18.04+
- **RAM**: Minimal 4GB (Recommended 8GB)
- **Storage**: Minimal 2GB free space
- **Internet**: Koneksi stabil untuk download dependencies

### Software Requirements
```bash
# Akan disesuaikan dengan teknologi stack yang dipilih
# Contoh untuk Laravel + MySQL:

- PHP >= 8.0
- Composer >= 2.0
- MySQL >= 8.0 atau PostgreSQL >= 12
- Node.js >= 16.0
- NPM >= 8.0
- Git >= 2.30
```

## 🚀 Instalasi Development Environment

### 1. Clone Repository
```bash
git clone https://github.com/nopiriana1701/sistem-informasi-management-tpq-baitus-shuffah.git
cd sistem-informasi-management-tpq-baitus-shuffah
```

### 2. Setup Backend (Laravel Example)
```bash
# Install PHP dependencies
composer install

# Copy environment file
cp .env.example .env

# Generate application key
php artisan key:generate

# Setup database connection di .env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=tpq_baitus_shuffah
DB_USERNAME=your_username
DB_PASSWORD=your_password
```

### 3. Setup Database
```bash
# Create database
mysql -u root -p
CREATE DATABASE tpq_baitus_shuffah;
exit

# Run migrations
php artisan migrate

# Seed initial data
php artisan db:seed
```

### 4. Setup Frontend
```bash
# Install Node.js dependencies
npm install

# Build assets for development
npm run dev

# Or watch for changes
npm run watch
```

### 5. Start Development Server
```bash
# Start Laravel server
php artisan serve

# Start frontend build process (new terminal)
npm run watch

# Access application at: http://localhost:8000
```

## 🐳 Docker Installation (Alternative)

### Prerequisites
- Docker >= 20.0
- Docker Compose >= 2.0

### Setup dengan Docker
```bash
# Clone repository
git clone https://github.com/nopiriana1701/sistem-informasi-management-tpq-baitus-shuffah.git
cd sistem-informasi-management-tpq-baitus-shuffah

# Copy environment file
cp .env.example .env

# Build dan start containers
docker-compose up -d

# Install dependencies
docker-compose exec app composer install
docker-compose exec app npm install

# Run migrations
docker-compose exec app php artisan migrate --seed

# Access application at: http://localhost:8000
```

## 🔧 Konfigurasi

### Environment Variables
```bash
# Application
APP_NAME="TPQ Baitus Shuffah"
APP_ENV=local
APP_DEBUG=true
APP_URL=http://localhost:8000

# Database
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=tpq_baitus_shuffah
DB_USERNAME=root
DB_PASSWORD=

# Mail Configuration
MAIL_MAILER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_USERNAME=your-email@gmail.com
MAIL_PASSWORD=your-app-password
MAIL_ENCRYPTION=tls

# WhatsApp API (Optional)
WHATSAPP_API_URL=
WHATSAPP_API_TOKEN=
```

### File Permissions (Linux/macOS)
```bash
sudo chown -R $USER:www-data storage
sudo chown -R $USER:www-data bootstrap/cache
chmod -R 775 storage
chmod -R 775 bootstrap/cache
```

## 🧪 Testing Installation

### Run Tests
```bash
# Backend tests
php artisan test

# Frontend tests
npm run test

# Check code style
./vendor/bin/phpcs
npm run lint
```

### Verify Installation
1. **Database Connection**: Cek apakah bisa connect ke database
2. **File Permissions**: Pastikan storage dan cache writable
3. **Dependencies**: Semua package terinstall dengan benar
4. **Environment**: Semua environment variables ter-set

## 🚨 Troubleshooting

### Common Issues

#### 1. Composer Install Error
```bash
# Clear composer cache
composer clear-cache

# Update composer
composer self-update

# Install with verbose output
composer install -v
```

#### 2. NPM Install Error
```bash
# Clear npm cache
npm cache clean --force

# Delete node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

#### 3. Database Connection Error
- Pastikan MySQL/PostgreSQL service running
- Cek credentials di .env file
- Pastikan database sudah dibuat
- Cek firewall settings

#### 4. Permission Denied Error
```bash
# Fix storage permissions
sudo chmod -R 775 storage bootstrap/cache
sudo chown -R $USER:www-data storage bootstrap/cache
```

#### 5. Port Already in Use
```bash
# Check what's using port 8000
lsof -i :8000

# Use different port
php artisan serve --port=8080
```

## 📱 Mobile App Setup (Future)
```bash
# React Native setup
npm install -g react-native-cli

# Flutter setup
flutter doctor
flutter pub get
```

## 🔄 Update Installation
```bash
# Pull latest changes
git pull origin main

# Update dependencies
composer update
npm update

# Run new migrations
php artisan migrate

# Clear caches
php artisan cache:clear
php artisan config:clear
php artisan view:clear
```

## 📞 Support

Jika mengalami masalah instalasi:
1. Cek dokumentasi troubleshooting di atas
2. Search di GitHub Issues
3. Buat issue baru dengan detail error
4. Contact: novirianarosita13@gmail.com

---

**Note**: Dokumentasi ini akan diupdate seiring dengan development progress.
