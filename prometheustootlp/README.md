# Pulling Prometheus metrics and sending to New Relic via OTLP

This example simulates a source of data produced using Prometheus
and then sent to New Relic over OTLP using the OpenTelemetry Collector.

Running the example spins up two instance of the OpenTelemetry Collector.

1. The `local` collector is meant to simulate the data source that exposes
   metrics via a Prometheus scrape endpoint. For the purposes of this
   example the metrics generated using the Host Metrics Receiver. The
   collector is configured with the Prometheus Exporter and exposes collected
   metrics on the endpoint `local-collector:1234`.
2. The `gateway` collector is configured with the Promethus Receiver and
   scrapes metrics from the `local` collector's endpoint. It is configured with
   the OTLP Exporter to ship metrics to New Relic.

To run the example:

```shell
export NEW_RELIC_OTLP_ENDPOINT=https://otlp.nr-data.net:4317
export NEW_RELIC_API_KEY=<your_api_key>
docker compose up --build
```

**NOTE:** Given this example produces system metrics, you might expect it to
result in a host entity in New Relic. Though, it does not. The synthesis rule
to generate a host entity from OpenTelemetry data require the system metrics to
have a `system.` prefix. Since these metrics are produced using Prometheus, the
metrics instead have a `system_` prefix.

The gateway collector could be configured to rename these metrics, but that is
beyond the scope of this example since the focus is not really host metrics.
