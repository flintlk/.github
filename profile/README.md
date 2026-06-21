# Flint Toolkit

Flint is a suite of production-grade, embeddable infrastructure primitives for Go. Each component is designed to work standalone as an imported library or as a deployed daemon, with a shared operational contract across all repos — same config schema, same health protocol, same metrics conventions.

The goal is to eliminate the integration tax that comes from stitching together Nginx, Redis, Kafka, Jaeger, and others with different config formats, different observability models, and different deployment patterns. Flint components are designed together, so they compose without friction.

## Components

| Component                                         | Description                                                                               | Status      |
| ------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------- |
| [core](https://github.com/flintlk/core)           | Shared interfaces, health, metrics, config, lifecycle, and logging primitives             | stable      |
| [cache](https://github.com/flintlk/cache)         | O(1) LFU cache with TTL, sharded concurrency, and active expiry                           | in progress |
| [ratelimit](https://github.com/flintlk/ratelimit) | Sliding window and token bucket rate limiter, local and Redis-backed distributed mode     | planned     |
| [breaker](https://github.com/flintlk/breaker)     | Circuit breaker with half-open probing and configurable failure thresholds                | planned     |
| [pool](https://github.com/flintlk/pool)           | Generic connection pool with health eviction and backpressure                             | planned     |
| [lb](https://github.com/flintlk/lb)               | L4/L7 load balancer with weighted least-connections, health checks, and hot config reload | planned     |
| [gateway](https://github.com/flintlk/gateway)     | Plugin-based API gateway with routing, auth, rate limiting, and hot reload                | planned     |
| [mesh](https://github.com/flintlk/mesh)           | Lightweight service mesh sidecar with mTLS, retries, and traffic shaping                  | planned     |
| [btree](https://github.com/flintlk/btree)         | Embeddable B-tree KV storage engine with WAL and concurrent read access                   | planned     |
| [lsm](https://github.com/flintlk/lsm)             | Write-optimized LSM and SSTable storage engine                                            | planned     |
| [tsdb](https://github.com/flintlk/tsdb)           | Time series storage engine with compression and range query support                       | planned     |
| [raft](https://github.com/flintlk/raft)           | Embeddable Raft consensus with leader election and log replication                        | planned     |
| [lock](https://github.com/flintlk/lock)           | Distributed lock manager with lease-based fencing tokens                                  | planned     |
| [cron](https://github.com/flintlk/cron)           | Distributed job scheduler with exactly-once delivery semantics                            | planned     |
| [mq](https://github.com/flintlk/mq)               | Persistent message queue with partitions, consumer groups, and offset tracking            | planned     |
| [tracer](https://github.com/flintlk/tracer)       | Distributed tracing with OpenTelemetry-compatible context propagation                     | planned     |
| [cli](https://github.com/flintlk/cli)             | Unified CLI to scaffold, configure, and run any Flint component                           | planned     |

## Design Principles

Every Flint component implements the `core.Component` interface, exposing `Start`, `Stop`, `Health`, and `Name`. This means every component participates in the same lifecycle management, health reporting, and graceful shutdown model regardless of what it does internally.

Components share a config loading convention via `core/config` — YAML-first with environment variable override support. Metrics are registered through `core/metrics`, which wraps a Prometheus registry and enforces consistent label conventions (`component`, `version`, `env`) across all instrumentation. Logging is handled via `core/log`, a structured zap wrapper with standard fields baked in.

Each component is a standalone Go module, importable independently with no coupling to other Flint components beyond `core`. The `daemon/` package in each repo provides a runnable binary for teams that prefer a sidecar or standalone deployment model over library embedding.

## Language and Runtime

All components are implemented in Go. Client libraries for Node.js and Python are planned as thin gRPC wrappers around the daemon mode, with no reimplementation of core logic.

## License

MIT
