# Project Overview

This repository contains a comprehensive setup for a monitoring stack using Docker Compose. The project leverages Prometheus for monitoring, Grafana for visualization, and Loki for logging. It also includes configurations for reverse proxying and metric scraping using Caddy, NGINX, and Apache servers along with their respective exporters.

## File Tree

```
.
├── apache/
│   └── httpd.conf                   # Apache server configuration file
├── blackbox/
│   └── blackbox.yml                 # Blackbox exporter configuration for Prometheus
├── caddy/
│   └── Caddyfile                    # Configuration for Caddy reverse proxy
├── docker-compose.yml               # Docker Compose file defining the services and their configurations
├── loki/
│   └── config.yml                   # Configuration for Loki log aggregation
├── nginx-template-dashboard.json    # Grafana dashboard template for NGINX
├── nginx/
│   └── default.conf                 # NGINX server configuration file
├── prometheus/
│   └── prometheus.yml               # Prometheus server configuration for scraping metrics
├── promtail/
│   └── config.yml                   # Configuration for Promtail to scrape logs
├── README.md                        # Main project documentation
```

## Architecture & Structure

- **Apache Configuration**: Located under `apache/`, the `httpd.conf` file configures the Apache HTTP servers used in this setup.
- **Blackbox Exporter**: In the `blackbox/` directory, `blackbox.yml` defines modules for HTTP/HTTPS probing used by Prometheus.
- **Caddy Setup**: The `Caddyfile` in the `caddy/` directory configures reverse proxy rules for routing requests in a secured way.
- **Docker Compose**: `docker-compose.yml` defines all the services, including Prometheus, Grafana, Loki, NGINX, and Apache, along with their configurations and network settings.
- **Loki Configuration**: The `config.yml` under `loki/` contains configurations for the Loki log aggregator.
- **NGINX Dashboard**: `nginx-template-dashboard.json` stores a Grafana dashboard template to visualize NGINX metrics collected by Prometheus.
- **NGINX Configuration**: Under `nginx/`, the `default.conf` file sets up basic server configurations for NGINX instances.
- **Prometheus Configuration**: Located in `prometheus/`, the `prometheus.yml` file defines scraping jobs and targets for Prometheus.
- **Promtail Configuration**: The `config.yml` file in `promtail/` configures log scraping settings for the Promtail client to forward logs to Loki.
- **README.md**: This file provides an overview, setup instructions, and other necessary details about the project.

## Deployment & Setup

### Prerequisites
- Ensure Docker and Docker Compose are installed on your system.

### Deployment Steps
1. Clone the repository:
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```
2. Start the stack using Docker Compose:
    ```bash
    docker-compose up -d
    ```
3. Access Grafana on `http://localhost:3000` using default credentials (`admin` / `admin`).

### Service Ports
- Prometheus: `9090`
- Grafana: `3000`
- Loki: `3100`
- Caddy: `80`, `443`
- Blackbox Exporter: `9115`
- Custom Application Servers (NGINX, Apache): Monitored through respective reverse proxy paths.

## Configuration & Environment

Configurations for the project are primarily handled within `docker-compose.yml`. Key environment variables include:

- `GF_SECURITY_ADMIN_PASSWORD`: Sets Grafana's admin password.
- Network and volume configurations ensure persistent data storage for Prometheus, Loki, and Grafana.

## Troubleshooting

- **Containers Not Starting**: Check logs for errors using `docker-compose logs <service-name>`.
- **Network Issues**: Ensure all required ports are open and not blocked by firewall settings.
- **Metric Scraping Failures**: Confirm that Prometheus targets are correctly configured and accessible.
- **SSL/TLS Issues with Caddy**: Verify Caddy configurations in the `Caddyfile` for correct domain and certificate settings.

## Scripts & Automation

The `docker-compose.yml` is the central file for orchestrating and deploying all services. It ensures configurations are applied and services start in the intended state. Docker volumes and network settings facilitate inter-service communication and persistent data storage, ensuring the stack runs smoothly with minimal manual intervention.