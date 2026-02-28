# WASIX Patches for Rust Crates

This repository contains WASIX-compatible patches for the following Rust crates:

| Crate | Version | Purpose |
|-------|---------|---------|
| libc | 0.2.181 | C library bindings with WASIX socket/network API |
| mio | 1.1.1 | Non-blocking I/O with WASIX epoll support |
| socket2 | 0.6.2 | Socket bindings for WASIX |
| tokio | 1.49.0 | Async runtime with WASIX support |

## Target Platform

- `target_os = "wasi"`
- `target_vendor = "wasmer"` (Wasmer/WASIX)

## Usage

Add these patches to your `Cargo.toml`:

```toml
[patch.crates-io]
libc = { path = "./libc" }
mio = { path = "./mio" }
socket2 = { path = "./socket2" }
tokio = { path = "./tokio" }
```

Or use git references:

```toml
[patch.crates-io]
libc = { git = "https://github.com/YOUR_USERNAME/wasix-patches.git", branch = "main" }
mio = { git = "https://github.com/YOUR_USERNAME/wasix-patches.git", branch = "main" }
socket2 = { git = "https://github.com/YOUR_USERNAME/wasix-patches.git", branch = "main" }
tokio = { git = "https://github.com/YOUR_USERNAME/wasix-patches.git", branch = "main" }
```

## Key Features

### libc (0.2.181)
- Added `src/wasi/wasix.rs` with socket and network API bindings
- Conditional compilation for `target_vendor = "wasmer"`

### mio (1.1.1)
- Added `src/sys/wasi/` directory with:
  - epoll implementation using `wasix::epoll_*`
  - TCP/UDP socket support
  - Pipe and waker support
- Uses `wasix = "0.13"` crate

### socket2 (0.6.2)
- Added `src/sys/wasi.rs` for WASIX socket operations
- Compatible with mio WASIX implementation

### tokio (1.49.0)
- Modified compile error check to allow Wasmer target
- Added `wasi_ext` feature for filesystem operations
- Updated conditional compilation for `target_vendor = "wasmer"`
- Uses patched libc, mio, socket2

## Building

```bash
# Build with cargo wasix
cargo wasix build --release
```

## License

Each crate retains its original license from upstream.
