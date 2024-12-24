### LEARNING PROMETHEUS

### Prometheus Basics & Configuration

`Prometheus` is a monitoring tool that collects metrics data, and provide tools to visualize the collected data.

Prometheus collects the metrics by scraping targets who expose metrics through an HTTP endpoint. i.e by sending http requests to `/metrics` endpoint of each target.

Although, prometheus can be configured to use a different path other than `metrics`

The scraped metrics are then stored in a time series database which can then be queried using prometheus `PromQL`

Prometheus collects metrics of the following type

- CPU/Memory utilization
- Disk space
- Service uptime
- Application specific data

Also, most systems by default son't collect metrics and expose them on an HTTP endpoint to be consumed by a prometheus server, but an _**exporter**_ collects and expose them in a format prometheus expects.

`Prometheus configuration` is handled through a YAML file usually named `prometheus.yml`. This file determines how prometheus operates from data collection to scraping of target systems.

Below is an example of the _**prometheus.yml**_ file

```yml
global:
  scrape_interval: 1m
  scrape_timeout: 15s

scrape_configs:
  - job_name: "node"
    scrape_interval: 20s
    scrape_timeout: 5s
    scrape_limit: 1000
    static_configs:
      - targets: ["localhost:9090"]
    basic_auth:
      [ username: <string> ]
      [ username_file: <string> ]
      [ password: <secret> ]
      [ password_file: <string> ]
    metrics_path: "/metrics_path"

# Configuration related to alert manager
alerting:
# Specify a list of files rules are read from
rule_files:
# Settings related to remote read/write feature
remote_read:
remote_write:
# Storage related settings
storage:
```

After making changes to the prometheus config file, there is need for a reload of the configuration for the changes to take place.
