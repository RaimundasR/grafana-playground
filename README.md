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
├── tets                             # Placeholder or test directory
```

## Architecture & Structure

- **Apache Configuration**: The `httpd.conf` file located in the `apache/` directory configures the Apache HTTP servers used in this setup.

- **Blackbox Exporter**: Located in `blackbox/`, `blackbox.yml` defines modules for HTTP/HTTPS probing used by Prometheus.

- **Caddy Setup**: The `Caddyfile` in the `caddy/` directory configures the reverse proxy rules for routing requests to different services.

- **Docker Compose**: The `docker-compose.yml` file defines all the services including Prometheus, Grafana, Loki, NGINX, and Apache along with their configurations and network settings.

- **Loki Configuration**: The `config.yml` under the `loki/` directory contains configurations for the Loki log aggregator.

- **NGINX Dashboard**: The `nginx-template-dashboard.json` stores a Grafana dashboard template to visualize NGINX metrics collected by Prometheus.

- **NGINX Configuration**: The `default.conf` in `nginx/` sets up basic server configuration for the NGINX instances used.

- **Prometheus Configuration**: Located in `prometheus/`, the `prometheus.yml` defines scraping jobs and targets for Prometheus.

- **Promtail Configuration**: The `promtail/config.yml` file configures log scraping settings for the Promtail client that forwards logs to Loki.

- **README.md**: Main project documentation providing an overview, setup instructions, and other necessary details about the project.

- **tets**: Presumably a placeholder or test directory.

## Deployment & Setup

1. **Prerequisites**:
   - Ensure Docker and Docker Compose are installed on your system.

2. **Deployment Steps**:
   - Clone the repository:
     ```
     git clone <repository-url>
     cd <repository-directory>
     ```
   - Start the stack using Docker Compose:
     ```
     docker-compose up -d
     ```
   - Access Grafana on `http://localhost:3000` using default credentials (`admin` / `admin`).

3. **Service Ports**:
   - Prometheus: `9090`
   - Grafana: `3000`
   - Loki: `3100`
   - Caddy: `80`, `443`
   - Blackbox Exporter: `9115`
   - Custom Application Servers (NGINX, Apache): Monitored through respective reverse proxy paths.

## Configuration & Environment

Configure environment variables as needed in the `docker-compose.yml` for various services. Key environment variables include:

- `GF_SECURITY_ADMIN_PASSWORD`: Sets Grafana's admin password.
- Network and volume configurations ensure persistent data storage for Prometheus, Loki, and Grafana.

## Troubleshooting

- **Containers Not Starting**: Check logs for errors using `docker-compose logs <service-name>`.
- **Network Issues**: Ensure all required ports are open and not blocked by firewall settings.
- **Metric Scraping Failures**: Confirm that Prometheus targets are correctly configured and accessible.
- **SSL/TLS Issues with Caddy**: Verify Caddy configurations in the `Caddyfile` for correct domain and certificate settings.

## Scripts & Automation

The `docker-compose.yml` centralizes the orchestration and deployment of all services, ensuring they start with the defined configurations and environments. Docker volumes and network configurations facilitate the inter-service communication and persistent data storage automatically.