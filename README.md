# local_manifests

Local manifest for building **LunarisAOSP** (Android 16) for the **Xiaomi 12S Pro (unicorn, sm8450)**.

## Usage

**1. Clone this repo as your local manifests**

```bash
git clone -b lunaris-16 https://github.com/hoainamvip/local_manifests .repo/local_manifests
```

**2. Sync the source**

```bash
repo sync -c --no-tags --force-sync -j$(nproc --all)
```

## Updating

**1. Pull the latest manifest**

```bash
git -C .repo/local_manifests pull
```

**2. Sync again**

```bash
repo sync -c --no-tags --force-sync -j$(nproc --all)
```
