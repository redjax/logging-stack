# Central Logging

A selfhosted, centralized logging and monitoring stack built with [Grafana](https://grafana.com/), [Loki](https://grafana.com/docs/loki/latest), and [Prometheus](https://prometheus.io/).

The stack provides a central destination for collecting, storing, querying, and visualizing logs and metrics from machines and devices across my homelab's infrastructure. Remote machines use independently configured collectors, such as [Grafana Alloy](https://grafana.com/docs/alloy/latest/) and [Node Exporter](https://prometheus.io/docs/guides/node-exporter/), to forward telemetry to this server.

## Setup

- Copy the [example `.env` file](./.env.example) to `.env`
  - Optionally edit `.env` to customize configuration, such as service ports, resource limits, storage retention, and Grafana credentials.
- Start the stack with `docker compose up -d`

Grafana will be available at `http://<server-ip>:3000`, or whatever port you set in `GRAFANA_HTTP_PORT` in the `.env` file.

## Configuration

The `config/` directory contains configuration files for the central services.

- `config/grafana/`: Grafana provisioning, including datasource configuration.
- `config/loki/`: Loki configuration, including storage and log retention settings.
- `config/prometheus/`: Prometheus configuration and scrape target definitions.

### Adding Prometheus Targets

Remote Prometheus exporters can be added through YAML files in `config/prometheus/targets/`.

Create a new file for a machine or group of machines (e.g. `desktop.yml`):

```yaml
- targets:
    - 192.168.1.50:9100
  labels:
    hostname: desktop
    environment: home
```

Targets are automatically discovered by Prometheus through file-based service discovery. Changes are detected periodically and do not require a Prometheus restart. Ensure the target directory is mounted into the Prometheus container and referenced by a `file_sd_configs` entry in `prometheus.yml`.

## Troubleshooting

### Permission errors with local volume mounts

If you set a host bind mount (local directory) for `PROMETHEUS_DATA_DIR` or `GRAFANA_DATA_DIR`, you are likely to get permission errors when starting the container. While you could use `chown` to set the correct owner on the local directory, it is easier to use the default Docker named volumes for these 2 services. If you want to interact with the files in the volume, find its path in `/var/lib/docker/volumes`.

Loki does not have this problem, and can use host volume mounts for its data directory.
