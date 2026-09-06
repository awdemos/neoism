# neoism

## OVERVIEW

Neoism is a GPU-accelerated terminal emulator / IDE workspace built in Rust. It uses wgpu for rendering, supports agent-driven workspace management, and targets Linux (X11/Wayland), macOS, and WebAssembly.

## STRUCTURE

```
sugarloaf/                    GPU/2D rendering stack (wgpu, custom shaders)
teletypewriter/               Pty and terminal emulation primitives
corcovado/                    Coroutines / async runtime utilities
copa/                         Configuration parser
neoism-backend/               Core backend services
neoism-terminal-core/         Terminal widget / rendering core
neoism-frontend/              Desktop, WASM, and shared frontend crates
neoism-agent/                 AI agent server and CLI crates
neoism-workspace-*            Workspace indexing and daemon
neoism-protocol/              IPC protocol between components
neoism-extensions/            Extension system
```

## COMMANDS

```bash
cargo check -p neoism-terminal-core       # Fast check of terminal core
cargo check -p neoism                    # Full desktop check (requires system libs)
cargo run -p neoism --release            # Run release desktop build
make dev                                 # Dev run with wgpu Metal HUD (macOS)
make docs                                # Start local docs server (npm-based)
make docs-build                          # Build docs site
```

## SETUP

- Rust 1.78+ (check `rust-toolchain.toml` if present).
- System dependencies on Linux: `fontconfig` dev package (`pkg-config` must find `fontconfig.pc`), plus graphics drivers for wgpu/Vulkan.
- The repo contains a `.cargo/config.toml` that points `target-dir` to a shared location. If that path is read-only, override with `CARGO_TARGET_DIR=/var/tmp/neoism-target cargo build` or edit `.cargo/config.toml` locally.
- Use `make dev-isolated` for containerized builds.

## CODE STYLE

- Rust edition 2021.
- Run `cargo fmt` before committing.
- Prefer `cargo clippy -p <crate>` for scoped linting.
- Keep frontend crates split by platform (`desktop`, `wasm`, `shared`).

## DEPLOYMENT

No Dagger module or recognized deployment configuration was found. The project packages via `cargo-deb` / `.goreleaser.yaml` for macOS `.app` bundles and Linux packages.
