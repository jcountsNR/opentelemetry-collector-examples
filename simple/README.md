# Simple example

To run the example:

```shell
export NEW_RELIC_API_KEY=<your_api_key>
docker compose up --build
```

Exercise the instrumented .NET application at http://localhost:8080/Weatherforecast.
Or, send data from another application running locally configured to send data over
OTLP to http://localhost:4317 (gRPC) or http://localhost:4318 (HTTP).
