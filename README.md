# Docker + Caddy Example

## Overview
This repository demonstrates how to proxy one or more Docker‑based applications with [Caddy](https://caddyserver.com/). It contains:

- **`caddy/`** – Caddy reverse‑proxy configuration.
- **`docker-compose.yml`** *(root)* – brings up the Caddy container.
- **`example-for-laravel/`**  
  - **`Dockerfile`** – builds a PHP‑FPM image for a Laravel application.  
  - **`docker-compose.yml`** – services required by the Laravel app (PHP‑FPM, Nginx, database, etc.).

> **Tip** Install Docker **before** you start—everything else runs inside containers.

---

## Prerequisites
- Docker Engine ≥ 24
- Docker Compose v2 (the `docker compose` CLI plugin)

---

## Quick Start
```bash
# 1 Clone the repo
$ git clone https://github.com/your‑org/your‑repo.git
$ cd your‑repo

# 2 Start the Caddy reverse proxy (root directory)
$ docker compose up -d caddy

# 3 Build & start the Laravel stack
$ cd example-for-laravel
$ docker compose up -d --build
```
Caddy will automatically obtain TLS certificates and proxy traffic to the Laravel application as soon as its container reports healthy.

---

## Directory Layout
```
.
├── caddy/
│   └── Caddyfile          # Reverse‑proxy rules
├── docker-compose.yml     # Caddy service definition
└── example-for-laravel/
    ├── Dockerfile         # PHP‑FPM & Composer
    ├── docker-compose.yml # Laravel app, Nginx, DB
```

---

## Customisation
- **Domains & routing** – edit `caddy/Caddyfile`.
- **Additional services** – tweak `example-for-laravel/docker-compose.yml` (e.g. Redis, MailHog).
- **Environment variables** – live in `.env` files next to each compose file.

---

## Stopping & Cleanup
```bash
# Stop Caddy (root)
$ docker compose down

# Stop the Laravel stack
$ cd example-for-laravel
$ docker compose down
```

---

## Troubleshooting
| What to check | Command / Note |
|---------------|----------------|
| Container logs | `docker compose logs -f <service>` |
| Port conflicts | Ensure ports **80** & **443** are free for Caddy |
| Health status  | `docker compose ps` shows `healthy` for app services |

---

Good luck
