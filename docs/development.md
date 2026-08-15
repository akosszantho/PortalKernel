# PortalKernel Development Environment

## Development workflow

PortalKernel is developed locally and versioned with Git. GitHub is the remote repository and the Synology NAS is used as an additional local backup target.

```text
CLion / local workspace
        |
        +---- Git ----> GitHub
        |
        +---- backup -> Synology NAS
```

The local workspace remains the primary development environment. The NAS is not intended to become the canonical source tree.

## Current tools

### IDE

- CLion
- C is the primary implementation language.

### Version control

- Git
- GitHub
- Default branch: `main`

### Backup

- Synology DS224+
- Synology Drive is intended to provide automatic backup/synchronization of the local project.

## Planned kernel toolchain

The exact toolchain configuration will be documented after it is established. The current direction is:

- x86_64 cross-compiler
- assembler tooling (including NASM where appropriate)
- linker/binutils
- Limine as the initial bootloader/boot protocol environment
- QEMU for virtualized kernel execution
- GDB for debugging

The project should avoid relying on a normal host-target compiler configuration for bare-metal kernel builds. The build process needs to produce the appropriate x86_64 kernel objects and final image independently of the Windows host environment.

## Build philosophy

The first build system should be simple enough that the relationship between source code, compiler, assembler, linker, ELF output, and bootable image remains visible and understandable.

Build-system convenience should not hide the underlying kernel build process during the early learning stages.

## Git workflow

Changes should be kept small and understandable. Commit messages should describe the purpose of a change.

Example:

```text
chore: initialize repository
```

The current repository was initialized with `.gitignore`, and the first commit was pushed to GitHub.

## Documentation workflow

The project discussion in ChatGPT is the planning/design workspace. Decisions and stable project knowledge are recorded in this repository's `docs/` directory.

The kernel source remains the user's implementation work. Documentation may be updated from decisions made during project discussions.
