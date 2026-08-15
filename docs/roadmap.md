# PortalKernel Roadmap

This roadmap is a guide, not a rigid schedule. Milestones may be reordered, split, removed, or expanded as the project develops.

## Phase 0 — Development environment

- [x] Create the GitHub repository
- [x] Set up the local Git repository
- [x] Configure the `main` branch
- [x] Establish the first commit and GitHub push workflow
- [x] Set up the Synology NAS as the project backup target
- [ ] Document the complete development environment
- [ ] Establish the kernel cross-compilation toolchain
- [ ] Set up QEMU
- [ ] Set up Limine
- [ ] Set up GDB/debugging workflow

## Phase 1 — First boot

Goal: produce a minimal x86_64 kernel image and boot it in QEMU.

- [ ] Understand the boot protocol and bootloader responsibilities
- [ ] Build a minimal kernel ELF
- [ ] Boot the kernel with Limine
- [ ] Establish a minimal kernel entry point
- [ ] Produce a first observable kernel output

## Phase 2 — CPU, interrupts, and architecture

- [ ] Understand x86_64 privilege levels and CPU state
- [ ] Establish GDT-related structures as required
- [ ] Establish the IDT
- [ ] Handle CPU exceptions
- [ ] Establish interrupt handling
- [ ] Initialize an interrupt controller
- [ ] Investigate timer interrupts
- [ ] Document architecture-specific boundaries

## Phase 3 — Memory management

- [ ] Discover and describe physical memory
- [ ] Implement a physical page management strategy
- [ ] Understand and establish page tables
- [ ] Implement virtual memory management
- [ ] Design kernel heap allocation
- [ ] Evaluate allocator interfaces and possible implementations

## Phase 4 — Processes, threads, and scheduling

- [ ] Define execution context structures
- [ ] Introduce threads
- [ ] Introduce processes/address spaces
- [ ] Implement context switching
- [ ] Design the scheduler interface
- [ ] Implement an initial simple scheduler

## Phase 5 — System calls and user space

- [ ] Define the initial syscall boundary
- [ ] Implement syscall entry/dispatch
- [ ] Establish a minimal user-space execution environment
- [ ] Define basic process lifecycle operations
- [ ] Introduce initial IPC mechanisms

## Phase 6 — VFS and filesystems

- [ ] Define the VFS model
- [ ] Define file, directory, and filesystem interfaces
- [ ] Introduce a first filesystem implementation
- [ ] Evaluate replaceable filesystem backends
- [ ] Add a block-device abstraction where appropriate

## Phase 7 — Device framework and drivers

- [ ] Design device registration/discovery
- [ ] Investigate PCI enumeration
- [ ] Introduce the first practical device driver
- [ ] Define driver/subsystem interfaces
- [ ] Evaluate driver isolation boundaries

## Phase 8 — Networking

- [ ] Define network-device interfaces
- [ ] Implement initial packet handling
- [ ] Introduce Ethernet support
- [ ] Introduce IP networking
- [ ] Introduce UDP/TCP as appropriate
- [ ] Define a user-facing socket interface

## Phase 9 — User space and system services

- [ ] Establish an init process/service model
- [ ] Build a basic shell
- [ ] Introduce system utilities
- [ ] Establish a coherent user-space API

## Phase 10 — Higher-level platform

Possible future areas:

- [ ] Graphics/display subsystem
- [ ] Input subsystem
- [ ] Window management
- [ ] Compositor/desktop environment
- [ ] Power management
- [ ] Audio
- [ ] More complete hardware support

These are long-term possibilities, not current commitments.

## Guiding rule

A milestone is complete when the underlying concepts are understood and documented, not merely when code happens to work.
