# Configuration Directory

Folder ini berisi file-file konfigurasi untuk aplikasi TPQ Baitus Shuffah.

## 📁 Struktur Konfigurasi

```
config/
├── app.php              # Konfigurasi aplikasi utama
├── database.php         # Konfigurasi database
├── auth.php            # Konfigurasi authentication
├── mail.php            # Konfigurasi email
├── whatsapp.php        # Konfigurasi WhatsApp API
├── payment.php         # Konfigurasi payment gateway
├── logging.php         # Konfigurasi logging
├── cache.php           # Konfigurasi caching
├── session.php         # Konfigurasi session
└── cors.php            # Konfigurasi CORS
```

## ⚙️ Konfigurasi yang Akan Dibuat

### 1. Application Config (app.php)
```php
<?php
return [
    'name' => env('APP_NAME', 'TPQ Baitus Shuffah'),
    'env' => env('APP_ENV', 'production'),
    'debug' => env('APP_DEBUG', false),
    'url' => env('APP_URL', 'http://localhost'),
    'timezone' => 'Asia/Jakarta',
    'locale' => 'id',
    'fallback_locale' => 'en',
    'faker_locale' => 'id_ID',
    'key' => env('APP_KEY'),
    'cipher' => 'AES-256-CBC',
];
```

### 2. Database Config (database.php)
```php
<?php
return [
    'default' => env('DB_CONNECTION', 'mysql'),
    'connections' => [
        'mysql' => [
            'driver' => 'mysql',
            'host' => env('DB_HOST', '127.0.0.1'),
            'port' => env('DB_PORT', '3306'),
            'database' => env('DB_DATABASE', 'tpq_baitus_shuffah'),
            'username' => env('DB_USERNAME', 'root'),
            'password' => env('DB_PASSWORD', ''),
            'charset' => 'utf8mb4',
            'collation' => 'utf8mb4_unicode_ci',
            'prefix' => '',
            'strict' => true,
            'engine' => null,
        ],
    ],
    'migrations' => 'migrations',
];
```

### 3. Authentication Config (auth.php)
```php
<?php
return [
    'defaults' => [
        'guard' => 'web',
        'passwords' => 'users',
    ],
    'guards' => [
        'web' => [
            'driver' => 'session',
            'provider' => 'users',
        ],
        'api' => [
            'driver' => 'jwt',
            'provider' => 'users',
        ],
    ],
    'providers' => [
        'users' => [
            'driver' => 'eloquent',
            'model' => App\Models\User::class,
        ],
    ],
    'passwords' => [
        'users' => [
            'provider' => 'users',
            'table' => 'password_resets',
            'expire' => 60,
            'throttle' => 60,
        ],
    ],
    'password_timeout' => 10800,
];
```

### 4. Mail Config (mail.php)
```php
<?php
return [
    'default' => env('MAIL_MAILER', 'smtp'),
    'mailers' => [
        'smtp' => [
            'transport' => 'smtp',
            'host' => env('MAIL_HOST', 'smtp.gmail.com'),
            'port' => env('MAIL_PORT', 587),
            'encryption' => env('MAIL_ENCRYPTION', 'tls'),
            'username' => env('MAIL_USERNAME'),
            'password' => env('MAIL_PASSWORD'),
            'timeout' => null,
        ],
    ],
    'from' => [
        'address' => env('MAIL_FROM_ADDRESS', 'noreply@tpq-baitus-shuffah.com'),
        'name' => env('MAIL_FROM_NAME', 'TPQ Baitus Shuffah'),
    ],
];
```

### 5. WhatsApp Config (whatsapp.php)
```php
<?php
return [
    'api_url' => env('WHATSAPP_API_URL'),
    'api_token' => env('WHATSAPP_API_TOKEN'),
    'sender_number' => env('WHATSAPP_SENDER_NUMBER'),
    'templates' => [
        'payment_reminder' => [
            'id' => 'payment_reminder_template',
            'message' => 'Assalamu\'alaikum. Reminder pembayaran SPP {nama_santri} bulan {bulan} sebesar Rp {nominal}. Terima kasih.',
        ],
        'absensi_notification' => [
            'id' => 'absensi_notification',
            'message' => 'Assalamu\'alaikum. {nama_santri} {status_absensi} pada hari ini. Terima kasih.',
        ],
    ],
];
```

### 6. Payment Gateway Config (payment.php)
```php
<?php
return [
    'default_gateway' => env('PAYMENT_DEFAULT_GATEWAY', 'midtrans'),
    'gateways' => [
        'midtrans' => [
            'server_key' => env('MIDTRANS_SERVER_KEY'),
            'client_key' => env('MIDTRANS_CLIENT_KEY'),
            'is_production' => env('MIDTRANS_IS_PRODUCTION', false),
            'is_sanitized' => true,
            'is_3ds' => true,
        ],
        'xendit' => [
            'secret_key' => env('XENDIT_SECRET_KEY'),
            'public_key' => env('XENDIT_PUBLIC_KEY'),
            'webhook_token' => env('XENDIT_WEBHOOK_TOKEN'),
        ],
    ],
    'supported_methods' => [
        'bank_transfer',
        'credit_card',
        'e_wallet',
        'qris',
        'virtual_account',
    ],
];
```

### 7. Logging Config (logging.php)
```php
<?php
return [
    'default' => env('LOG_CHANNEL', 'stack'),
    'channels' => [
        'stack' => [
            'driver' => 'stack',
            'channels' => ['single', 'daily'],
            'ignore_exceptions' => false,
        ],
        'single' => [
            'driver' => 'single',
            'path' => storage_path('logs/laravel.log'),
            'level' => env('LOG_LEVEL', 'debug'),
        ],
        'daily' => [
            'driver' => 'daily',
            'path' => storage_path('logs/laravel.log'),
            'level' => env('LOG_LEVEL', 'debug'),
            'days' => 14,
        ],
        'payment' => [
            'driver' => 'daily',
            'path' => storage_path('logs/payment.log'),
            'level' => 'info',
            'days' => 30,
        ],
        'absensi' => [
            'driver' => 'daily',
            'path' => storage_path('logs/absensi.log'),
            'level' => 'info',
            'days' => 90,
        ],
    ],
];
```

## 🔐 Environment Variables

### .env.example
```bash
# Application
APP_NAME="TPQ Baitus Shuffah"
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost:8000

# Database
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=tpq_baitus_shuffah
DB_USERNAME=root
DB_PASSWORD=

# Mail
MAIL_MAILER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_USERNAME=
MAIL_PASSWORD=
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=noreply@tpq-baitus-shuffah.com
MAIL_FROM_NAME="TPQ Baitus Shuffah"

# WhatsApp API
WHATSAPP_API_URL=
WHATSAPP_API_TOKEN=
WHATSAPP_SENDER_NUMBER=

# Payment Gateway
PAYMENT_DEFAULT_GATEWAY=midtrans
MIDTRANS_SERVER_KEY=
MIDTRANS_CLIENT_KEY=
MIDTRANS_IS_PRODUCTION=false

# Cache & Session
CACHE_DRIVER=file
SESSION_DRIVER=file
SESSION_LIFETIME=120

# Queue
QUEUE_CONNECTION=sync

# Logging
LOG_CHANNEL=stack
LOG_LEVEL=debug
```

## 📋 Configuration Best Practices

### 1. Security
- Jangan commit file .env ke repository
- Gunakan environment variables untuk sensitive data
- Rotate API keys secara berkala
- Implement proper validation untuk config values

### 2. Performance
- Cache configuration di production
- Minimize config file loading
- Use appropriate data types
- Optimize database connections

### 3. Maintainability
- Group related configurations
- Use descriptive naming
- Add comments untuk complex configurations
- Version control untuk config changes

---

**Note**: File konfigurasi akan dibuat sesuai dengan technology stack yang dipilih.
