# Beyond The Pool — Django (Dockerized)

A Django 5.x application containerized with **Docker** and **Docker Compose**.  
This project powers a swimming-pool page that includes an embedded **3D model** (e.g., GLTF/GLB) rendered in the browser.

---

## ✨ Features

- **Django** backend running on Python 3.11 (slim image).
- **Internationalization**: `gettext` installed; messages compiled on build and on container start.
- **Database migrations** executed automatically on start.
- **Hot reloading** in development via a bind mount (`.:/app`) and Django dev server.
- **Static files** persisted to a named Docker volume (`static_volume`).
- **3D model** support via `<model-viewer>` (GLTF/GLB) or your choice of viewer.

---

## 🧱 Stack

- Python 3.11 (Debian slim)
- Django 5.x (`DJANGO_SETTINGS_MODULE=basen.settings`)
- Docker & Docker Compose v2
- gettext (for i18n)
- Optional: PostgreSQL client libs preinstalled (`libpq-dev`) for psycopg2 if you add Postgres later

---

## 🗂️ Repository Layout (excerpt)

```
.
├─ basen/                     # Your Django project (settings, urls, wsgi/asgi)
├─ app_or_apps/               # Django apps
├─ static/                    # Collected static (mounted to a volume in Compose)
│  └─ models/                 # Place .gltf/.glb here (e.g., pool.gltf)
├─ templates/                 # Django templates (uses {% static %} for assets)
├─ locale/                    # i18n .po/.mo files
├─ requirements.txt
├─ Dockerfile
├─ docker-compose.yml
└─ README.md
```

> The Compose file also mounts the **entire project directory** into the container, so changes on your host reflect immediately in the running server.

---

## 🚀 Quick Start (with Docker Compose)

Prerequisites: **Docker Desktop** (or Docker Engine) and **Docker Compose**.

```bash
# 1) Build the image
docker compose build

# 2) Start the app
docker compose up
```

Visit: **http://localhost:8000**  
Admin (if enabled): **http://localhost:8000/admin**

On first run, the container will:
- compile translation messages,
- apply migrations,
- start the Django dev server at `0.0.0.0:8000`.

Stop the stack with `Ctrl+C`, or run in the background:
```bash
docker compose up -d
```
