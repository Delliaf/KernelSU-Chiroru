# KernelSU-Next for Chiroru

Fork of [KernelSU-Next](https://github.com/KernelSU-Next/KernelSU-Next) for the
Yandex Station Duo Max (`chiron`). The `chiron` branch is based on upstream
[`v3.4.0-legacy`](https://github.com/KernelSU-Next/KernelSU-Next/commit/8af3d4fec33be32fa5d3f8dae4f380fac45bf2cd),
with the adaptation used by [Chiroru](https://github.com/klockky/Chiroru).

## Changes

- Vendor Linux 5.4 compatibility and exact-profile symbol resolution.
- Transactional SELinux policy updates and vendor policy ABI adapters.
- UAPI 5 service lifecycle handling and root-domain handoff.
- Late loading through Chiroru without writing boot partitions.

The initial adaptation is imported from Chiroru `1dd43d0`, preserving the
tested source contents apart from the include path for upstream's root `uapi/`
directory. Factory-specific adjustments remain in Chiroru's
`tools/factory/kernel.patch` and are applied by its build tool.

## Build

Chiroru pins this fork as `third_party/kernelsu`. Its build tool selects the
firmware profile, compatibility flags and factory patch together:

```sh
git clone --recurse-submodules https://github.com/klockky/Chiroru.git
cd Chiroru
python3 tools/build-kernel-modules.py 5000001289 /path/to/prepared-kernel /path/to/new-output --module ksu
```

See [build requirements and checks](https://github.com/klockky/Chiroru/blob/main/tools/KERNEL_MODULES.md).

GPL-2.0; see [LICENSE](LICENSE), [kernel/LICENSE](kernel/LICENSE) and individual
file headers. Upstream history and copyright notices are preserved.
