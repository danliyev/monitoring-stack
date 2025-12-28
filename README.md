# Monitoring Stack

Docker Compose stack for monitoring with Prometheus, Grafana, Loki, and Node Exporter.

## Components

- **Prometheus** - metrics collection and storage
- **Grafana** - data visualization
- **Loki** - log aggregation
- **Node Exporter** - host metrics
- **Nginx** - reverse proxy with basic auth

## Security

All services listen only on `127.0.0.1` and are not directly accessible from outside. Access is only through Nginx.

## Installation

1. Copy `.env.example` to `.env` and change passwords:

   ```bash
   cp .env.example .env
   ```

2. Generate password for Nginx basic auth:

   ```bash
   htpasswd -nb admin yourpassword > nginx/.htpasswd
   ```

3. (Optional) Add SSL certificates to `nginx/ssl/`:

   - `cert.pem` - certificate
   - `key.pem` - private key

4. Start the stack:

   ```bash
   docker compose up -d
   ```

## Access

| Service    | URL                            | Authentication         |
| ---------- | ------------------------------ | ---------------------- |
| Grafana    | http://example.com/            | Login from .env        |
| Prometheus | http://example.com/prometheus/ | Basic Auth (.htpasswd) |
| Loki       | http://example.com/loki/       | Basic Auth (.htpasswd) |

## Ports

- Prometheus: 127.0.0.1:9090
- Grafana: 127.0.0.1:8880
- Loki: 127.0.0.1:3100
- Node Exporter: 127.0.0.1:9100
- Nginx: 0.0.0.0:80, 0.0.0.0:443
