[<center><img src="https://raw.githubusercontent.com/sourajitk/STX-Logo/main/stx-2021-kernel.png" height="50%" width="50%;" /></center>](https://github.com/StatiXOS)

## Android 17 BPF / OnePlus 9 Pro

This branch tracks the boot-tested Linux 5.4.254 Android 17 BPF compatibility
kernel plus the task-local-storage recursion hardening branch. The manifest also
selects the LTO-capable kernel build tools required for BTF generation.

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

The optional Docker/LXC/KVM profile lives on the dedicated kernel branch
`oneplus/sm8350v_17.0.0_oneplus9pro_sukisu_lxc_docker_kvm` and uses
`kernel/msm-5.4/build.config.lemonade.container`. The build Action selects that
branch explicitly; it is not enabled by this plain manifest checkout.
