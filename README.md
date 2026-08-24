[<center><img src="https://raw.githubusercontent.com/sourajitk/STX-Logo/main/stx-2021-kernel.png" height="50%" width="50%;" /></center>](https://github.com/StatiXOS)

## Android 17 BPF / OnePlus 9 Pro

This manifest tracks the current boot-tested OnePlus 9 Pro Android 17 branch:

```text
oneplus/sm8350v_17.0.0_oneplus9pro_sukisu
```

The same kernel source contains both the plain profile and the optional
Docker/LXC/KVM profile. Only `BUILD_CONFIG` changes between them. The manifest
also selects the LTO-capable kernel build tools required for BTF generation.

### Repo init

```bash
repo init -u https://github.com/tqmane/android_kernel_manifest.git \
  -b ci/a17-bpf-runtime-hardening
```

### Sync source

```bash
repo sync --force-sync --no-clone-bundle --current-branch --no-tags -j$(nproc --all)
```

### Plain Android 17 BPF build

```bash
BUILD_CONFIG=kernel/msm-5.4/build.config.lemonade \
VARIANT=qgki \
LTO=thin \
BUILD_KERNEL=1 \
build/build.sh
```

### Docker/LXC/KVM build

```bash
BUILD_CONFIG=kernel/msm-5.4/build.config.lemonade.container \
VARIANT=qgki \
LTO=thin \
BUILD_KERNEL=1 \
build/build.sh
```

SukiSU is already part of the kernel source and is synchronized as a submodule.
The build Action does not install another KernelSU implementation or inject
external kernel patches.
