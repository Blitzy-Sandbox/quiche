# Setup

This page summarizes how to build quiche from source. See the project
[README](https://github.com/cloudflare/quiche/blob/master/README.md) for the
authoritative instructions.

## Prerequisites

- **Rust 1.85 or later.** Install via [rustup](https://rustup.rs/).
- **cmake** — required to build the bundled BoringSSL.
- **NASM** — required on Windows for BoringSSL.

## Fetch the source

quiche uses git submodules, so clone recursively:

```bash
git clone --recursive https://github.com/cloudflare/quiche
```

## Build with cargo

```bash
cargo build --examples
```

Run the test suite:

```bash
cargo test
```

## TLS backend options

By default, cargo builds and links the bundled BoringSSL automatically.

To use a custom BoringSSL checkout, point `QUICHE_BSSL_PATH` at it:

```bash
QUICHE_BSSL_PATH="/path/to/boringssl" cargo build --examples
```

To use [OpenSSL/quictls] instead, enable the `openssl` feature. Note that
0-RTT is not supported with this backend.

```bash
cargo build --examples --features openssl
```

## C/C++ FFI

Enable the `ffi` feature to produce `libquiche.a`, a stand-alone static
library suitable for linking into C/C++ programs:

```bash
cargo build --release --features ffi
```

## Cross-compilation

- **Android** — install the Android NDK (r19+, r21 recommended), set
  `ANDROID_NDK_HOME`, add Rust targets
  (`aarch64-linux-android`, `armv7-linux-androideabi`,
  `i686-linux-android`, `x86_64-linux-android`), then build via
  [cargo-ndk]: `cargo ndk -t arm64-v8a -p 21 -- build --features ffi`.
- **iOS** — install Xcode command-line tools, add the
  `aarch64-apple-ios` and `x86_64-apple-ios` targets, then run
  `cargo lipo --features ffi`.

## Running the example apps

The `apps/` crate ships example client and server binaries. They are
intended for demonstration only — not for production.

```bash
cargo run --bin quiche-client -- https://cloudflare-quic.com/
cargo run --bin quiche-server -- \
  --cert apps/src/bin/cert.crt --key apps/src/bin/cert.key
```

The bundled certificate is self-signed; do not use it in production.

## Docker

Build the official images locally with:

```bash
make docker-build
```

Published images are available as `cloudflare/quiche` (client/server
binaries) and `cloudflare/quiche-qns` (quic-interop-runner harness).

[OpenSSL/quictls]: https://github.com/quictls/openssl
[cargo-ndk]: https://docs.rs/crate/cargo-ndk
