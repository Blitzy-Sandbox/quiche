# quiche

quiche is an implementation of the [QUIC] transport protocol and HTTP/3 as
specified by the [IETF]. It provides a low-level API for processing QUIC
packets and handling connection state. The application is responsible for
providing I/O (e.g. sockets handling) as well as an event loop with support
for timers.

quiche is developed by Cloudflare and published as a [Rust crate], with a
thin C API on top of the Rust API for use from C/C++ applications and other
languages via FFI.

## What is QUIC?

QUIC is a general-purpose, secure transport protocol standardized by the
IETF in [RFC 9000]. It runs over UDP, integrates TLS 1.3 for encryption,
multiplexes streams without head-of-line blocking, and provides the
foundation for HTTP/3.

## Who uses quiche?

- **Cloudflare** — powers the edge network's HTTP/3 support; see
  [cloudflare-quic.com](https://cloudflare-quic.com) for testing.
- **Android** — the platform DNS resolver uses quiche to implement
  DNS over HTTP/3.
- **curl** — quiche can be integrated into curl to provide HTTP/3 support.

## Supported standards

quiche tracks the IETF QUIC working group specifications, including the
core transport (RFC 9000), TLS binding (RFC 9001), loss detection and
congestion control (RFC 9002), and HTTP/3 (RFC 9114).

## Further reading

- API docs: <https://docs.quic.tech/quiche/>
- Crate page: <https://crates.io/crates/quiche>
- Design background: [Cloudflare blog post on quiche][post]

[QUIC]: https://quicwg.org/
[IETF]: https://quicwg.org/
[Rust crate]: https://crates.io/crates/quiche
[RFC 9000]: https://datatracker.ietf.org/doc/html/rfc9000
[post]: https://blog.cloudflare.com/enjoy-a-slice-of-quic-and-rust/
