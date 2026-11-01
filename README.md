# Homelab Logging

My Docker Compose stacks for collecting logs in my homelab. Uses a combination of Alloy, node_exporter, Loki, Grafana, and Prometheus to collect and chart events happening throughout the infrastructure.

> [!NOTE]
> This repository is a work in progress. The directory paths & configurations are subject to change. You can use this as a starting point for your own logging infrastructure if you'd like.

To see the logging server's Compose stack, check [`homenet-syslog`](./stacks/homenet-syslog/).

## TODO

Work in progress items:

- Formalize central logging server.
- Create templates for each container, instead of repeating them throughout the stacks.
- Separate central server templates from "satellite" collectors.
