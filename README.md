<p align="center">
    <a href="https://krayincrm.com">
        <picture>
            <source media="(prefers-color-scheme: dark)" height="100" srcset="packages/Webkul/Admin/src/Resources/assets/images/dark-logo.svg">
            <source media="(prefers-color-scheme: light)" height="100" srcset="packages/Webkul/Admin/src/Resources/assets/images/logo.svg">
            <img alt="Krayin CRM" height="100" src="packages/Webkul/Admin/src/Resources/assets/images/logo.svg">
        </picture>
    </a>
</p>

<p align="center">
<a href="https://packagist.org/packages/krayin/laravel-crm"><img src="https://poser.pugx.org/krayin/laravel-crm/d/total.svg" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/krayin/laravel-crm"><img src="https://poser.pugx.org/krayin/laravel-crm/v/stable.svg" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/krayin/laravel-crm"><img src="https://poser.pugx.org/krayin/laravel-crm/license.svg" alt="License"></a>
</p>


![enter image description here](https://raw.githubusercontent.com/krayin/temp-media/master/dashboard.png)

## Topics

1. [Introduction](#introduction)
2. [Documentation](#documentation)
3. [Docker Local Development (Recommended)](#docker-local-development-recommended)
4. [Native Requirements & Installation](#native-requirements--installation)
5. [Krayin Cloud System](#krayin-cloud-hosting)
6. [License](#license)
7. [Security Vulnerabilities](#security-vulnerabilities)

### Introduction

[Krayin CRM](https://krayincrm.com) is a hand tailored CRM framework built on some of the hottest opensource technologies
such as [Laravel](https://laravel.com) (a [PHP](https://secure.php.net/) framework) and [Vue.js](https://vuejs.org)
a progressive Javascript framework.

**Free & Opensource Laravel CRM solution for SMEs and Enterprises for complete customer lifecycle management.**

**Read our documentation: [Krayin CRM Docs](https://devdocs.krayincrm.com/)**

**We also have a forum for any type of concerns, feature requests, or discussions. Please visit: [Krayin CRM Forums](https://forums.krayincrm.com/)**

# Visit our live [Demo](https://demo.krayincrm.com)

<a href="javascript:void();">
    <img class="flag-img" src="https://raw.githubusercontent.com/krayin/temp-media/master/visit-our-live-demo.png" alt="Chinese" width="100%">
</a>

It packs in lots of features that will allow your E-Commerce business to scale in no time:

-   Descriptive and Simple Admin Panel.
-   Admin Dashboard.
-   Custom Attributes.
-   Built on Modular Approach.
-   Email parsing via Sendgrid.
-   Check out [these features and more](https://krayincrm.com/features/).

**For Developers**:
Take advantage of two of the hottest frameworks used in this project -- Laravel and Vue.js -- both of which have been used in Krayin CRM.

### Documentation

#### Krayin Documentation [https://devdocs.krayincrm.com](https://devdocs.krayincrm.com)

---

### Docker Local Development (Recommended)

Lingkungan pengembangan lokal proyek ini telah dikontainerisasi menggunakan **Docker** dan **Docker Compose** untuk menjamin konsistensi environment PHP 8.3, ekstensi lengkap, database MySQL 8.0, dan mail testing tanpa dependensi pada OS host.

#### 1. Arsitektur Container
- **`app` (`krayin-app`)**: PHP 8.3 FPM (Debian Bookworm) dengan ekstensi `calendar`, `pdo_mysql`, `mbstring`, `exif`, `pcntl`, `bcmath`, `gd`, `intl`, `zip`, `imap`, `opcache`, serta Composer 2 & Node.js 20 LTS.
- **`webserver` (`krayin-webserver`)**: Nginx Alpine (`port 8081:80`).
- **`db` (`krayin-db`)**: MySQL 8.0 (`port 3307:3306`, persistent volume `krayin-db-data`).
- **`mailpit` (`krayin-mailpit`)**: Mock SMTP & Web UI Mailpit (`port 1025` SMTP, `port 8025` Web UI).

#### 2. Panduan Menjalankan Proyek (Step-by-Step)

##### Langkah 1: Siapkan Environment
Salin file environment jika belum ada (atau sesuaikan file `.env` yang sudah disiapkan untuk Docker):
```bash
cp .env.example .env
```
> Pastikan variabel database di `.env` mengarah ke container:
> `DB_CONNECTION=mysql`, `DB_HOST=db`, `DB_PORT=3306`, `DB_DATABASE=laravel-crm`, `DB_USERNAME=krayin`, `DB_PASSWORD=123456`, dan `APP_URL=http://localhost:8081`.

##### Langkah 2: Build & Jalankan Container
```bash
docker compose up -d --build
```

##### Langkah 3: Install Dependensi PHP
```bash
docker compose exec app composer install
```

##### Langkah 4: Inisialisasi Krayin CRM (Key, Migrasi, Seeder, dan Admin)
```bash
docker compose exec app php artisan krayin-crm:install --skip-env-check
```

##### Langkah 5: Install & Build Frontend Assets (Vite)
```bash
docker compose exec app npm install
docker compose exec app npm run build
```

#### 3. URL Akses Layanan Lokal
- **Admin Panel Krayin CRM:** [http://localhost:8081/admin/login](http://localhost:8081/admin/login)
  - Default / created admin credentials sesuai prompt saat instalasi.
- **Mailpit Web UI (Email Testing):** [http://localhost:8025](http://localhost:8025)
- **Database MySQL (Akses GUI dari Host):** `127.0.0.1:3307`
  - User: `krayin` | Password: `123456` | Database: `laravel-crm`

#### 4. Perintah Harian yang Sering Digunakan
- **Vite Hot-Reloading (Frontend Dev):**
  ```bash
  docker compose exec app npm run dev
  ```
- **Menjalankan Artisan Command:**
  ```bash
  docker compose exec app php artisan <perintah>
  ```
- **Menghentikan / Menyalakan Container:**
  ```bash
  docker compose stop
  docker compose start
  ```

---

### Native Requirements & Installation

Gunakan instruksi ini hanya jika kamu tidak ingin menggunakan Docker dan memilih menjalankan langsung di OS host:

-   **SERVER**: Apache 2 or NGINX.
-   **RAM**: 3 GB or higher.
-   **PHP**: 8.3 or higher (ekstensi: calendar, ctype, curl, dom, fileinfo, filter, gd, hash, intl, json, mbstring, openssl, pcre, pdo, session, tokenizer, xml, imap, zip).
-   **Composer**: 2.5 or higher.
-   **For MySQL users**: 8.0.32 or higher.
-   **For MariaDB users**: 11.4 LTS or higher (11.8 LTS recommended).

##### Execute these commands below, in order:
```bash
composer install
php artisan key:generate
php artisan krayin-crm:install
npm install
npm run build
php artisan serve
```

### Krayin Cloud Hosting

[Krayin CRM Cloud Hosting](https://krayincrm.com/crm-cloud-hosting) is a fully managed hosting solution where our team sets up, secures, and configures your Krayin CRM on reliable infrastructure.

Get a ready-to-use CRM on your own domain, without manual installation or infrastructure complexity, and focus on growing your business while we handle the technology.

![Krayin CRM Cloud Hosting](https://raw.githubusercontent.com/krayin/temp-media/master/cloud_hosting.png)

### Krayin CRM Multi Tenant SaaS

[Krayin CRM Multi Tenant SaaS](https://krayincrm.com/extensions/krayin-crm-multi-tenant-saas-extension/) Krayin Multitenant SaaS is a Laravel-based CRM solution that allows multiple businesses (tenants) to use a single application instance while keeping their data isolated and secure.

![enter image description here](https://raw.githubusercontent.com/krayin/temp-media/master/krayin-saas.png)

### WhatsApp CRM Integration

[Krayin CRM WhatsApp](https://krayincrm.com/extensions/krayin-crm-whatsapp-extension/) Extension enables the store administrator to generate leads via their WhatsApp number.

![enter image description here](https://raw.githubusercontent.com/krayin/temp-media/master/krayin-crm-whatsapp-integration.png)

### VoIP CRM Integration

[Krayin CRM VoIP](https://krayincrm.com/extensions/krayin-crm-voip/) extension allows the user to make Trunk calls over a broadband Internet connection and the user can also perform Inbound routes.

![enter image description here](https://raw.githubusercontent.com/krayin/temp-media/master/krayin-voip.png)

### License

Krayin CRM is a fully open-source CRM framework which will always be free under the [MIT License](https://github.com/krayin/laravel-crm/blob/2.1/LICENSE).

### Security Vulnerabilities

Please don't disclose security vulnerabilities publicly. If you find any security vulnerability in Krayin CRM then please email us: sales@krayincrm.com.
