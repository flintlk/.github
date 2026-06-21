# flintlk

Production-grade infrastructure primitives for Go.

flintlk is a suite of embeddable, composable infrastructure components — each works standalone as a library or as a deployed daemon. Built with a shared config convention, unified observability, and consistent operational interface across every component.

## Components

| Component                                         | Description                                                  | Status         |
| ------------------------------------------------- | ------------------------------------------------------------ | -------------- |
| [core](https://github.com/flintlk/core)           | Shared interfaces, health, metrics, config, lifecycle, log   | ✅ stable      |
| [cache](https://github.com/flintlk/cache)         | LFU cache with TTL, sharding, and active expiry              | 🚧 in progress |
| [ratelimit](https://github.com/flintlk/ratelimit) | Sliding window + token bucket, local and distributed         | 🔜 planned     |
| [breaker](https://github.com/flintlk/breaker)     | Circuit breaker with half-open probing                       | 🔜 planned     |
| [pool](https://github.com/flintlk/pool)           | Generic connection pool with health eviction                 | 🔜 planned     |
| [lb](https://github.com/flintlk/lb)               | L4/L7 load balancer with health checks and hot reload        | 🔜 planned     |
| [gateway](https://github.com/flintlk/gateway)     | Plugin-based API gateway                                     | 🔜 planned     |
| [mesh](https://github.com/flintlk/mesh)           | Lightweight service mesh sidecar with mTLS                   | 🔜 planned     |
| [btree](https://github.com/flintlk/btree)         | Embeddable B-tree KV engine with WAL                         | 🔜 planned     |
| [lsm](https://github.com/flintlk/lsm)             | Write-optimized LSM + SSTable engine                         | 🔜 planned     |
| [tsdb](https://github.com/flintlk/tsdb)           | Time series storage with compression and range queries       | 🔜 planned     |
| [raft](https://github.com/flintlk/raft)           | Embeddable Raft consensus                                    | 🔜 planned     |
| [lock](https://github.com/flintlk/lock)           | Distributed lock manager with fencing tokens                 | 🔜 planned     |
| [cron](https://github.com/flintlk/cron)           | Distributed job scheduler with exactly-once semantics        | 🔜 planned     |
| [mq](https://github.com/flintlk/mq)               | Persistent message queue with partitions and consumer groups | 🔜 planned     |
| [tracer](https://github.com/flintlk/tracer)       | Distributed tracing, OTel-compatible                         | 🔜 planned     |
| [cli](https://github.com/flintlk/cli)             | `flint` CLI to scaffold, configure, and run any component    | 🔜 planned     |

## Design Principles

- Every component implements the same `core.Component` interface — `Start`, `Stop`, `Health`, `Name`
- Shared config schema, metrics label convention, and health protocol across all repos
- Embeddable as a Go library or deployable as a standalone daemon
- No framework lock-in — pure Go, minimal dependencies

## License

MIT
