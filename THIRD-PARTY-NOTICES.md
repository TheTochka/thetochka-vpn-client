# Third-party notices

This file lists third-party software used by the **open VPN client / engine** in this repository (the Apple client based on sing-box for Apple, plus Libbox). It is not a list of libraries used by the closed TheTochka marketplace application.

## GNU GPLv3 (copyleft)

### This repository (Apple client fork)

- Project: TheTochka VPN Client, based on sing-box for Apple
- Upstream: https://github.com/SagerNet/sing-box-for-apple
- License: GNU General Public License v3.0 or later
- Copyright: Copyright (C) 2022 by nekohasekai &lt;contact-sagernet@sekai.icu&gt;
- Additional modifications: TheTochka contributors (see [DIFFERENCES.md](DIFFERENCES.md))
- Full text: [LICENSE](LICENSE)

### sing-box / Libbox

- Project: sing-box (universal proxy platform) and its mobile library Libbox
- Source: https://github.com/SagerNet/sing-box
- License: GNU General Public License v3.0 or later (and additional notices in that tree, including BSD-3-Clause for some files)
- Copyright: Copyright (C) 2022 by nekohasekai &lt;contact-sagernet@sekai.icu&gt;

The App Store binary of TheTochka links **Libbox**. Corresponding Source for that library is the sing-box tree used to run:

```bash
go run ./cmd/internal/build_libbox -target apple
```

A full `go-licenses` report belongs with that sing-box checkout at the matching module version, not with this Swift tree.

## Swift Package Manager dependencies (Apple client)

These pins come from `sing-box.xcodeproj` / `Package.resolved` in this fork. They are used by the full SFI/SFM/SFT client. The TheTochka store tunnel uses a smaller subset (primarily Libbox + GRDB for profiles). License text is in each upstream repository.

| Package | Source | Typical license (confirm in upstream) |
| --- | --- | --- |
| BinaryCodable | https://github.com/christophhagen/BinaryCodable | MIT |
| LegacyBinaryCodable | https://github.com/christophhagen/LegacyBinaryCodable | MIT |
| GRDB.swift | https://github.com/groue/GRDB.swift | MIT |
| DeviceKit | https://github.com/devicekit/DeviceKit | MIT |
| NetworkImage | https://github.com/gonzalezreal/NetworkImage | MIT |
| swift-markdown-ui | https://github.com/gonzalezreal/swift-markdown-ui | MIT |
| swift-collections | https://github.com/apple/swift-collections | Apache-2.0 |
| qrcode | https://github.com/dagronf/qrcode | MIT |
| swift-qrcode-generator | https://github.com/dagronf/swift-qrcode-generator | Apache-2.0 / MIT (see repo) |
| SwiftImageReadWrite | https://github.com/dagronf/SwiftImageReadWrite | MIT |
| PLCrashReporter | https://github.com/microsoft/plcrashreporter | MIT AND Apache-2.0 |
| CodeEditSourceEditor | https://github.com/nekohasekai/CodeEditSourceEditor | MIT |
| CodeEditTextView | https://github.com/CodeEditApp/CodeEditTextView | MIT |
| CodeEditLanguages | https://github.com/CodeEditApp/CodeEditLanguages | MIT |
| CodeEditSymbols | https://github.com/CodeEditApp/CodeEditSymbols | MIT |
| SwiftTreeSitter | https://github.com/ChimeHQ/SwiftTreeSitter | MIT |
| tree-sitter | https://github.com/tree-sitter/tree-sitter | MIT |
| Rearrange | https://github.com/ChimeHQ/Rearrange | MIT |
| TextFormation | https://github.com/ChimeHQ/TextFormation | BSD-3-Clause |
| TextStory | https://github.com/ChimeHQ/TextStory | BSD-3-Clause |
| swift-cmark | https://github.com/swiftlang/swift-cmark | BSD-2-Clause / others (see repo) |
| libghostty-spm | https://github.com/Lakr233/libghostty-spm | see upstream |
| MSDisplayLink | https://github.com/Lakr233/MSDisplayLink | see upstream |
| SwiftLintPlugin | https://github.com/lukepistrol/SwiftLintPlugin | MIT (build-time) |

SQLite (via GRDB) is public domain / blessing license as published by sqlite.org.

## Runtime rule-sets (not compiled into the binary)

If Russian bypass routing is enabled, the engine may download public sing-box rule-set binaries from:

- https://github.com/runetfreedom/russia-v2ray-rules-dat

Those files are third-party data, not TheTochka source. Their license is defined by that project.

## Trademarks

“TheTochka” and related logos are trademarks of their owners and are **not** licensed under GPLv3.

“sing-box” and SagerNet names and marks belong to their owners. This fork is **based on** sing-box for Apple and is **not** an official SagerNet product.
