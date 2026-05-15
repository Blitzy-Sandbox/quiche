# Workspace overview

quiche is a Cargo workspace. The repository is organized as a collection of
crates that together implement QUIC, HTTP/3, and supporting tooling.

## Core library

- **`quiche/`** — the core crate. Implements the QUIC transport, the
  HTTP/3 layer, and exposes both the Rust API and the C FFI header
  (`quiche/include/quiche.h`).

## Example applications

- **`apps/`** — the `quiche-apps` crate. Contains the `quiche-client` and
  `quiche-server` example binaries used in the README walkthrough.
  Demonstration code only; not production-grade.

## Higher-level integrations

- **`tokio-quiche/`** — async integration layered on top of the core
  library using the Tokio runtime.
- **`h3i/`** — interactive HTTP/3 client used for protocol exploration
  and conformance testing.

## Wire-format and observability helpers

- **`octets/`** — zero-copy buffer helpers for reading and writing the
  on-wire byte representations used throughout the codebase.
- **`qlog/`** — Rust types for the [qlog] structured logging format used
  to capture QUIC and HTTP/3 events.
- **`qlog-dancer/`** — tooling around qlog event streams.
- **`netlog/`** — additional network-event logging support.
- **`buffer-pool/`** — reusable buffer pooling primitives.
- **`datagram-socket/`** — abstractions over UDP datagram sockets used
  by the higher-level crates.
- **`task-killswitch/`** — cooperative cancellation primitive for
  long-running async tasks.

## Testing and tooling

- **`fuzz/`** — fuzzing harnesses driven by `cargo-fuzz`.
- **`tools/`** — helper scripts, including Android build helpers
  (e.g. `tools/android/build_android_ndk19.sh`) and interop utilities.
- **`Dockerfile`, `Makefile`** — produce the published
  `cloudflare/quiche` and `cloudflare/quiche-qns` Docker images.

## Repository metadata

- **`Cargo.toml`** — workspace manifest tying the crates together.
- **`COPYING`** — BSD-2-Clause license.
- **`RELEASING.md`** — maintainer release process.
- **`catalog-info.yaml`** — Backstage catalog entry for this repository.

[qlog]: https://datatracker.ietf.org/doc/draft-ietf-quic-qlog-main-schema/
