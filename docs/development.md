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

The initial Windows development environment will use **MSYS2 UCRT64** as the tool/package environment. MSYS2 recommends UCRT64 when unsure which environment to use.

The kernel compiler itself must target bare-metal x86_64 rather than Windows. The current direction is to use LLVM/Clang with an explicit `x86_64-elf` target and LLD, rather than treating the normal Windows compiler as a kernel compiler.

### Toolchain components

| Component | Purpose | Project / official source |
|---|---|---|
| MSYS2 UCRT64 | Windows Unix-like package/build environment | [MSYS2](https://github.com/msys2) |
| Clang / LLVM | C compiler and LLVM toolchain | [LLVM](https://github.com/llvm/llvm-project) |
| LLD | LLVM linker, including ELF support | [LLVM](https://github.com/llvm/llvm-project) |
| NASM | x86 assembler | [NASM](https://github.com/netwide-assembler/nasm) |
| GNU Make | Initial build-system tool | [GNU Make](https://git.savannah.gnu.org/cgit/make.git) |
| Limine | Initial bootloader / boot protocol environment | [Limine](https://github.com/Limine-Bootloader/Limine) |
| QEMU | Virtual machine / hardware emulation | [QEMU](https://github.com/qemu/qemu) |
| GDB | Debugger | [GDB / binutils-gdb](https://sourceware.org/git/binutils-gdb.git) |

### Official download / documentation links

- [MSYS2 installer](https://www.msys2.org/docs/installer/)
- [MSYS2 environments](https://www.msys2.org/docs/environments/)
- [LLVM downloads](https://releases.llvm.org/download.html)
- [NASM](https://www.nasm.us/)
- [QEMU Windows downloads](https://www.qemu.org/download/)
- [GDB downloads](https://www.sourceware.org/gdb/download/)
- [Limine releases](https://github.com/Limine-Bootloader/Limine/releases)
- [Limine boot protocol](https://github.com/Limine-Bootloader/limine-protocol)

## Windows installation plan

Install MSYS2 first. Use the **UCRT64** terminal for the PortalKernel toolchain.

After the initial MSYS2 installation and system update, the intended packages are:

```bash
pacman -S --needed make xorriso
pacman -S --needed mingw-w64-ucrt-x86_64-clang
pacman -S --needed mingw-w64-ucrt-x86_64-lld
pacman -S --needed mingw-w64-ucrt-x86_64-nasm
pacman -S --needed mingw-w64-ucrt-x86_64-gdb
pacman -S --needed mingw-w64-ucrt-x86_64-qemu
pacman -S --needed mingw-w64-ucrt-x86_64-mtools
```

These packages are intentionally installed through one package environment so the development setup is reproducible instead of mixing many unrelated Windows installers.

The exact package list may change as the build system develops. In particular, `xorriso` and `mtools` are image-building dependencies and may only become necessary when the first bootable ISO/disk image is created.

## Toolchain verification

After installation, verify the host-side tools before writing kernel code.

Run these from the MSYS2 UCRT64 terminal:

```bash
clang --version
ld.lld --version
nasm -v
make --version
gdb --version
qemu-system-x86_64 --version
xorriso --version
mformat -V
```

The first important cross-compilation test will be performed separately and must confirm that Clang can target bare-metal x86_64:

```bash
clang --target=x86_64-elf --version
```

A successful version response alone does not prove that a complete kernel can be linked. The next milestone is a small freestanding compilation/link test that verifies the complete compiler → object → ELF linker pipeline.

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
