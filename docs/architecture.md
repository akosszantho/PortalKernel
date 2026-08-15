# PortalKernel Architecture

## Purpose

This document records the current architectural direction of PortalKernel. It is intentionally a living document and will change as the project is implemented and better understood.

## Architectural principles

1. **Understandability first.** The design should remain understandable to the person implementing it.
2. **Modularity where it has value.** Components should be replaceable when an interface provides real portability, extensibility, or clarity benefits.
3. **Avoid premature abstraction.** Modularity is not a goal by itself.
4. **Clear subsystem boundaries.** Components should depend on stable interfaces instead of unnecessary implementation details.
5. **Document the reasoning.** Important architectural choices should be recorded together with alternatives and trade-offs.

## High-level model

The intended system can be viewed as layers:

```text
User space
    |
System call interface
    |
Kernel core
    |-- Process / thread management
    |-- Scheduler
    |-- Virtual memory
    |-- Interrupts / exceptions
    |-- IPC
    |
Kernel subsystems / interfaces
    |-- VFS
    |-- Block devices
    |-- Device framework
    |-- Networking
    |
Drivers / concrete implementations
    |
Hardware / x86_64 architecture
```

This is a direction rather than a final implementation requirement.

## Major subsystems

### Boot and architecture

Responsible for bringing the kernel into execution and initializing x86_64-specific functionality such as CPU state, descriptor tables, interrupt handling, and later multi-core support.

### Memory management

Expected to contain physical memory management, virtual memory/page tables, and kernel dynamic allocation. Different allocation strategies may eventually be replaceable behind appropriate interfaces.

### Processes, threads, and scheduler

Responsible for execution contexts, address spaces, process/thread lifecycle, and deciding which runnable execution context receives CPU time.

### Interrupts and exceptions

Provides the boundary between asynchronous hardware events, CPU exceptions, and kernel handlers.

### Device and driver framework

The kernel should reason about generic device capabilities where practical rather than hard-coding individual hardware models into higher-level subsystems.

### VFS and filesystems

A virtual filesystem interface is planned so that higher-level code can work with files and directories without depending directly on one filesystem implementation. Concrete filesystem implementations should be replaceable when that abstraction remains useful.

### Block devices

A block-device abstraction can separate storage consumers from concrete devices such as NVMe or SATA storage.

### Networking

A future networking stack is expected to separate socket/application interfaces, network protocols, and network-device drivers.

### IPC and system calls

IPC will provide mechanisms for communication between execution contexts. System calls will define the controlled interface between user space and kernel space.

## Kernel vs user space

Not every subsystem must permanently live inside the kernel. As the project develops, individual responsibilities can be evaluated based on isolation, performance, complexity, and educational value.

The exact kernel architecture (monolithic, microkernel, hybrid, or another design) is intentionally **not decided yet**.

## Current status

No subsystem implementation has been committed yet. The current architecture describes design intent, not completed functionality.
