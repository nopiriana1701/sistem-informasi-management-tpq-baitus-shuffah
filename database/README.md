# Database Directory

Folder ini berisi semua file terkait database untuk aplikasi TPQ Baitus Shuffah.

## 📁 Struktur Database

```
database/
├── migrations/          # Database schema migrations
├── seeders/            # Data seeding files
├── factories/          # Model factories untuk testing
├── sql/               # Raw SQL files
└── backups/           # Database backup files
```

## 🔄 Migrations

### Struktur Migration Files
```
migrations/
├── 2025_01_01_000001_create_users_table.php
├── 2025_01_01_000002_create_wali_santri_table.php
├── 2025_01_01_000003_create_ustadz_table.php
├── 2025_01_01_000004_create_santri_table.php
├── 2025_01_01_000005_create_kelas_table.php
├── 2025_01_01_000006_create_jadwal_table.php
├── 2025_01_01_000007_create_materi_table.php
├── 2025_01_01_000008_create_absensi_table.php
├── 2025_01_01_000009_create_nilai_table.php
├── 2025_01_01_000010_create_jenis_pembayaran_table.php
└── 2025_01_01_000011_create_pembayaran_table.php
```

### Contoh Migration File
```php
<?php
// 2025_01_01_000004_create_santri_table.php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    public function up()
    {
        Schema::create('santri', function (Blueprint $table) {
            $table->id();
            $table->foreignId('user_id')->nullable()->constrained()->onDelete('set null');
            $table->string('nis', 20)->unique();
            $table->string('nama_lengkap', 100);
            $table->string('nama_panggilan', 50)->nullable();
            $table->enum('jenis_kelamin', ['L', 'P']);
            $table->string('tempat_lahir', 50)->nullable();
            $table->date('tanggal_lahir')->nullable();
            $table->text('alamat')->nullable();
            $table->string('no_hp', 15)->nullable();
            $table->foreignId('kelas_id')->nullable()->constrained()->onDelete('set null');
            $table->foreignId('wali_santri_id')->nullable()->constrained()->onDelete('set null');
            $table->date('tanggal_masuk');
            $table->enum('status', ['aktif', 'nonaktif', 'lulus', 'pindah'])->default('aktif');
            $table->string('foto')->nullable();
            $table->timestamps();
            
            $table->index(['kelas_id', 'status']);
            $table->index('wali_santri_id');
        });
    }

    public function down()
    {
        Schema::dropIfExists('santri');
    }
};
```

## 🌱 Seeders

### Database Seeder Structure
```
seeders/
├── DatabaseSeeder.php           # Main seeder
├── UserSeeder.php              # Users data
├── UstadzSeeder.php            # Ustadz data
├── WaliSantriSeeder.php        # Wali santri data
├── SantriSeeder.php            # Santri data
├── KelasSeeder.php             # Kelas data
├── MateriSeeder.php            # Materi pembelajaran
├── JenisPembayaranSeeder.php   # Jenis pembayaran
└── DemoDataSeeder.php          # Demo data untuk testing
```

### Contoh Seeder File
```php
<?php
// SantriSeeder.php
namespace Database\Seeders;

use Illuminate\Database\Seeder;
use App\Models\Santri;
use App\Models\User;
use App\Models\Kelas;
use App\Models\WaliSantri;

class SantriSeeder extends Seeder
{
    public function run()
    {
        $kelas = Kelas::all();
        $waliSantri = WaliSantri::all();
        
        // Create sample santri data
        $santriData = [
            [
                'nis' => '001001',
                'nama_lengkap' => 'Ahmad Fauzi',
                'nama_panggilan' => 'Ahmad',
                'jenis_kelamin' => 'L',
                'tempat_lahir' => 'Jakarta',
                'tanggal_lahir' => '2015-05-15',
                'alamat' => 'Jl. Masjid No. 123, Jakarta',
                'no_hp' => '081234567890',
                'tanggal_masuk' => '2025-01-01',
                'status' => 'aktif',
            ],
            // Add more sample data...
        ];

        foreach ($santriData as $data) {
            // Create user account for santri
            $user = User::create([
                'username' => strtolower(str_replace(' ', '', $data['nama_lengkap'])),
                'email' => strtolower(str_replace(' ', '', $data['nama_lengkap'])) . '@tpq.com',
                'password' => bcrypt('password123'),
                'role' => 'santri',
            ]);

            // Create santri record
            Santri::create(array_merge($data, [
                'user_id' => $user->id,
                'kelas_id' => $kelas->random()->id,
                'wali_santri_id' => $waliSantri->random()->id,
            ]));
        }
    }
}
```

## 🏭 Factories

### Model Factory Structure
```
factories/
├── UserFactory.php
├── SantriFactory.php
├── UstadzFactory.php
├── WaliSantriFactory.php
├── KelasFactory.php
├── AbsensiFactory.php
├── NilaiFactory.php
└── PembayaranFactory.php
```

### Contoh Factory File
```php
<?php
// SantriFactory.php
namespace Database\Factories;

use Illuminate\Database\Eloquent\Factories\Factory;
use App\Models\Santri;
use App\Models\User;
use App\Models\Kelas;
use App\Models\WaliSantri;

class SantriFactory extends Factory
{
    protected $model = Santri::class;

    public function definition()
    {
        return [
            'user_id' => User::factory(),
            'nis' => $this->faker->unique()->numerify('######'),
            'nama_lengkap' => $this->faker->name(),
            'nama_panggilan' => $this->faker->firstName(),
            'jenis_kelamin' => $this->faker->randomElement(['L', 'P']),
            'tempat_lahir' => $this->faker->city(),
            'tanggal_lahir' => $this->faker->dateTimeBetween('-12 years', '-5 years')->format('Y-m-d'),
            'alamat' => $this->faker->address(),
            'no_hp' => $this->faker->phoneNumber(),
            'kelas_id' => Kelas::factory(),
            'wali_santri_id' => WaliSantri::factory(),
            'tanggal_masuk' => $this->faker->dateTimeBetween('-2 years', 'now')->format('Y-m-d'),
            'status' => $this->faker->randomElement(['aktif', 'nonaktif']),
        ];
    }

    public function aktif()
    {
        return $this->state(function (array $attributes) {
            return [
                'status' => 'aktif',
            ];
        });
    }
}
```

## 📄 SQL Files

### Raw SQL Structure
```
sql/
├── initial_setup.sql       # Initial database setup
├── views.sql              # Database views
├── stored_procedures.sql   # Stored procedures
├── triggers.sql           # Database triggers
└── indexes.sql            # Additional indexes
```

### Contoh SQL File
```sql
-- views.sql
-- View untuk laporan santri per kelas
CREATE VIEW v_santri_per_kelas AS
SELECT 
    k.id as kelas_id,
    k.nama_kelas,
    k.tingkat,
    u.nama_lengkap as nama_ustadz,
    COUNT(s.id) as jumlah_santri,
    k.kapasitas_maksimal,
    ROUND((COUNT(s.id) / k.kapasitas_maksimal) * 100, 2) as persentase_terisi
FROM kelas k
LEFT JOIN santri s ON k.id = s.kelas_id AND s.status = 'aktif'
LEFT JOIN ustadz u ON k.ustadz_id = u.id
WHERE k.status = 'aktif'
GROUP BY k.id, k.nama_kelas, k.tingkat, u.nama_lengkap, k.kapasitas_maksimal;

-- View untuk laporan pembayaran bulanan
CREATE VIEW v_laporan_pembayaran AS
SELECT 
    s.id as santri_id,
    s.nama_lengkap as nama_santri,
    s.nis,
    k.nama_kelas,
    jp.nama_pembayaran,
    p.periode_pembayaran,
    p.nominal,
    p.status as status_pembayaran,
    p.tanggal_pembayaran,
    CASE 
        WHEN p.status = 'lunas' THEN 'Lunas'
        WHEN p.tanggal_pembayaran < CURDATE() THEN 'Terlambat'
        ELSE 'Pending'
    END as keterangan_status
FROM santri s
LEFT JOIN kelas k ON s.kelas_id = k.id
LEFT JOIN pembayaran p ON s.id = p.santri_id
LEFT JOIN jenis_pembayaran jp ON p.jenis_pembayaran_id = jp.id
WHERE s.status = 'aktif';
```

## 💾 Backup Strategy

### Backup Structure
```
backups/
├── daily/              # Daily backups
├── weekly/             # Weekly backups
├── monthly/            # Monthly backups
└── manual/             # Manual backups
```

### Backup Script Example
```bash
#!/bin/bash
# backup_database.sh

DB_NAME="tpq_baitus_shuffah"
DB_USER="root"
DB_PASS="password"
BACKUP_DIR="/path/to/backups"
DATE=$(date +%Y%m%d_%H%M%S)

# Create backup
mysqldump -u $DB_USER -p$DB_PASS $DB_NAME > $BACKUP_DIR/daily/backup_$DATE.sql

# Compress backup
gzip $BACKUP_DIR/daily/backup_$DATE.sql

# Remove backups older than 30 days
find $BACKUP_DIR/daily -name "*.sql.gz" -mtime +30 -delete

echo "Backup completed: backup_$DATE.sql.gz"
```

## 🔧 Database Commands

### Migration Commands
```bash
# Create new migration
php artisan make:migration create_table_name

# Run migrations
php artisan migrate

# Rollback migrations
php artisan migrate:rollback

# Reset and re-run all migrations
php artisan migrate:fresh

# Check migration status
php artisan migrate:status
```

### Seeder Commands
```bash
# Create new seeder
php artisan make:seeder TableNameSeeder

# Run all seeders
php artisan db:seed

# Run specific seeder
php artisan db:seed --class=SantriSeeder

# Fresh migration with seeding
php artisan migrate:fresh --seed
```

### Factory Commands
```bash
# Create new factory
php artisan make:factory ModelNameFactory

# Use factory in tinker
php artisan tinker
>>> Santri::factory(10)->create()
```

---

**Note**: Database structure akan dikembangkan sesuai dengan kebutuhan fitur yang diimplementasi.
