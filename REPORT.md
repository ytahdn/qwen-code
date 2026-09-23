# PR #12466 review-fix browser evidence

Chromium E2E: 2/2 passed on 2026-09-23, light and dark themes. Actual Web Shell rendered with a **mock daemon/SSE and deterministic history**; no real tool execution, daemon persistence or Git backend operations are claimed.

Verified localized labels/descriptions, completed/cancelled icons, recorded timestamps, MCP 11px regular badge, tool filtering, JSON arguments/results, prompt popup, one explicit calls refresh, and reload restoring the open dock and durable selection. Each full scenario issued 5 tool-calls and 5 index requests across initial connection, settlement, refresh and reload; there is no per-open full-index walk. The mock advertises the real session_turn_navigation capability so the shared navigation store is exercised. Browser page errors: none.

Images were opened and visually checked after dismissing the timing tooltip with Escape and disabling capture-time animations:
- light-overview-panel.png: localized call list and selectors.
- dark-mcp-json-panel.png: MCP filtering and JSON detail blocks.
- light-prompt-picker.png: actual prompt picker open with its selected option.

The separate 5000-prompt regression uses the real navigation store under jsdom: only 10 options on initial open, bounded visible-page loading, keyboard Home/End/Enter, cache reuse across prompt changes, and one head refresh. This is not a browser performance benchmark.

Known harness-only limitations: ancillary model/stat requests can hit the unavailable mock backend; file-preview availability is not asserted here. Fresh real-daemon execution after restart remains unverified.

中文：浅色和深色 Chromium E2E 均通过，截图为真实 Web Shell 渲染的模拟 daemon 数据。验证了工具展示、MCP 与 JSON、prompt 选择及刷新恢复；不代表真实工具执行、daemon 持久化或 Git 后端操作。已目视检查最终截图。5000 条 prompt 的窗口化与键盘选择另由真实导航 store 的 jsdom 测试验证，不作为浏览器性能基准。
