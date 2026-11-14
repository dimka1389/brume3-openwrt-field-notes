# Brume 3 / GL-MT5000: OpenWrt field notes

[Русский](README.ru.md) · [Latest test report](docs/2026-11-14.en.md) · [Report a problem](https://github.com/dimka1389/brume3-openwrt-field-notes/issues/new/choose) · [Discussions](https://github.com/dimka1389/brume3-openwrt-field-notes/discussions)

Independent, bilingual field notes from one retail GL.iNet Brume 3 running an experimental OpenWrt build. The purpose is to make observations reproducible and useful to other testers and upstream developers.

This repository contains documentation, not a firmware distribution. It is not an official OpenWrt, GL.iNet or StealthSurf project. One working installation is not evidence that an image is safe for every device.

## Tested baseline

| Component | Observed on 2026-11-14 |
|---|---|
| Device | GL.iNet GL-MT5000 / Brume 3 |
| Target | `mediatek/filogic`, `aarch64_cortex-a53` |
| Build identifier | OpenWrt SNAPSHOT `r0-1713e8b` |
| Source base | `GLiNet-Tech/openwrt`, commit `1713e8be63b628fe2f1d336f4fb3a8aa152875af` |
| Kernel | Linux `6.18.60` |
| Firewall | fw4 / nftables |
| Connectivity exercised | Existing IPv4 PPPoE connection, LAN, DNS, SSH, LuCI, transparent VPN |
| StealthSurf | Manually updated from `1.0.101` to `1.0.106` |
| System package maintenance | 26 packages updated in checked batches; kernel, libc and build-specific base-files pins retained |

The device had approximately six days of uptime before maintenance. The firmware image and kernel were not replaced. One user-authorized reboot after the package changes passed: SSH returned, the new procd executable ran, PPPoE reconnected and StealthSurf connected automatically. Direct and VPN HTTPS probes passed. Power-loss recovery and long-term operation remain untested.

## Findings

- Repeated scheduled StealthSurf update attempts stopped the application; a previously installed local watchdog brought it back. Manual invocation of the official installer outside the application's service completed successfully.
- A standard OpenWrt configuration backup did not include this installation's StealthSurf account/settings directory. A separate private backup was required.
- The previous verbose Xray log stopped growing close to 8 MiB. Logging resumed after the application update/restart. A log-rotation `Bad file descriptor` message was also observed; its cause is unresolved.
- Direct and VPN HTTPS probes passed after each package group. Full application use, streaming, failover, IPv6, LAN-to-LAN switching and sustained throughput are not established by these probes.

See the [full report](docs/2026-11-14.en.md), [test matrix](docs/test-matrix.md), [package version table](docs/packages-2026-11-14.md) and [privacy rules](PRIVACY.md).

## Upstream and credits

- Device support: [OpenWrt PR #24237](https://github.com/openwrt/openwrt/pull/24237), still open when checked on 2026-11-14. Device support and kernel work belong to the upstream contributors, not this notes repository.
- Source branch: [GLiNet-Tech/openwrt](https://github.com/GLiNet-Tech/openwrt/tree/mt5000).
- StealthSurf requirements and installation: [official router documentation](https://stealthsurf.net/routers).
- [Official OpenWrt downloads](https://downloads.openwrt.org/) and [firmware selector](https://firmware-selector.openwrt.org/).

Links provide attribution and context; they do not automatically notify maintainers or imply endorsement. Reports here should distinguish a device-driver issue from a VPN application or provider issue.

Field testing and editorial decisions: the device owner. Diagnostics and drafting: assisted by Codex. This is a collaboration on testing and documentation, not a claim of authorship of upstream firmware or third-party software.

## Participate

Use [Issues](https://github.com/dimka1389/brume3-openwrt-field-notes/issues/new/choose) for a specific reproducible problem and [Discussions](https://github.com/dimka1389/brume3-openwrt-field-notes/discussions) for questions and comparisons. Russian and English reports are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) first.

No personal image, backup, private configuration or subscription is published. A reusable firmware image would need a separate clean build, removal of all embedded credentials and per-device data, reproducible build information and recovery testing. Do not flash someone else's personal backup.

[Clean build starting point](docs/clean-build.md) — no downloadable image yet.
