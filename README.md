# aussom-server-examples

A public collection of example applications for [aussom-server](https://aussom-lang.com/docsProduct?product=aussom-server), demonstrating how to build and host apps with the Aussom language and runtime.

Each app under `apps/` is a self-contained example you can run, inspect, and adapt. The current set includes:

- **hogan** — a small REST + HTML fan-page API for the TV show *Hogan's Heroes*. Demonstrates Handlebars templates, JSON endpoints, static resources, scheduled methods, and OpenAPI (`@Api`) annotations.

## Running locally

1. Download the latest aussom-server distribution and extract it into this directory so that `aussom-server`, `aussom-server.jar`, and `lib/` sit alongside `apps/`.
2. Install the local files (generates `start-server.sh`, `config.yaml`, and supporting directories):
   ```bash
   ./aussom-server -i
   ```
3. Start the server:
   ```bash
   ./start-server.sh
   ```
4. The example app is then reachable at `http://localhost:8081/hogan/`.

The admin interface listens on port `8091` by default. Both ports are configurable in `config.yaml`.

---

Copyright 2026 Austin Lehman

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE) for details.
