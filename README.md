# Message deletion UI evidence / 消息删除 UI 证据

Recaptured on 2026-10-20 after merging origin/main d21060e8 and fixing review findings. Playwright Chromium used a simulated daemon (HTTP/SSE fixtures); the complete deletion suite passed 26/26 without retries. All four images were visually inspected. They show a hover menu with the hovered Edit item actually focused/highlighted, middle-entry selection extended to later groups with Delete visible but disabled, a surviving turn after non-contiguous deletion, and surviving saved/local messages with an accurate explanation after committed deletion followed by reload failure.

2026-10-20 合并 origin/main d21060e8 并修复 review 问题后重新截图。Playwright Chromium 使用模拟 daemon HTTP/SSE；完整删除用例 26/26 通过且无重试。四张截图均已目视检查，展示 hover 菜单中的编辑项实际取得焦点和高亮、从中间入口选择后续组且删除入口可见但禁用、非连续删除后保留轮次，以及已删除但重载失败时保留未删消息和本地命令并准确说明结果。

These screenshots establish UI behavior against simulated APIs only; they do not prove real JSONL mutation or model input. Previous real-daemon/ACP/JSONL/model evidence remains in the PR discussion. This run used isolated port 42349, cleaned up afterward, and did not mutate user sessions or services. Images are only on this independent fork asset branch.

截图仅证明模拟 API 下的 UI 行为，不证明真实 JSONL 修改或模型输入；此前真实 daemon/ACP/JSONL/模型验证保留在 PR 讨论中。本轮使用隔离端口 42349 并已清理，未修改用户会话或服务。图片仅在 fork 的独立素材分支。
