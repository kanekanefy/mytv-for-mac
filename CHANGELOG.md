# 更新日志

本文件记录每个发布版本的变更。格式参考 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，版本号遵循 [Semantic Versioning](https://semver.org/lang/zh-CN/)。

## [未发布]

暂无。

## [1.0.1] - 2026-09-29

### Fixed

- 修复添加某些订阅源后 App 一启动就闪退：同一分组里有名字相近、会被识别为同一台的频道时，合并逻辑越界
- 修复实时翻译的长句被截断成「…」：一次识别到多句话时，超长译文现在会拆成几条字幕依次显示，每条最多两行
- 同一个附加订阅源被重复添加时自动去重

### Changed

- 字幕字号改为按视频画面高度等比缩放，去掉原来 40pt 的上限：窗口小字就小，全屏或外接大屏时字会跟着变大

### Added

- 翻译设置里新增「字幕大小」：小 / 标准 / 大 / 特大，远距离看电视时可以选大一档

## [1.0.0] - 2026-09-27

首个对外分享版本。

### Added

- IPTV 直播播放：m3u/m3u8/txt 订阅源，同名频道多线路合并，libmpv 硬解（VideoToolbox），1080i 自动去隔行
- EPG 节目单、频道台标、收藏、数字选台
- 本机实时翻译字幕：系统 SpeechAnalyzer 语音识别 + 本地 GGUF 模型翻译（llama-server，Metal 加速），支持同传模式（画面延后对齐）、双语字幕、按频道自动语种判断
- 模型对比/盲评模式
- 可选「国际纪实 / 外语台」附加源（默认关闭）

### 发布相关

- App 完全自包含：mpv/FFmpeg 及全部依赖、本地翻译运行时（llama-server + ggml Metal/CPU 后端）均已打包进 .app，不依赖本机 Homebrew 安装
- 翻译模型不随包分发，首次使用在 App 内下载
- ad-hoc 签名（无 Apple Developer ID 公证），首次打开需要手动放行一次，见 README「安装」

[未发布]: https://github.com/kanekanefy/mytv-for-mac/compare/v1.0.1...HEAD
[1.0.1]: https://github.com/kanekanefy/mytv-for-mac/releases/tag/v1.0.1
[1.0.0]: https://github.com/kanekanefy/mytv-for-mac/releases/tag/v1.0.0
