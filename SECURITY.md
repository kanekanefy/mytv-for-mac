# 安全策略

## 支持的版本

只有 [Releases](../../releases) 里最新发布的版本会收到安全相关的修复。请始终使用最新版本。

## 报告安全问题

本仓库不含源代码（只分发编译好的 `.dmg`），所以能报告的安全问题主要是这几类：

- 下载到的安装包被篡改，或校验和（SHA-256，见对应 Release 页面）不一致
- App 打包的第三方运行时/依赖（见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)）已知存在漏洞
- App 本身的行为表现出明显的隐私/安全隐患（例如意外联网、意外写入不该访问的位置）

**请不要在公开 Issue 里贴具体的利用细节。** 优先用本仓库 Security 标签页下的「Report a vulnerability」私密提交；如果你在 Security 标签页看不到这个选项（说明还没启用），改用一个措辞克制、不含细节的 Issue（比如"发现一个安全相关问题，请私下联系我"），我们会尽快跟进并转为私下沟通。

## 响应时间

这是个人维护的项目，不保证 SLA，但会尽量在几天内回应。修复后会在下一个 Release 的更新日志里说明（不一定会公开披露完整细节，取决于影响面）。

---

# Security Policy

## Supported versions

Only the latest release on the [Releases](../../releases) page receives security-related fixes. Please always run the latest version.

## Reporting a vulnerability

This repository has no source code (it only distributes a compiled `.dmg`), so reportable security issues mainly fall into these categories:

- A downloaded installer that appears tampered with, or a checksum (SHA-256, listed on the relevant Release page) that doesn't match
- A known vulnerability in a bundled third-party runtime/dependency (see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md))
- App behavior that shows a clear privacy/security concern (e.g. unexpected network access, writing to somewhere it shouldn't)

**Please do not post exploit details in a public Issue.** Prefer this repository's Security tab → "Report a vulnerability" for a private submission. If that option isn't available (meaning it hasn't been enabled yet), open a low-detail Issue instead (e.g. "found a security issue, please contact me privately") and we'll follow up privately.

## Response time

This is a personally maintained project with no formal SLA, but reports are usually acknowledged within a few days. Fixes are noted in the changelog of the next release (full disclosure details depend on the impact).
