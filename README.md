# xzwz1 OpenWrt Plugin Feed

Pinned third-party packages for the AX3600 NSS firmware builder.

## Packages

- `luci-app-openclash` — OpenClash v0.47.116, built from the upstream tagged source archive.
- `openclash-core` — Mihomo v1.19.28 for Linux ARM64, installed as `/etc/openclash/core/clash_meta`.

All downloads are version-pinned and SHA-256 verified. OpenClash is disabled by default and ships without subscriptions or user configuration.

## Feed usage

```text
src-git xzwz_packages https://github.com/xzwz1/openwrt-packages.git;main
```

This repository contains packaging metadata only; upstream application development remains in [vernesong/OpenClash](https://github.com/vernesong/OpenClash) and [MetaCubeX/mihomo](https://github.com/MetaCubeX/mihomo).
