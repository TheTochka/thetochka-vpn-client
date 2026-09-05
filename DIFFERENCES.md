# Differences from upstream

This repository is a fork of [sing-box for Apple](https://github.com/SagerNet/sing-box-for-apple) (SagerNet / nekohasekai).

TheTochka VPN: VPN Marketplace ships an embedded VPN engine built from **this fork**, not from an unmodified upstream checkout. The marketplace app (catalog, accounts, payments, backend) is **not** in this repository.

App Store / TestFlight mapping:

| Marketplace app | This repository | Notes |
| --- | --- | --- |
| Version `2.0.0` (build `95`) | Git tag `v2.0.0+build.95` | **Current / active** |
| Version `2.0.0` (build `94`) | Git tag `v2.0.0+build.94` | Intermediate TestFlight |
| Version `2.0.0` (build `93`) | Git tag `v2.0.0+build.93` | Intermediate TestFlight |
| Version `2.0.0` (build `86`) | Git tag `v2.0.0+build.86` | Earlier snapshot |

Upstream remains the SagerNet project. TheTochka is not affiliated with or endorsed by SagerNet.

## Exact sources used in the App Store binary

Directory `TheTochkaEngine/` is the Network Extension + Libbox client library as compiled into `com.direct.thetochka` / `SingBoxPacketTunnel`.

- `TheTochkaEngine/Library/` — Swift library that talks to Libbox and the packet tunnel
- `TheTochkaEngine/PacketTunnel/` — Packet Tunnel Provider used in the store binary

The same Library files are also applied onto `Library/` in this fork so the GPL tree is not split from the Apple client project.

Not published here (proprietary marketplace): Flutter UI, catalog, payments, backend, partner APIs.

## Added files (not in upstream Library)

These files exist only in the TheTochka engine snapshot:

- `Library/Service/DailyTrafficStore.swift` — local daily traffic counters
- `Library/Service/RussianBypassRouting.swift` — optional RU→`direct` rule-sets (public geosite/geoip URLs)
- `Library/Service/SingBoxConfigMigrator.swift` — config migration helpers
- `Library/Service/SubscriptionConfigBuilder.swift` — normalize subscription payloads to sing-box JSON
- `Library/Service/SubscriptionHTTP.swift` — subscription HTTP fetch / User-Agent
- `Library/Service/SubscriptionMetadata.swift` — subscription header metadata
- `Library/Service/VLESSConfigBuilder.swift` — `vless://` share-link import

## Modified upstream Library files

Relative to SagerNet/sing-box-for-apple `Library/` (this fork’s parent):

- `Library/Shared/Variant.swift` — application name `TheTochka` instead of SFI/SFM/SFT
- `Library/Shared/AppConfiguration.swift` — Packet Tunnel bundle suffix `.SingBoxPacketTunnel`; team identifier used by the store app
- `Library/Shared/BlockingIO.swift` — dispatch queue label
- `Library/Network/HTTPClient.swift` — User-Agent identifies TheTochka
- `Library/Database/*` — profile / preferences subset used by the marketplace tunnel
- `Library/Network/Extension*.swift`, `CommandClient.swift`, and related tunnel/XPC files — trimmed to the code path compiled into TheTochka (no Tailscale/editor-only paths from full SFI)
- `Library/Update/GitHubUpdateChecker.swift` — still compares against SagerNet/sing-box releases for engine versioning

`Extension/PacketTunnelProvider.swift` in the full Apple client is unchanged (`ExtensionProvider` subclass). The store tunnel wrapper and entitlements live in `TheTochkaEngine/PacketTunnel/` (`group.com.direct.thetochka`).

## What we did not copy from the marketplace app

- Flutter / Dart sources
- `VpnEnginePlugin.swift` (Flutter method channel; not required to build SFI from this repo)
- Production backend URLs, payment keys, partner credentials

## How to rebuild Libbox

From [sing-box](https://github.com/SagerNet/sing-box) sources matching the Libbox version linked into the app:

```bash
go run ./cmd/internal/build_libbox -target apple
```

Place `Libbox.xcframework` next to `sing-box.xcodeproj`, then build scheme **SFI** (or the TheTochka Packet Tunnel target in the marketplace Xcode project) with your own Apple ID.
