# Collectors

This directory contains independently deployable telemetry collectors for monitoring machines across the infrastructure. Each collector has its own Docker Compose configuration and environment file, allowing it to be deployed and configured independently on individual machines.

## Available collectors

| Collector                         | Purpose                                                  |
| --------------------------------- | -------------------------------------------------------- |
| [Alloy](./alloy/)                 | Collects and forwards logs to the central Loki instance. |
| [cAdvisor](./cadvisor/)           | Exposes Docker container metrics for Prometheus.         |
| [Node Exporter](./node-exporter/) | Exposes Linux host metrics for Prometheus.               |

## Deployment

Each collector can be deployed independently. Navigate to its directory and start the service:

```bash
cd collectors/<collector>
docker compose up -d
```

Before deploying, review the `.env` file and adjust settings for the local machine and central logging server.
