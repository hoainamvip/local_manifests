# local_manifests

Local manifest for building Android 17 (Evolution X) for the **Xiaomi 12S Pro (unicorn, sm8450)** with the **6.6 kernel** from cupid-development.

## What's inside

`unicorn_6.6.xml` syncs:

- **Kernel 6.6:** kernel, devicetrees, modules and build (`cupid-development`, branch `lineage-24.0-6.6`)
- **Device / vendor:** `sm8450-common` and `unicorn` (`cupid-development`, branch `lineage-24.0-6.6`)
- **Qualcomm CAF HAL:** display and audio-ar for sm8450 6.6
- **hardware/xiaomi:** LineageOS, branch `lineage-24.0`
- **hardware/dolby:** Evolution-X-Devices, branch `cnb-aidl` (AIDL)

## Usage

Run everything from the root of your ROM source.

1. Clone this repo as your local manifests:

```bash
git clone https://github.com/hoainamvip/local_manifests .repo/local_manifests
```

2. Sync the source:

```bash
repo sync -c --no-tags --force-sync -j8
```

3. Set up the build environment:

```bash
source build/envsetup.sh
```

4. Pick the device:

```bash
breakfast unicorn
```

5. Build:

```bash
m evolution
```

## Updating

1. Pull the latest manifest:

```bash
git -C .repo/local_manifests pull
```

2. Sync again:

```bash
repo sync -c --no-tags --force-sync -j8
```

## Notes

- The manifest includes `manifests/snippets/kernel-6.6.xml`, which must exist in your ROM manifest.
- Do not declare the same project paths in another local manifest.
- Dolby: make sure the device tree inherits `hardware/dolby/dolby.mk` and that `DEVICE_MANIFEST_FILE` and `DEVICE_FRAMEWORK_COMPATIBILITY_MATRIX_FILE` only use `+=`.

## Credits

- [cupid-development](https://github.com/cupid-development)
- [LineageOS](https://github.com/LineageOS)
- [Evolution-X-Devices](https://github.com/Evolution-X-Devices)
