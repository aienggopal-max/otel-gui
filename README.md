# otel-gui

otel-gui is a local OpenTelemetry viewer for traces, logs, and metrics. It accepts OTLP over HTTP in JSON or Protobuf and updates the browser as telemetry arrives. It includes a trace waterfall, correlated logs, metrics charts, and a service map. Telemetry is stored in memory by default.

This repository is owned by [aienggopal-max](https://github.com/aienggopal-max). It is a copy of [metafab/otel-gui](https://github.com/metafab/otel-gui), originally created by Fabrice Marguerie. The imported commit attribution was rewritten for this copy. The upstream repository records the original authors and contributors.

## Quick start

Install Node.js 22.17 or newer and pnpm 11.27.0.

```sh
git clone https://github.com/aienggopal-max/otel-gui.git
cd otel-gui
pnpm install --frozen-lockfile
pnpm run dev
```

Open [localhost:4318](http://localhost:4318). From another terminal in the checkout, run the bundled demo to populate the viewer with an e-commerce trace, its logs, and metrics.

```sh
./demo-ecommerce.sh
```

On Windows, run the demo in PowerShell.

```powershell
.\demo-ecommerce.ps1
```

See the [sample data guide](samples/SAMPLE_TRACES.md) for additional examples.

## Sending traces

Configure your SDK to use an OTLP/HTTP exporter and set its base endpoint to `http://localhost:4318`. With a shared OTLP base URL, exporters append `/v1/traces`, `/v1/logs`, or `/v1/metrics` for each signal.

```sh
export OTEL_EXPORTER_OTLP_ENDPOINT=http://localhost:4318
export OTEL_EXPORTER_OTLP_PROTOCOL=http/protobuf
```

## Connect an AI agent with MCP

Add `http://localhost:4318/mcp` as a Streamable HTTP MCP server in your client. The read-only tools search and inspect telemetry, list services, and return the service map. MCP is enabled for loopback clients by default.

## Documentation

- [HTTP API](docs/http-api.md) and [OpenAPI specification](static/openapi.yaml)
- [Environment settings](.env.example) and [optional persistence](docs/enterprise-persistence-module.md)
- [Testing guide](docs/testing.md)

Run `pnpm run check` for type checking, `pnpm run test` for the test suite, and `pnpm run build` for a production build. Start the built server with `node build`.

## License

The project is [MIT licensed](LICENSE). The vendored OpenTelemetry Protocol definitions retain their copyright headers and [Apache 2.0 license](proto/opentelemetry/LICENSE).
