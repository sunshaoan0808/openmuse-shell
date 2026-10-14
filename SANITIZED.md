# 说明：本仓库是「已脱敏的可构建快照」

上游：[CopilotKit/openmuse](https://github.com/CopilotKit/openmuse)（MIT）。

## 为什么有这个仓库

上游 fork 的 GitHub Actions 被平台停用（fork 专有开关，API 改不动），APK 无法从 CI 出包。
这是一个**非 fork** 的公开副本，Actions 直接可用，用来构建 Android 客户端壳。

## 与私有开发仓的差异（均为有意为之）

| 项目 | 处理 |
| --- | --- |
| `.env` 及一切凭据（API key / 访问密钥 / 令牌） | **不入库**，由 `.gitignore` 拦住 |
| 第三方人设文案与立绘（CC BY-NC-ND 4.0） | **不入库**，仅存在于本地开发机 |
| 运行时数据目录（数据库目录）、本地日志、一次性探针脚本 | 已从工作树**与全部历史**中移除 |
| 记录内网拓扑的内部笔记（部署总览 / 可行性评估 / 反代说明） | 已剔除 |
| 内网示例地址 `10.7.0.x` | 换成文档专用保留段 `192.0.2.x` |
| `android-apk.yml` 的 `api_url` 默认值 | 换成 `https://your-api.example.com` 占位 |

## 构建 APK

Actions → **Build Android APK** → Run workflow，三个输入：

| 输入 | 说明 |
| --- | --- |
| `api_url` | 客户端要连的服务端地址 |
| `build_type` | `assembleRelease`（可安装）或 `assembleDebug` |
| `abis` | 例如 `arm64-v8a` |

## 自检过什么

- 全部历史对象按「真凭据值精确比对 + 常见凭据形态」双路扫过，零命中
- 公网克隆回来复扫（不信本地）：凭据 0、第三方资产 0、内部笔记 0
