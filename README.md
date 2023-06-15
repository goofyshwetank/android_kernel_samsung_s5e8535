# Kernel Source — Samsung Exynos 1330 (s5e8535)

Kernel source for the Samsung Exynos 1330 (s5e8535) SoC, used in the
Samsung Galaxy F14 5G (SM-E146B, codename m14x) and related devices.

---

## Target Device

| Field | Value |
|---|---|
| Device | Samsung Galaxy F14 5G (SM-E146B) |
| Codename | m14x |
| SoC | Samsung Exynos 1330 (s5e8535) |
| Architecture | arm64 |
| Defconfig | `s5e8535-m14xnsxx_defconfig` |
| Kernel type | GKI 2.0 — boot header v4 |
| Boot image | `vendor_boot` + `init_boot` (generic `boot.img`) |

---

## Building

```bash
export ARCH=arm64
export CROSS_COMPILE=aarch64-linux-android-

make s5e8535-m14xnsxx_defconfig

# Build with Clang (recommended)
make -j$(nproc) LLVM=1 LLVM_IAS=1
```

The GKI `boot.img` is built separately from AOSP; this tree produces only
`vendor_boot.img` content (vendor modules, DTBs, vendor ramdisk).

---

## GKI Notes

This kernel follows the GKI 2.0 model:

- The generic `boot.img` ramdisk comes from AOSP (android15-6.6 common kernel)
- Samsung-specific drivers are in `vendor_boot` as vendor modules (`*.ko`)
- `init_boot.img` carries the generic first-stage init
- No `recovery` partition — recovery is handled by `vendor_boot` ramdisk

---

## Related Repositories

- [android_device_samsung_m14x](https://github.com/goofyshwetank/android_device_samsung_m14x) — Device tree
- [android_vendor_samsung_m14x](https://github.com/goofyshwetank/android_vendor_samsung_m14x) — Vendor blobs
