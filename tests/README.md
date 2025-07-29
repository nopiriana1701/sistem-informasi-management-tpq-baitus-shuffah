# Tests Directory

Folder ini berisi semua test files untuk aplikasi TPQ Baitus Shuffah.

## 📋 Testing Strategy

### 1. Unit Tests
- Test individual functions dan methods
- Mock dependencies
- Fast execution
- High code coverage target: 80%+

### 2. Integration Tests
- Test interaction antar components
- Database integration
- API endpoints testing
- Service layer testing

### 3. Feature Tests
- End-to-end user workflows
- Browser automation (Selenium/Cypress)
- User acceptance testing

## 🗂️ Struktur Testing

```
tests/
├── Unit/
│   ├── Models/
│   │   ├── SantriTest.php
│   │   ├── UstadzTest.php
│   │   ├── KelasTest.php
│   │   └── PembayaranTest.php
│   ├── Services/
│   │   ├── AuthServiceTest.php
│   │   ├── AbsensiServiceTest.php
│   │   └── PembayaranServiceTest.php
│   └── Helpers/
├── Feature/
│   ├── Auth/
│   │   ├── LoginTest.php
│   │   └── RegisterTest.php
│   ├── Santri/
│   │   ├── CreateSantriTest.php
│   │   ├── UpdateSantriTest.php
│   │   └── DeleteSantriTest.php
│   ├── Absensi/
│   │   ├── RecordAbsensiTest.php
│   │   └── ViewAbsensiTest.php
│   └── Pembayaran/
│       ├── ProcessPaymentTest.php
│       └── GenerateReportTest.php
├── Browser/
│   ├── LoginFlowTest.php
│   ├── SantriManagementTest.php
│   └── PaymentFlowTest.php
└── Fixtures/
    ├── santri_data.json
    ├── ustadz_data.json
    └── test_database.sql
```

## 🧪 Test Cases yang Harus Dibuat

### Authentication & Authorization
- [ ] Login dengan credentials valid
- [ ] Login dengan credentials invalid
- [ ] Role-based access control
- [ ] Session management
- [ ] Password reset flow

### Santri Management
- [ ] Create santri dengan data valid
- [ ] Create santri dengan data invalid
- [ ] Update data santri
- [ ] Delete santri
- [ ] Search dan filter santri
- [ ] Assign santri ke kelas

### Absensi System
- [ ] Record absensi harian
- [ ] Bulk absensi input
- [ ] Generate laporan absensi
- [ ] Notifikasi ketidakhadiran
- [ ] Export absensi data

### Penilaian System
- [ ] Input nilai santri
- [ ] Calculate rata-rata nilai
- [ ] Generate rapor
- [ ] Tracking progress pembelajaran

### Payment System
- [ ] Process pembayaran SPP
- [ ] Generate invoice
- [ ] Payment reminder notifications
- [ ] Financial reporting
- [ ] Payment history tracking

## 🛠️ Testing Tools

### PHP/Laravel
```bash
# PHPUnit untuk unit testing
./vendor/bin/phpunit

# Laravel Dusk untuk browser testing
php artisan dusk

# Code coverage
./vendor/bin/phpunit --coverage-html coverage
```

### JavaScript/Node.js
```bash
# Jest untuk unit testing
npm test

# Cypress untuk E2E testing
npm run cypress:open

# Coverage report
npm run test:coverage
```

## 📊 Test Data Management

### Database Seeding untuk Testing
```php
// TestDatabaseSeeder.php
class TestDatabaseSeeder extends Seeder
{
    public function run()
    {
        // Create test users
        User::factory(10)->create();
        
        // Create test santri
        Santri::factory(50)->create();
        
        // Create test ustadz
        Ustadz::factory(5)->create();
        
        // Create test classes
        Kelas::factory(8)->create();
    }
}
```

### Factory Patterns
```php
// SantriFactory.php
class SantriFactory extends Factory
{
    public function definition()
    {
        return [
            'nis' => $this->faker->unique()->numerify('######'),
            'nama_lengkap' => $this->faker->name(),
            'jenis_kelamin' => $this->faker->randomElement(['L', 'P']),
            'tanggal_lahir' => $this->faker->date(),
            'alamat' => $this->faker->address(),
        ];
    }
}
```

## 🔄 Continuous Integration

### GitHub Actions Workflow
```yaml
name: Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup PHP
        uses: shivammathur/setup-php@v2
        with:
          php-version: 8.0
      - name: Install dependencies
        run: composer install
      - name: Run tests
        run: ./vendor/bin/phpunit
```

## 📈 Test Metrics

### Coverage Goals
- **Unit Tests**: 90%+ coverage
- **Feature Tests**: 80%+ coverage
- **Critical Paths**: 100% coverage

### Performance Benchmarks
- API response time < 200ms
- Database queries < 50ms
- Page load time < 2s

---

**Note**: Test suite akan dikembangkan parallel dengan development features.
