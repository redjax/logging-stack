# cAdvisor

cAdvisor monitors Docker containers and exposes resource utilization metrics for collection by the central Prometheus instance. Metrics include CPU usage, memory consumption, network activity, and filesystem statistics.

## Configuration

Edit `.env` to configure:

- `CADVISOR_IMAGE`: Container image.
- `CADVISOR_BIND_ADDRESS`: Network interface to bind the metrics endpoint.

## Deployment

```bash
docker compose up -d
```

Metrics are exposed at: `http://<machine-ip>:8080/metrics`

Add this endpoint to the central Prometheus scrape targets to begin collecting metrics.
