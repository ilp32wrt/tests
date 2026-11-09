# ILP32Wrt tests

Tests of [ILP32Wrt](https://github.com/ilp32wrt/ilp32wrt) images in QEMU, used by its release workflow
and on a local machine. Like [openwrt-tests](https://github.com/openwrt/openwrt-tests) for *OpenWrt*,
the tests are kept apart from the source tree.

| File | What it does |
|---|---|
| `run-openwrt-qemu.sh` | Boots the armsr/armv8 initramfs image and runs the system and C library checks (`openwrt-qemu-test.py`); `NOTIME32=1` forbids the time32 and stat64 system calls with seccomp for the whole system; `BUILD_ONLY=1` only builds the test programs with the toolchain of an ILP32Wrt tree, `PREBUILT` runs prebuilt ones |
| `run-armsr-matrix.sh` | `run-openwrt-qemu.sh` on cortex-a53 and `-cpu max` (PAC, BTI, SVE), each with `NOTIME32` 0 and 1 |
| `measure-memory.sh`, `openwrt-memory.py`, `summarize-memory.py`, `workload-loaded.txt` | Memory comparison of ILP32 and LP64 images with the same workload |
| `src/` | Test programs: C library checks (`musl-test.c`, `tlsmod.c`), raw system calls (`syscall-test.c`), the seccomp init (`notime32-init.c`) |

The test programs come from [test-ilp32](https://github.com/ilp32-a64/test-ilp32), with their history.

```
# in an ILP32Wrt tree after make: build the test programs and run all four QEMU checks
OPENWRT=~/ilp32wrt ./run-armsr-matrix.sh
```

ILP32Wrt is based on *OpenWrt* and is not affiliated with *OpenWrt*. *OpenWrt* is a registered trademark
owned by Software Freedom Conservancy (SFC).
