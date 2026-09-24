# Merge verification / 合并验证

Merge commit: 2e424efa8e. Base: origin/main 906418aa9b. Resolved three conflicts in the embedding documentation, transcript viewport and its tests. Retained the upstream conversation-search action alongside the existing durable-record Tool calls provider, and retained both sides' regression tests and host-option documentation.

1,379 scoped Web Shell tests passed across 10 files, including App, standalone entry, transcript viewport, conversation search, Tool calls and artifact/trajectory panels. Full repository build, typecheck, bundle and commit hooks passed.

Chromium uses the built real daemon and bundled Web Shell, with a local scripted OpenAI-compatible model and real shell/glob execution. No mock daemon or browser response interception. The sender selection persists while running with no tool-history polling; settlement reads history once; reopening the sender adopts the durable record ID; reload restores both completed calls. The trajectory overview renders both tool spans and clicking a span selects it. Screenshots are visually inspected. Conversation search is covered by unit tests, not claimed as part of this browser scenario.

The pre-existing initial empty-session index notice is cleared with a manual index refresh; it is not claimed fixed. No production-model, real Git-operation, large-session survey or Windows/Linux coverage is claimed. Earlier cross-package verification remains in previous PR comments.

## 中文

合并提交 2e424efa8e，主分支 906418aa9b。解决宿主文档、历史消息视口及其测试三个文件的冲突，同时保留主分支会话搜索入口、工具调用持久记录映射，以及两边回归测试和宿主选项说明。

10 个文件共 1,379 项 Web Shell 相关测试通过，覆盖 App、独立入口、历史视口、会话搜索、工具调用及扩展区/轨迹面板。完整仓库构建、类型检查、打包与提交钩子通过。

Chromium 使用构建后的真实 daemon 与打包 Web Shell，本地脚本模型提供 OpenAI 兼容响应，shell/glob 真实执行，无模拟 daemon 或响应拦截。运行中保存发送端选择且不轮询工具历史；结算后读取一次历史；从原消息重新打开采用持久 record ID；刷新恢复两条已完成调用。轨迹时间轴绘制两条工具区间，点击可选中。截图已目视检查。会话搜索由单测覆盖，不声称本浏览器场景验证了搜索。

既有空会话初始索引提示通过手动刷新索引消除，不声称已修复。不代表生产模型、真实 Git 操作、大会话调查或 Windows/Linux 验证；此前跨包验证保留在原 PR 评论中。
