# README.md

## Overview

This repository provides a Docker-based infrastructure for monitoring and managing multiple web server instances. It leverages Prometheus and Grafana for monitoring, Caddy for reverse proxying, Loki and Promtail for log management, and integrates various exporters for collecting metrics from NGINX and Apache servers.

## Architecture & Structure

```
.
├── apache/
│   └── httpd.conf                  # Apache server configuration
├── blackbox/
│   └── blackbox.yml                # Configuration for Blackbox Exporter
├── caddy/
│   └── Caddyfile                   # Caddy reverse proxy configuration
├── docker-compose.yml              # Docker Compose configuration for deploying the stack
├── loki/
│   └── config.yml                  # Loki configuration for log aggregation
├── nginx-template-dashboard.json   # Grafana dashboard template for NGINX monitoring
├── nginx/
│   └── default.conf                # Default NGINX server configuration
├── prometheus/
│   └── prometheus.yml              # Prometheus configuration for scraping metrics
├── promtail/
│   └── config.yml                  # Promtail configuration for log forwarding
├── test.txt                        # Placeholder text file
├── test.txt.2                      # Additional placeholder text file
```

### Directory & File Descriptions

- **apache/httpd.conf**: Contains the configuration settings for the Apache HTTP Server, including module loading and logging details.
- **blackbox/blackbox.yml**: Defines the module configurations for the Blackbox Exporter, responsible for probing endpoints.
- **caddy/Caddyfile**: Configures the Caddy server to act as a TLS-enabled reverse proxy to route requests to various server instances.
- **docker-compose.yml**: Describes the complete stack via Docker Compose, including services, networks, and volume definitions.
- **loki/config.yml**: Specifies the setup for Loki, which collects logs from configured sources.
- **nginx-template-dashboard.json**: Provides a pre-configured Grafana dashboard for visualizing NGINX metrics.
- **nginx/default.conf**: Sets up NGINX server behavior, including response for specific locations.
- **prometheus/prometheus.yml**: Lists scraping configurations for Prometheus, which collects metrics from monitored services and exporters.
- **promtail/config.yml**: Details Promtail's setup for forwarding system logs to Loki.
- **test.txt** and **test.txt.2**: Placeholder files for unspecified purposes.

## Deployment & Setup

1. **Install Docker and Docker Compose**: Ensure both tools are installed on your system.
2. **Clone the Repository**: Retrieve the repository files using `git clone`.
3. **Navigate into the Repo**: Move into the directory with `cd <repository-dir>`.
4. **Deploy with Docker Compose**:
   ```bash
   docker-compose up -d
   ```
   This command boots the stack in detached mode.

## Configuration & Environment

- **Network and Volumes**: Defined in `docker-compose.yml`, featuring shared networks and persistent volumes for data storage.
- **Environment Variables**: Configured primarily through the Docker Compose file, particularly for Grafana (`GF_SECURITY_ADMIN_PASSWORD`, etc.).
- **External Dependencies**: The environment assumes access to Docker Hub for pulling necessary images.

## Troubleshooting

- **Verify Service Status**: Check container logs to diagnose issues:
  ```bash
  docker-compose logs <service-name>
  ```
- **Network Connectivity**: Ensure defined ports (e.g., `3000`, `9090`, `3100`, etc.) are not blocked by firewalls.
- **Persistent Data Issues**: If data is not persisting, check volume mounting paths and permissions.

## Scripts & Automation

While the repository does not include explicit Bash scripts, it utilizes Docker Compose for orchestration and management of the multi-container environment, handling service dependencies, network, and volume setup automatically.

This README aims to ensure a clear understanding of repository utilization, facilitating both deployment and effective troubleshooting for DevOps professionals.