
# local_manifests

Local manifest for building **PixelOS** (Android 17) for the **Xiaomi 12S Pro (unicorn, sm8450)** with the **6.6 kernel** from cupid-development.

## What's inside

`unicorn_6.6.xml` syncs:

- **Kernel 6.6:** kernel, devicetrees, modules and build (`cupid-development`, branch `lineage-24.0-6.6`)
- **Device / vendor:** `sm8450-common` and `unicorn` (`cupid-development`, branch `lineage-24.0-6.6`)
- **Qualcomm CAF HAL:** display and audio-ar for sm8450 6.6
- **hardware/xiaomi:** LineageOS, branch `lineage-24.0`
- **hardware/dolby:** Evolution-X-Devices, branch `cnb-aidl` (AIDL)

## Usage

Run everything from the root of your PixelOS source, synced from the [PixelOS manifest](https://github.com/PixelOS-AOSP/android_manifest) (branch `seventeen`).

**1. Init the PixelOS source (skip if already done)**

```bash
repo init -u https://github.com/PixelOS-AOSP/android_manifest -b seventeen
```

**2. Clone this repo as your local manifests**

```bash
git clone https://github.com/hoainamvip/local_manifests .repo/local_manifests
```

**3. Sync the source**

```bash
repo sync -c --no-tags --force-sync -j8
```

**4. Set up the build environment**

```bash
source build/envsetup.sh
```

**5. Replace lineage_unicorn with custom_unicorn**

The unicorn device tree ships as `lineage_unicorn`. For PixelOS, rename it to `custom_unicorn`.

Go to the device tree:

```bash
cd device/xiaomi/unicorn
```

Rename the product makefile:

```bash
mv lineage_unicorn.mk custom_unicorn.mk
```

Replace the product name:

```bash
sed -i 's/lineage_unicorn/custom_unicorn/g' custom_unicorn.mk AndroidProducts.mk
```

Inherit the PixelOS common config instead of Lineage:

```bash
sed -i 's#vendor/lineage/config/common_full_phone.mk#vendor/custom/config/common_full_phone.mk#' custom_unicorn.mk
```

Go back to the source root:

```bash
cd ../../..
```

`repo sync` resets the device tree, so repeat this step after every sync.

**6. Pick the device**

```bash
breakfast unicorn
```

**7. Build**

```bash
m pixelos
```

## Notes

- The manifest includes `manifests/snippets/kernel-6.6.xml`, which must exist in your PixelOS manifest.
- Do not declare the same project paths in another local manifest.
- Dolby: make sure the device tree inherits `hardware/dolby/dolby.mk` and that `DEVICE_MANIFEST_FILE` and `DEVICE_FRAMEWORK_COMPATIBILITY_MATRIX_FILE` only use `+=`.

## Credits

- [PixelOS-AOSP](https://github.com/PixelOS-AOSP)
- [cupid-development](https://github.com/cupid-development)
- [LineageOS](https://github.com/LineageOS)
- [Evolution-X-Devices](https://github.com/Evolution-X-Devices)
