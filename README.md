# 🐳 Docker-Laravel

A lightweight and fast Docker environment to run multiple **Laravel/PHP** applications with **Nginx** and **MySQL**.

This setup is designed for both modern and legacy Laravel projects, providing a simple, reusable, and stable environment.

---

## 🚀 Stack

| Service | Version | Container |
|----------|----------|------------|
| PHP | 7.0 (FPM Alpine) | `php` |
| Nginx | Stable Alpine | `nginx` |
| MySQL | 5.7.22 | `mysql` |
| Composer | Latest | Included in PHP container |

---

## 📁 Directory Structure

```.
docker-laravel/
├── DockerFile
├── docker-compose.yml
├── nginx/
│ └── default.conf
├── php/
│ └── custom.ini
├── mysql/
│ └── (persistent database files)
└── src/
└── (your PHP/Laravel project here)
```

## ⚙️ Setup

### 1️⃣ Build and start containers

```bash
docker compose build
docker compose up -d
```

This will create and start the PHP, MySQL, and Nginx containers.

### 2️⃣ Database configuration
A database named **laravel** is automatically created with the following credentials:

| Parameter     | Value     |
| ------------- | --------- |
| Host          | `mysql`   |
| Database      | `laravel` |
| User          | `laravel` |
| Password      | `root`    |
| Root Password | `root`    |

### 3️⃣ Running Artisan commands

You can execute Artisan commands directly inside the PHP container:

```
docker-compose exec -w /var/www/html/project-name php php artisan key:generate
docker-compose exec -w /var/www/html/project-name php php artisan migrate
```

### 4️⃣ Serving the application

Clone or copy your Laravel project inside the /src directory and run:


```
docker-compose exec -w /var/www/html/project-name php php artisan serve --host=0.0.0.0 --port=8000
```

Your application will be available at:

👉 http://localhost:8000/

### 5️⃣ Fixing storage permissions (if needed)

If you encounter permission issues, run:

```
docker-compose exec -w /var/www/html/project-name php chmod -R o+w storage
```

## 🧹 Stopping containers

To stop and remove all containers:

```
docker compose down
```


## 🧠 Notes
Composer is already installed inside the PHP container.

MySQL data is persisted via a mounted volume.

You can use this same Docker setup for multiple Laravel projects — just add each one as a subfolder under /src/.

Designed for Laravel 5.x and older PHP versions but can be easily extended for newer stacks.

---

Built with ❤️ to simplify and accelerate development of legacy Laravel projects — where Sail isn’t available or suitable.