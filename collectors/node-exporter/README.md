# Prometheus Node Exporter

Node Exporter exposes hardware and operating system metrics from the local Linux machine for collection by the central Prometheus instance. Metrics include CPU utilization, memory usage, disk I/O, filesystem capacity, network statistics, and system uptime.

## Configuration

Edit `.env` to configure:

- `NODE_EXPORTER_IMAGE`: Container image.
- `NODE_EXPORTER_LISTEN_ADDRESS`: Address and port used for the metrics endpoint.

Node Exporter uses host networking and requires access to the host filesystem to collect system metrics.

## Deployment

```bash
docker compose up -d
```

Metrics are exposed at `http://<machine-ip>:9100/metrics`

Add this endpoint to the central Prometheus scrape targets to begin collecting metrics.
