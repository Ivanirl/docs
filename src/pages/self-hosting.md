---
title: Self Hosting Plane
pageTitle: Self Hosting | Plane
description: This section helps you get comfortable with Plane and find your way around more effectively.
---

Plane is still in its early days, not everything is perfect yet, and
hiccups may happen. Please let us know of any suggestions, ideas, or bugs that
you encounter on our [Discord](https://discord.com/invite/A92xrEGCge).

This guide assumes you already have Docker installed
and have permissions to run Docker containers.
See the [Install on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
guide which explains installing Docker on your machine.

## Install with Docker Compose (recommended way)

### Clone the Repository and change the directory

```bash
git clone --depth 1 -b master https://github.com/makeplane/plane.git && cd plane
```

### Run setup.sh

This script sets up the environment with the IP address or the Domain name you provided.

```bash
./setup.sh http://<your_ip|domain_name>
```

{% callout type="note" %}
`<your_ip>` is a placeholder for the actual IP address
that you'd want your Plane instance to be available on.

If you are setting Plane up, for example, on your own PC,
it is recommended to use `localhost` for the IP address.
{% /callout %}

### Environment Variables
```bash
# Frontend
# Extra image domains that need to be added for Next Image
NEXT_PUBLIC_EXTRA_IMAGE_DOMAINS=
# Google Client ID for Google OAuth
NEXT_PUBLIC_GOOGLE_CLIENTID=""
# Github ID for Github OAuth
NEXT_PUBLIC_GITHUB_ID=""
# Github App Name for GitHub Integration
NEXT_PUBLIC_GITHUB_APP_NAME=""
# Sentry DSN for error monitoring
NEXT_PUBLIC_SENTRY_DSN=""
# Enable/Disable OAUTH - default 0 for selfhosted instance 
NEXT_PUBLIC_ENABLE_OAUTH=0
# Enable/Disable sentry
NEXT_PUBLIC_ENABLE_SENTRY=0
# Enable/Disable session recording 
NEXT_PUBLIC_ENABLE_SESSION_RECORDER=0
# Enable/Disable event tracking
NEXT_PUBLIC_TRACK_EVENTS=0
# Slack for Slack Integration
NEXT_PUBLIC_SLACK_CLIENT_ID=""

# Backend
# Debug value for api server use it as 0 for production use
DEBUG=0

# Error logs
SENTRY_DSN=""

# Database Settings
PGUSER="plane"
PGPASSWORD="plane"
PGHOST="plane-db"
PGDATABASE="plane"
DATABASE_URL=postgresql://${PGUSER}:${PGPASSWORD}@${PGHOST}/${PGDATABASE}

# Redis Settings
REDIS_HOST="plane-redis"
REDIS_PORT="6379"
REDIS_URL="redis://${REDIS_HOST}:6379/"

# Email Settings
EMAIL_HOST=""
EMAIL_HOST_USER=""
EMAIL_HOST_PASSWORD=""
EMAIL_PORT=587
EMAIL_FROM="Team Plane <team@mailer.plane.so>"
EMAIL_USE_TLS="1"
EMAIL_USE_SSL="0"

# AWS Settings
AWS_REGION=""
AWS_ACCESS_KEY_ID="access-key"
AWS_SECRET_ACCESS_KEY="secret-key"
AWS_S3_ENDPOINT_URL="http://plane-minio:9000"
# Changing this requires change in the nginx.conf for uploads if using minio setup
AWS_S3_BUCKET_NAME="uploads"
# Maximum file upload limit
FILE_SIZE_LIMIT=5242880

# GPT settings
OPENAI_API_KEY=""
GPT_ENGINE=""

# Github
GITHUB_CLIENT_SECRET="" # For fetching release notes

# Settings related to Docker
DOCKERIZED=1
# set to 1 If using the pre-configured minio setup 
USE_MINIO=1

# Nginx Configuration
NGINX_PORT=80

# Default Creds
DEFAULT_EMAIL="captain@plane.so"
DEFAULT_PASSWORD="password123"

# SignUps
ENABLE_SIGNUP="1"
# Auto generated and Required that will be generated from setup.sh
NEXT_PUBLIC_API_BASE_URL=http://<your_ip|domain_name>
SECRET_KEY="<redacted>"
WEB_URL=http://<your_ip|domain_name>
```

### Bootstrap Plane with Docker Compose

```bash
docker compose -f docker-compose-hub.yml up
```

### Log in and enjoy your new and shiny Plane instance!

Open your browser and navigate to `http://<your_ip|domain_name>/` to login onto your Plane instance.

{% callout type="note" %}
The Plane self-hosted setup has been updated with the release of version 0.7.1. If you are currently using an older version of Plane and encounter a database connection error after running the new containers, it is likely due to the username and password changes for the PostgreSQL containers in the 0.7.1 setup.

To resolve this error, you can follow these steps if you were using the default password and username:

Set the username as `PGUSER=plane` and the old password as `PGPASSWORD=xyzzyspoon` in the generated env file.
Restart the containers.
{% /callout %}

