# Actual /export command browser verification

Source: `b7ea5bf61f82e8c8c83d687fb1a70e9acee8a012`, before the subsequent merge of main. Captured on 2026-09-17 using Chromium 152.0.7977.83 and an isolated real daemon serving the production Web Shell.

A real user prompt (“请用一句话说明 Markdown 和 HTML 的区别。”) received a real assistant response. The browser then submitted `/export md` and `/export html`. Both commands wrote real workspace files, registered turn artifacts and opened their respective previews. Both screenshots were visually inspected and show the prompt/response, command, success result, artifact card and preview. Downloads matched the original bytes:

| Format | Bytes | SHA-256 of both original and download |
| --- | ---: | --- |
| md | 1073 | `1dde3b087d2d962f005b11baab3d4f63ff2db48e1e4446ea4ce603eb532fb737` |
| html | 9848 | `875fa33b9d129d70cf4d2a2200d0c51615a893de12ff9989c1784eb7b64b9a88` |

No command, daemon, file API, artifact event or model response was mocked. Only the exact HTML renderer/CSS CDN responses were substituted with actual local bundle bytes matching the original export SRI. Neither exported HTML nor production CSP was modified. This does not establish availability of the unpublished local renderer on the public CDN, Vite development compatibility, or behavior of the subsequent merge commit. No authentication values or user-session exports are included in this evidence.

# 中文

证据对应提交 `b7ea5bf61f82e8c8c83d687fb1a70e9acee8a012`，早于后续合并 main。2026-09-17 使用 Chromium 152.0.7977.83，隔离的真实 daemon 提供生产 Web Shell。

先发送真实 prompt“请用一句话说明 Markdown 和 HTML 的区别。”并收到真实助手回复，再通过浏览器执行 `/export md`、`/export html`。两个命令实际写入文件、注册回合产物并打开各自预览。两张截图均已目视检查，展示问答、命令、成功结果、卡片与预览。下载与原文件逐字节一致，字节数及两者相同的 SHA-256 见上表。

命令、daemon、文件 API、artifact 事件、模型回复均未模拟。仅精确的 HTML renderer/CSS CDN 响应替换为与导出原始 SRI 匹配的本地真实 bundle；未修改导出 HTML 或生产 CSP。不据此声明未发布资源在公共 CDN 可用、Vite 开发环境可用或后续合并提交已通过验证。证据不含认证值或用户原有会话导出。
