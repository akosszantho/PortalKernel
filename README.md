# PortalKernel

## Overview

PortalKernel is an educational, modular x86_64 operating-system kernel project written primarily in C.

The project is intended to be built as a long-term learning project: understanding how a kernel works is more important than reaching a usable operating system as quickly as possible.

## Goals

- Learn low-level systems programming and x86_64 architecture.
- Build a working kernel from the ground up.
- Keep the kernel modular and understandable.
- Design replaceable subsystem interfaces where that provides real architectural value.
- Explore the boundary between kernel-space and user-space.
- Document architectural decisions and the reasoning behind them.

## Non-goals

PortalKernel is not intended to be a Linux replacement or a clone of an existing operating system. It is an experimental and educational platform that may eventually grow into a usable system.

## Development philosophy

The project follows a framework-oriented approach where practical. Subsystems should communicate through clear interfaces rather than unnecessarily depending on concrete implementations.

For example, a filesystem implementation should be replaceable behind a filesystem/VFS interface when doing so keeps the system easier to maintain and extend.

Modularity is not an end in itself: abstractions should be introduced when they provide a meaningful benefit in portability, extensibility, or clarity.

## Project status

The project is currently in the planning and development-environment phase. The repository and basic Git workflow are established; kernel implementation has not started yet.

See [`docs/roadmap.md`](docs/roadmap.md) for the current development plan.

## Documentation

- [`docs/architecture.md`](docs/architecture.md) — system architecture and subsystem boundaries
- [`docs/roadmap.md`](docs/roadmap.md) — development roadmap and milestones
- [`docs/development.md`](docs/development.md) — development environment and tooling
- [`docs/decisions.md`](docs/decisions.md) — architectural decisions and their reasoning

## License

License to be decided.
