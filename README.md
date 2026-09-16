# Web Shell tool file preview evidence

Real Chrome and daemon screenshots, visually inspected. No mock daemon was used.

- Before: globally installed qwen 0.22.0, expanded text-read/edit and PNG-read details without preview actions.
- After file/edit/image: final local qwen 0.23.4 build for implementation commit 3efc4b995c2f41c8123fc4e716ca3df40e946b3e, restored real tool transcript. Opens current file/image; historical text/diff remains inline. No new model calls were needed for final capture.
- Additional unavailable/refresh screenshots: earlier feature build from the same worktree before the subsequent subagent callback-stability fix. These cover missing-target hiding and active-tab text/image refresh. The callback fix is covered by deterministic component tests with mocked SDK responses, not a real streaming-subagent browser race.
- Browser coverage is text read, edit, PNG read, tab reuse, active-tab refresh, and a missing target simulated by reversibly moving a disposable fixture. It does not validate real multi-workspace/split/subagent backend ownership, Git operations, or every tool alias.

These images live on an independent asset branch and are not part of the implementation branch.

## 中文说明

真实 Chrome 与 daemon 截图，均已目视检查，未使用模拟 daemon。

- Before：全局安装的 qwen 0.22.0，展开文本读取、编辑与 PNG 读取详情，尚无查看入口。
- After 文件/编辑/图片：实现提交 3efc4b995c2f41c8123fc4e716ca3df40e946b3e 对应的本地 qwen 0.23.4 最终构建，恢复真实工具会话。打开当前文件或图片，历史文本和 diff 仍保留。最终截图无需新增模型调用。
- 额外的不可用/刷新截图：来自同一 worktree 的较早功能构建，早于后续子任务回调稳定性修复，验证缺失目标隐藏和活动标签的文本/图片刷新。回调修复通过模拟 SDK 响应的确定性组件测试验证，并非真实流式子任务浏览器竞态测试。
- 浏览器覆盖文本读取、编辑、PNG 读取、标签复用、活动标签刷新，以及通过可逆移动临时文件模拟目标缺失。不代表真实多工作区/分屏/子任务后端归属、Git 操作或所有工具别名均经过验证。

图片保存在独立素材分支，不进入实现分支。
