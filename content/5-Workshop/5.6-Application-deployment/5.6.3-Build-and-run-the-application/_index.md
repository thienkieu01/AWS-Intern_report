---
title : "Build and Run the Application"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.6.3 </b> "
---

After Docker is installed and `.env` is configured, the final step is to fix the `docker-compose.yml` configuration, build the container, and initialize the application's data.

#### Step 1: Fix `DJANGO_SETTINGS_MODULE` in `docker-compose.yml`

Open the `docker/docker-compose.yml` file:

```bash
nano docker/docker-compose.yml
```

Find the `DJANGO_SETTINGS_MODULE` line and make sure it points to `production` instead of `local`:

```yaml
environment:
  DJANGO_SETTINGS_MODULE: config.settings.production
```

{{% notice warning %}}
If left as `config.settings.local`, the application will not read the correct S3 configuration, and book cover images will fail to upload — this is a real error encountered during deployment.
{{% /notice %}}

#### Step 2: Build and Run the Container

```bash
docker compose -f docker/docker-compose.yml up -d --build
```

This command both builds the image and runs the container in the background (`-d`).

Check that the container is running:

```bash
docker compose -f docker/docker-compose.yml ps
```

To view logs for debugging:

```bash
docker compose -f docker/docker-compose.yml logs -f
```

Press `Ctrl+C` to exit log-following mode.

#### Step 3: Create Migrations, Migrate the Database, Create a Superuser, and Import Data

1. Create migrations:

```bash
docker compose -f docker/docker-compose.yml exec web python manage.py makemigrations
```

2. Migrate the database:

```bash
docker compose -f docker/docker-compose.yml exec web python manage.py migrate
```

3. Create a superuser:

```bash
docker compose -f docker/docker-compose.yml exec web python manage.py createsuperuser
```

4. Import sample data (flushing old data before importing):

```bash
docker compose -f docker/docker-compose.yml exec web python manage.py import_legacy_csv --flush
```

{{% notice note %}}
Make sure to run these commands after `DJANGO_SETTINGS_MODULE` has been switched to `production` — if run while still on `local`, the superuser/data will be created on a different database (the Docker volume), not the real RDS instance.
{{% /notice %}}

#### Step 4: Fixing the `ERR_SSL_PROTOCOL_ERROR` Error

If accessing via `http://` causes the browser to automatically redirect to `https://` and show an SSL error, the cause is `SECURE_SSL_REDIRECT=True` in `production.py` forcing HTTPS while EC2 doesn't yet have an SSL certificate.

Open the production settings file:

```bash
nano config/settings/production.py
```

Find and change the following lines to `False` / `0`:

```python
SECURE_SSL_REDIRECT = False
SESSION_COOKIE_SECURE = False
CSRF_COOKIE_SECURE = False
SECURE_HSTS_SECONDS = 0
```

Rebuild the container to apply the changes:

```bash
docker compose -f docker/docker-compose.yml up -d --build
```

{{% notice warning %}}
If the browser was previously redirected to HTTPS, you'll need to clear the HSTS cache: open `chrome://net-internals/#hsts`, enter the domain/IP in the "Delete domain security policies" field and delete it, then try again.
{{% /notice %}}

#### Step 5: Access the Application

Open your browser and go to:

```
http://54.82.167.72:8000
```

If you see the Library Management System login screen, the deployment was successful.