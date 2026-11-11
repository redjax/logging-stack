# Grafana Alloy

Alloy is used to collect and forward logs from the local machine to the central Loki instance. This configuration collects systemd journal entries and forwards them to Loki, including kernel messages, service events, and other system events.

## Configuration

Edit `.env` to configure:

- `LOKI_URL` : URL of the central Loki instance.
- `COLLECTOR_HOSTNAME`: Hostname used to identify this machine in Loki.

The [`config.alloy`](./example.config.alloy) file controls which logs are collected and how they are forwarded.

## Deployment

```bash
docker compose up -d
```

Alloy's HTTP interface is available on port `12345` by default.
