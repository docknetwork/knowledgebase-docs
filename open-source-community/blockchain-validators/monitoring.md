# Monitoring

The nodes don't send telemetry data to Polkadot telemetry by default. This can be enabled  by using the `--telemetry-url='wss://telemetry.polkadot.io/submit/ 0'` command.

You can also check our mainnet explorer at [Subscan](https://dock.subscan.io/).

To monitor other data such as network usage, CPU usage, disk usage, block production, number of connected peers, etc., [Prometheus](https://prometheus.io/) is used. Nodes by default make this data available at 127.0.0.1:9615 (but can be overwritten with `allowPrometheusExt`) and thus Prometheus interface can be configured to listen to that. Prometheus can be downloaded from [here](https://prometheus.io/download/). Once Prometheus is running, configure as follows:

```
scrape_configs:
  # The job name is added as a label `job=dock-node` to any timeseries scraped from this config.
  - job_name: 'dock-node'

    # Override the global default and scrape targets from this job every 5 seconds.
    scrape_interval: 5s

    static_configs:
      - targets: ['<hostname:port of Substrate's Prometheus server.>']
```

Now the Prometheus UI will show various metrics prefixed with `substrate_`.

To visualize the above metrics on [Grafana](https://grafana.com/), import [this Grafana dashboard](https://grafana.com/grafana/dashboards/11784). If you don't know how to import a dashboard, check [here](https://grafana.com/docs/grafana/latest/reference/export\_import/#importing-a-dashboard).
