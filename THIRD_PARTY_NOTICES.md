# 第三方组件声明

「我的电视」的可执行文件（.app）中静态/动态链接或运行时调用了以下第三方开源组件。此文件只列出直接可见、体量较大的组件；每个库自身还有一批更小的传递依赖（编解码、字体渲染、压缩等），未逐一列出，但都遵循各自 Homebrew 配方标注的开源许可证。

本仓库不包含源代码，只分发编译好的二进制（.app / .dmg）。

## 播放内核

| 组件 | 版本 | 许可证 | 项目地址 |
|---|---|---|---|
| mpv (libmpv) | 0.41.0 | GPL-2.0-or-later AND LGPL-2.1-or-later | https://mpv.io |
| FFmpeg（libavcodec / libavformat 等） | 9.0.1 | GPL-3.0-or-later（本构建启用了 `--enable-gpl --enable-libx264 --enable-libx265`） | https://ffmpeg.org |
| x264 | r3222 | GPL-2.0-or-later | https://www.videolan.org/developers/x264.html |
| x265 | 4.3 | GPL-2.0-or-later | https://www.x265.org |
| libass（字幕渲染） | 0.17.5 | ISC | https://github.com/libass/libass |
| libplacebo（视频渲染管线） | 7.360.1 | LGPL-2.1-or-later | https://code.videolan.org/videolan/libplacebo |

其余随 mpv/FFmpeg 一并打包的库（libdav1d、libvpx、libopus、libmp3lame、SvtAv1Enc、libbluray、libarchive、libfontconfig、libfreetype、libfribidi、libharfbuzz、libmujs、liblcms2、librubberband、libsamplerate、libshaderc_shared、libvulkan、libvmaf、libzimg、libuchardet、libudfread 等）分别遵循 BSD / MIT / LGPL / ISC 等许可证，具体以各自项目仓库为准。

## 本地翻译推理

| 组件 | 版本 | 许可证 | 项目地址 |
|---|---|---|---|
| llama.cpp（llama-server） | 0.5.0 | MIT | https://github.com/ggml-org/llama.cpp |
| ggml（含 Metal/CPU/BLAS 推理后端） | 0.25.3 | MIT | https://github.com/ggml-org/ggml |
| OpenSSL（libssl/libcrypto，llama-server 的运行时依赖） | 3.x | Apache-2.0 | https://openssl.org |

翻译模型本身不随 App 分发，由用户在设置页的「模型库」按需下载；每个模型条目在界面里标注了各自的许可证（如 Apache-2.0）。

## 系统能力

语音识别使用 Apple 系统框架 `Speech` / `SpeechAnalyzer`（macOS 26），文本翻译可选使用系统框架 `Translation`；这些是 macOS 自带能力，不随 App 分发额外二进制。

## 设计与功能参考

本项目的功能定位参考了安卓开源项目 [yaoxieyoulei/mytv-android](https://github.com/yaoxieyoulei/mytv-android)（MIT 协议），但本项目是使用 Swift / SwiftUI / libmpv 从零重写的 macOS 原生实现，未复制其源代码；图标与界面素材为本项目原创绘制。

## 公开数据源

- 默认订阅源预设：[vbskycn/iptv](https://github.com/vbskycn/iptv)、[Guovin/iptv-api](https://github.com/Guovin/iptv-api)、[iptv-org/iptv](https://github.com/iptv-org/iptv) —— 均为公开维护的 IPTV 频道列表项目
- 可选「国际纪实 / 外语台」附加源：取自 [iptv-org/iptv](https://github.com/iptv-org/iptv) 的公开流列表，默认关闭
- EPG 节目单预设：e.erw.cc / 51zmt / 112114，均为公开 EPG 服务
