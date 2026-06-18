# QwenPaw Android APP

<p align="center">
  <img src="https://img.shields.io/badge/Flutter-3.44.2-02569B?logo=flutter" alt="Flutter"/>
  <img src="https://img.shields.io/badge/Android-8.0%2B-3DDC84?logo=android" alt="Android"/>
  <img src="https://img.shields.io/badge/Dart-3.12.2-0175C2?logo=dart" alt="Dart"/>
  <img src="https://img.shields.io/github/v/release/R3lyW1nd/QwenPaw-Android-APP" alt="Release"/>
  <img src="https://img.shields.io/github/license/R3lyW1nd/QwenPaw-Android-APP" alt="License"/>
</p>

<p align="center">
  <b>让你的 QwenPaw Agent 随身而行</b> —— 功能丰富的 Android 客户端，通过 REST API 实现与 AI 助手的实时对话。
</p>

---

## 目录

- [功能特性](#-功能特性)
- [截图预览](#-截图预览)
- [技术栈](#-技术栈)
- [项目架构](#-项目架构)
- [使用说明](#-使用说明)
- [API 对接说明](#-api-对接说明)
- [注意事项](#-注意事项)
- [许可证](#-许可证)

---

## 功能特性

| 功能 | 说明 |
|------|------|
| 实时对话 | SSE 流式响应，打字机效果实时显示 AI 回复，支持工具调用结果展示 |
| 多 Agent 切换 | 支持切换不同智能体角色，每个 Agent 独立上下文管理 |
| 文件管理 | 查看 / 下载工作空间文件，工具调用产生的文件自动展示 |
| 数据统计 | Token 消耗统计、API 调用次数追踪、历史趋势分析 |
| 定时任务 | 查看和管理 Cron 定时任务状态 |
| 主题系统 | 浅色 / 深色 / 跟随系统 三种模式 + 6 种强调色 |
| 离线缓存 | 消息本地持久化存储，断网可查看历史记录 |
| 全局搜索 | 关键词搜索历史消息，快速定位 |
| 会话管理 | 新建 / 切换 / 删除会话，全屏历史浏览 |
| 分页加载 | 聊天历史支持无限滚动分页加载 |
| 自动刷新 | 连接状态变化时自动刷新数据 |
| 崩溃捕捉 | 应用异常自动捕捉并记录 |

## 截图预览

<div align="center">

| | | | |
|---|---|---|---|
<img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_1.jpg' width='170'/> | <img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_2.jpg' width='170'/> | <img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_3.jpg' width='170'/> | <img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_4.jpg' width='170'/> |
<img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_5.jpg' width='170'/> | <img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_6.jpg' width='170'/> | <img src='https://raw.githubusercontent.com/R3lyW1nd/QwenPaw-Android-APP/main/screenshots/screenshot_7.jpg' width='170'/> | |

</div>

## 技术栈

| 类别 | 技术 |
|------|------|
| 框架 | Flutter 3.44.2 (Dart 3.12.2) |
| UI 框架 | Material 3 + Cupertino 混合设计 |
| 状态管理 | Provider + Riverpod |
| HTTP 客户端 | Dio (REST API) |
| SSE 流式解析 | 基于 Dio 的自定义 SSE 解析器 |
| 本地存储 | SharedPreferences + 文件缓存 |
| 主题系统 | Material 3 动态颜色 + 自定义主题引擎 |
| 最低 SDK | Android 8.0 (API 26) |
| 构建工具 | Gradle 9.1.0 + AGP 9.0.1 |

## 项目架构

```
qwenpaw_app/
├── lib/
│   ├── main.dart                          # 应用入口 + 主题配置
│   ├── config/
│   │   └── theme.dart                     # 主题定义（浅色/深色 + 6 强调色）
│   ├── models/
│   │   ├── agent_info.dart                # Agent 信息模型
│   │   ├── cron_job.dart                  # 定时任务模型
│   │   ├── message.dart                   # 消息模型
│   │   ├── skill_model.dart               # 技能模型
│   │   ├── token_stats.dart               # Token 统计模型
│   │   └── workspace_file.dart            # 工作空间文件模型
│   ├── services/
│   │   ├── qwenpaw_api.dart               # API 层（60+ 端点）
│   │   ├── qwenpaw_service.dart           # 业务逻辑层
│   │   ├── message_cache.dart             # 离线消息缓存
│   │   └── crash_reporter.dart            # 崩溃捕捉
│   ├── providers/
│   │   ├── api_provider.dart              # API 连接管理
│   │   ├── chat_provider.dart             # 聊天状态管理
│   │   ├── connection_provider.dart       # 连接状态管理
│   │   └── data_providers.dart            # 数据层 Provider
│   ├── screens/
│   │   ├── main_screen.dart               # 主界面（底部导航）
│   │   ├── chat/
│   │   │   └── chat_screen.dart           # 聊天页（SSE 流式+分页+搜索）
│   │   ├── agent/
│   │   │   └── agent_screen.dart          # Agent 管理页
│   │   ├── control/
│   │   │   └── control_screen.dart        # 控制面板（技能/工具/MCP）
│   │   ├── manage/
│   │   │   └── manage_screen.dart         # 管理页（文件/任务）
│   │   ├── stats/
│   │   │   └── stats_screen.dart          # 数据统计页
│   │   └── settings/
│   │       └── settings_screen.dart       # 设置页
│   ├── widgets/
│   │   ├── loading_indicator.dart         # 加载指示器
│   │   ├── shimmer_loading.dart           # 骨架屏组件
│   │   ├── state_widgets.dart             # 空状态/错误状态组件
│   │   └── message_bubble.dart            # 消息气泡组件
│   └── utils/
│       └── logger.dart                    # 日志工具
├── android/
│   ├── app/
│   │   └── src/
│   │       └── main/
│   │           ├── AndroidManifest.xml
│   │           └── kotlin/
│   │               └── MainActivity.kt
│   └── build.gradle.kts
└── pubspec.yaml                           # 依赖配置
```

## 使用说明

### 下载安装

从 [Releases 页面](https://github.com/R3lyW1nd/QwenPaw-Android-APP/releases) 下载最新 APK。

| 架构 | 适用设备 | 建议 |
|------|---------|------|
| arm64-v8a | 2020 年后 Android 手机 | 推荐 |
| armeabi-v7a | 较旧 Android 设备 | 可选 |
| x86_64 | 模拟器 / Chromebook | 模拟器专用 |

### 首次使用

1. 下载对应架构的 APK 并安装
2. 启动应用，进入设置页
3. 填写服务器地址（例如 http://192.168.1.100:80）
4. 输入用户名和密码
5. 点击连接，验证通过后自动跳转主界面

### 聊天

1. 在底部输入框输入消息，点击发送
2. AI 回复以 SSE 流式实时展示（打字机效果）
3. 支持工具调用结果自动展示（文件、图片等）
4. 向上滑动可加载历史消息（分页）

### Agent 切换

点击底部导航栏「智能体」标签，可切换不同的 AI 角色，每个 Agent 拥有独立的技能和工具配置。

### 主题切换

在设置页可切换：
- 主题模式：浅色 / 深色 / 跟随系统
- 强调色：6 种颜色（蓝 / 绿 / 橙 / 紫 / 红 / 青）

## API 对接说明

应用对接 QwenPaw RESTful API，完整文档请参考 [QwenPaw RESTful API 文档](https://qwenpaw.agentscope.io/docs/api-tutorial)。

### 主要接口

| 接口 | 方法 | 说明 |
|------|------|------|
| /api/auth/login | POST | 用户登录认证 |
| /api/console/chat | POST | SSE 流式聊天消息 |
| /api/agents | GET | 获取 Agent 列表 |
| /api/sessions | GET | 获取会话列表 |
| /api/skills | GET | 获取可用技能 |
| /api/tools | GET | 获取可用工具 |
| /api/mcp/list | GET | 获取 MCP 配置 |
| /api/cron/jobs | GET | 获取定时任务列表 |
| /api/token/stats | GET | Token 使用统计 |
| /api/workspace/files | GET | 工作空间文件列表 |

### 认证方式

请求头携带 JWT Token：

```
Authorization: Bearer <JWT_TOKEN>
```

首次登录通过 `POST /api/auth/login` 获取 JWT Token。

### SSE 流式响应

聊天接口采用 Server-Sent Events (SSE) 协议，实时返回 AI 回复片段：

```
data: {"type": "text", "content": "正在思考..."}

data: {"type": "text", "content": "这是完整的"}

data: {"type": "done"}
```


## 注意事项

1. 应用使用 HTTP 明文传输，请仅在可信网络环境中使用
2. 登录信息会本地持久化存储
3. SSE 连接超时设置为 5 分钟，适合 AI 回复场景
4. 离线缓存已启用，断网可查看历史消息
5. 如遇到连接问题，检查服务器地址和网络状态

## 许可证

MIT License © 2026 R3lyW1nd

---

<p align="center">
  Made with ❤️ by R3lyW1nd &amp; GeoS4C
</p>
