# Dockerized PHP Development Environment (LEMP Stack)

This project provides an instant web development environment using Docker with the LEMP stack (Linux, Nginx, MySQL, PHP 8.2), including phpMyAdmin for easy database management.

## 📂 Project Structure
```
├── docker-compose.yaml     # Orchestrates 4 services (Nginx, PHP, MySQL, phpMyAdmin)
├── Dockerfile             # Custom PHP 8.2 image with mysqli & PDO extensions
├── .gitignore            # Ignores src/, mysql/, nginx/ folders
├── nginx/                 # Nginx server configuration
│   └── default.conf
└── src/                   # Your PHP application code
    └── index.php
```

## 🚀 Prerequisites
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/install/) (included with Docker Desktop)

## 🛠️ Setup Instructions

1. **Create project folders** (`src/` and `nginx/` are ignored by `.gitignore`):
   ```bash
   mkdir -p src nginx
   ```

2. **Create test PHP file** (`src/index.php`):
   ```php
   <?php phpinfo(); ?>
   ```

3. **Create Nginx configuration** (`nginx/default.conf`):
   ```nginx
   server {
    listen 80;
    server_name localhost;
    root /var/www/html;

    index index.php index.html;

    autoindex on;              
    autoindex_exact_size off;
    autoindex_localtime on;   

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass php:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
   ```

4. **Start containers**:
   ```bash
   docker-compose up -d --build
   ```

## 🌐 Service Access
| Service     | URL                    | Description                  |
|-------------|------------------------|------------------------------|
| PHP Website | http://localhost       | Displays `src/index.php`     |
| phpMyAdmin  | http://localhost:8082  | Database management          |

## 🔐 Database Credentials
| Parameter     | Value          |
|---------------|----------------|
| **Host**      | `mysql` (not `localhost`) |
| **Database**  | `app_db`       |
| **User**      | `app_user`     |
| **Password**  | `secret`       |
| **Root Password** | `root`     |

**PDO Connection Example**:
```php
$host = 'mysql';
$db   = 'app_db';
$user = 'app_user';
$pass = 'secret';
$charset = 'utf8mb4';

$dsn = "mysql:host=$host;dbname=$db;charset=$charset";
$pdo = new PDO($dsn, $user, $pass);
```

## ⚙️ Docker Compose Commands
```bash
# Start (detached + rebuild)
docker-compose up -d --build

# Stop services
docker-compose down

# Stop + remove volumes
docker-compose down -v

# View logs
docker-compose logs -f

# Restart services
docker-compose restart
```

## 🐛 Troubleshooting
- **PHP can't connect to MySQL**: Use `mysql` as hostname in PHP code (not `localhost`)
- **Permission denied**: Run `chmod -R 755 src/`
- **Containers won't start**: Clean old images with `docker-compose down --rmi all`

## 🤝 Contributing
1. Fork this repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

## 📄 License
This project is licensed under the [MIT License](LICENSE).

***