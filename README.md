# HonorHook

荣耀（MagicOS）系统应用净化 / 指定应用会员态 LSPosed 模块，基于 libxposed API 102。

一个 APK 两个运行面：hook 侧注入作用域内的荣耀系统应用进程，只改内存态、不动系统文件；UI 侧是配置面板，各功能开关经远端 prefs 下发。功能默认全开，改开关后**下次注入才生效**。

## 能做什么

**系统应用净化**

- 主题商店（`com.hihonor.android.thememanager`）：VIP 状态收口、资源免费化、试用无倒计时、广告槽位与底部推广 tab 源头裁剪、下载链走 VIP 通道、动态壁纸应用修复。
- 包管理器（`com.android.packageinstaller`）：不请求广告与 AB 实验、安装页广告与推广卡不展示、三方跳转不拦截、跳过联网安全检测（无「网络不佳」横幅、无风险拦截页）、不提示开启安全模式。
- 短信（`com.hihonor.mms`）：推广卡片统一清除。
- 设置（`com.android.settings`）：应用详情页「停用」按钮恒可点（荣耀对管控应用置灰）。
- SystemUI：隐藏副卡（SIM2）状态栏信号图标，≥2 卡才生效，快捷设置瓷贴不受影响。
- 系统桌面（`com.hihonor.android.launcher`）：隐藏 YOYO 卡片堆叠标题文本，应用图标名保留。
- 系统更新（`com.hihonor.ouc`）：禁掉后台自动检测、WiFi 自动下载、夜间安装、升级提醒通知等自动触发链，**手动检查更新保留**。
- 升级引导（`com.hihonor.android.upgradeguide`）：「发现新版本」全屏引导页闪现即退，引导流程无法展开。

**荣耀系应用通杀**

- 埋点通杀：拦截荣耀埋点 SDK（`com.hihonor.hianalytics`）的上报链路，事件不落库、不出网。覆盖浏览器、日历、天气、游戏中心、视频、云音乐等应用。
- 广告 SDK 通杀：荣耀系统广告 SDK（`com.hihonor.adsdk`）的信息流、横幅、开屏、插屏、激励全形态在渲染层短路。
- 日历运营推荐位：日历服务卡 / 资讯推荐位（`com.hihonor.osoperationsdk`）整链收口。
- 搜狗键盘（荣耀版，`com.sohu.inputmethod.sogou.honor`）：候选区功能免同意开启。

**指定应用会员态**

- 成人高考题库（`com.exam8.chengrenGK`）：会员档位、有效期、特权等级伪造为超级会员，「阅后即焚」特权 UI 门放行。

## 环境要求

- 荣耀 / MagicOS 设备，已 root。
- LSPosed 等支持 libxposed API 102 的框架。

## 安装

1. 安装本页 Release 里的 APK。
2. 在 LSPosed 中启用 HonorHook——模块自带静态作用域声明，按 LSPosed 提示把全部作用域勾上即可，无需手改。
3. 强停并重新打开对应应用（或重启系统）让 hook 注入生效。
4. 打开 HonorHook 面板，确认各目标状态，按需调整开关。

## 使用

- 配置面板按目标分页，每项功能独立开关，默认全开。
- 开关改动写入远端 prefs，**下次注入才生效**——改完记得强停对应应用。
- 某功能失效时看 LSPosed 框架日志的 `installed N/M` 汇总行：未命中挂载点会自动跳过，不影响其余功能。

## 注意

- 宿主应用 OTA 更新会更换混淆名，个别挂载点可能随之失效；模块按「检索不到自动跳过」设计，等适配即可。
- 适配基线：主题商店 20.1.63.305、包管理器 14.0.37.301、桌面 18.0.0.234、题库 5.9.0.0、系统更新 18.0.3.206。
- 题库「阅后即焚」的试卷正文由服务端按订单态下发，模块只能通过 UI 门，取不到正文。
- 停用管控应用的执行层受 system_server 保护，本模块不处理。

源码与构建说明见 [HonorHook](https://github.com/coderstory/HonorHook)。
