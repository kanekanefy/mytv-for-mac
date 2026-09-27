# 更新日志

## 1.0.0

首个对外分享版本。

**核心功能**
- IPTV 直播播放：m3u/m3u8/txt 订阅源，同名频道多线路合并，libmpv 硬解（VideoToolbox），1080i 自动去隔行
- EPG 节目单、频道台标、收藏、数字选台
- 本机实时翻译字幕：系统 SpeechAnalyzer 语音识别 + 本地 GGUF 模型翻译（llama-server，Metal 加速），支持同传模式（画面延后对齐）、双语字幕、按频道自动语种判断
- 模型对比/盲评模式
- 可选「国际纪实 / 外语台」附加源（默认关闭）

**发布相关**
- App 完全自包含：mpv/FFmpeg 及全部依赖、本地翻译运行时（llama-server + ggml Metal/CPU 后端）均已打包进 .app，不依赖本机 Homebrew 安装
- 翻译模型不随包分发，首次使用在 App 内下载
- ad-hoc 签名（无 Apple Developer ID 公证），首次打开需要手动放行一次，见 README「安装」
