# Sender tool-call panel verification

Implementation: `5aad27e6db`, following `6f68391f00` in QwenLM/qwen-code#12466.

## Verified

Chromium on macOS, real locally built `node dist/cli.js` daemon and bundled Web Shell, isolated temporary workspace/runtime, local scripted OpenAI-compatible model. Real shell and glob tools executed. No `page.route`, mock daemon, production model, or real Git mutation was used. The harness adapts the maintainer’s [round-two evidence](https://github.com/wenshao/qwen-code/tree/d7b8cc9c04fe2ef36f72e36c858d03cc3b45c43e/pr-12466-round2).

- Sent from the composer; while running, the sender's local message opened a persisted tab with `promptId`, selected prompt checkmark, one live row and zero tool-calls history requests.
- On settlement, exactly one history request returned 200 and two tool rows.
- Before reloading, closed the tab and reopened from the same sender message: adopted `recordId`, issued one additional history read and showed both rows.
- Reload restored the panel and both rows. Browser page errors: none. Both real-daemon runs passed.
- Screenshots were inspected visually: `sender-running-recovered.png` (light, selected running prompt) and `sender-restored.png` (dark, restored two completed calls).

## Observed limitation

A newly created empty session returned two turn-index 404s before prompt admission. The navigation store retained a temporary index-error notice while running (`sender-running.png` preserves this observation). It cleared after the successful post-completion index read. In the follow-up run, clicking Refresh while still running cleared it through an index-only read; tool-calls history requests remained zero. The light screenshot is after that manual index refresh. This pre-admission behavior is not claimed fixed by this patch.

## Checks

2,234 scoped unit tests passed: App 1,035; TurnCallsPanel 77; Session 1,052; tool-call emitter 70. New identity, missing-client loading, prepared/unprepared metadata, and page-size regressions failed before the fixes. Full build, typecheck and bundle passed, as did changed-file ESLint/Prettier and commit hooks. Two independent review/self-audit passes found no further defect in this follow-up.

## 中文说明

本轮在 macOS Chromium 中使用真实的本地 daemon 和打包 Web Shell，工具在隔离临时工作区真实执行；模型使用本地脚本化 OpenAI 兼容服务，没有模拟 daemon 或浏览器响应拦截，也没有验证生产模型或 Git 写入。

已确认：输入框发送后，运行中从原消息打开面板会保存 prompt ID、选中项有对勾且不读取历史；结算后恰好读取一次历史并显示两行；刷新前关闭页签再从原发送消息打开，会保存 record ID 并读取一次历史；刷新页面恢复面板和两行。两次真实 daemon 运行均通过，浏览器无 page error。浅色运行中与深色刷新后截图均已目视检查。

空会话首次加载在发送前出现索引 404，运行时一度保留错误提示；结算后自动恢复。补充测试运行中手动刷新只读取索引即可清除提示，历史请求仍为零。浅色主截图拍摄于该手动刷新之后，原始提示保留在 sender-running.png；这项初始化行为不列为本次已修复。

本轮 2,234 项相关单测通过，完整构建、类型检查、打包、格式和 lint 检查通过。截图仅说明上述实际观察到的行为。
