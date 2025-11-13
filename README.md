# Vidocu Clip

A Laravel-based video clip management application.

## Tech Stack

- Laravel 12.38.1
- PHP 8.3+
- MySQL 8.0
- Nginx
- Vite + Tailwind CSS

## Prerequisites

- Docker & Docker Compose
- Node.js & npm (for local development)
- Composer (for local development)

## Installation

### 1. Clone the repository

```bash
git clone <repository-url>
cd vidocu-clip
```

### 2. Setup environment

```bash
cp .env.example .env
```

### 3. Install dependencies (Optional - for local development)

```bash
composer install
npm install
```

### 4. Generate application key

```bash
php artisan key:generate
```

## Running the Application

### Using Docker (Recommended)

```bash
# Start all services
docker-compose up -d

# Stop all services
docker-compose down

# View logs
docker-compose logs -f

# Rebuild containers
docker-compose up -d --build
```

### Using Local Development Server

```bash
# Terminal 1 - Start Laravel development server
php artisan serve --port=8095

# Terminal 2 - Start Vite development server
npm run dev
```

## Access Points

- **Web Application**: http://localhost:8095
- **phpMyAdmin**: http://localhost:8096
- **Vite HMR**: http://localhost:5174

## Database Configuration

### Docker MySQL
- Host: localhost
- Port: 3310
- Database: vidocu_clip
- Username: vidocu_clip
- Password: vidocu_clip
- Root Password: root

### Local SQLite (Default)
The application uses SQLite by default. Database file is located at `database/database.sqlite`

## Docker Services

- `vidocu_clip_app` - PHP-FPM application container
- `vidocu_clip_web` - Nginx web server
- `vidocu_clip_db` - MySQL database
- `vidocu_clip_phpmyadmin` - phpMyAdmin interface

## Common Commands

### Docker

```bash
# Execute artisan commands
docker-compose exec app php artisan <command>

# Run migrations
docker-compose exec app php artisan migrate

# Clear cache
docker-compose exec app php artisan cache:clear

# Access application container
docker-compose exec app bash

# Access database container
docker-compose exec db mysql -u vidocu_clip -p
```

### Local

```bash
# Run migrations
php artisan migrate

# Seed database
php artisan db:seed

# Clear cache
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan view:clear

# Run tests
php artisan test
```

## Development

### Frontend Assets

```bash
# Development with hot reload
npm run dev

# Build for production
npm run build

# Watch mode
npm run watch
```

### Code Quality

```bash
# Run Laravel Pint (code formatting)
./vendor/bin/pint

# Run tests
php artisan test

# Run tests with coverage
php artisan test --coverage
```

## Troubleshooting

### Port conflicts

If you encounter port conflicts, modify the ports in `docker-compose.yml` and `.env`:

- Web: Change `8095:80` to another port
- MySQL: Change `3310:3306` to another port
- phpMyAdmin: Change `8096:80` to another port
- Vite: Change port in `vite.config.js`

### Permission issues (Docker)

```bash
# Fix storage and cache permissions
docker-compose exec app chmod -R 775 storage bootstrap/cache
docker-compose exec app chown -R www-data:www-data storage bootstrap/cache
```

### Database connection issues

```bash
# Wait for MySQL to be ready
docker-compose exec db mysqladmin ping -h localhost -u root -proot

# Recreate database
docker-compose exec app php artisan migrate:fresh
```

## License

This project is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
