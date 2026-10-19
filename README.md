# Message deletion regression evidence / 消息删除回归证据

Captured on 2026-10-19 from the implementation worktree based on08fec5f93b with the CI/review fixes applied. Playwright Chromium ran against simulated daemon HTTP/SSE responses. All four images were visually inspected: hover menu with composer focus retained, linked non-contiguous selection, surviving middle turn, and deleted first turn absent while unselected saved/local rows survive a failed reload with an accurate explanation.

2026-10-19，在基于08fec5f93b并应用CI/review修复的实现worktree中捕获。Playwright Chromium使用模拟daemon HTTP/SSE响应。四张图片均已目视检查：悬停菜单且输入框保留焦点、联动的非连续选择、删除后保留中间轮次，以及重载失败时已删首轮不存在、未选已保存消息与本地命令仍可见，并明确提示删除已完成但重载失败。

The formal browser suite passed25/25. Independent failure-injection probes separately reproduced and verified lifecycle/context recovery, failed reload retention, mixed replay/live local ordering, and refusal of ambiguous abandoned-branch compression ownership. These images prove UI states only; they do not prove a real backend JSONL mutation or model request. Earlier real-daemon/ACP/model evidence remains in the PR discussion.

正式浏览器用例25/25通过。独立故障注入探针另行复现并验证生命周期/上下文恢复、重载失败保留、混合replay/live本地命令顺序，以及废弃分支压缩归属不明确时拒绝删除。这些图片仅证明UI状态，不证明真实后端JSONL修改或模型请求；先前真实daemon/ACP/模型证据保留在PR讨论中。

Images are stored only on this independent fork asset branch. / 图片仅存于fork独立素材分支。
