# Post-merge Web Shell browser verification

Commit: `d10c76801c30a743674ac5b53e2833e16b1a9648` (feature merged with origin/main). Date: 2026-09-22.

**Scope: mock-daemon frontend E2E.** Chromium loads the actual merged Web Shell through its Vite development server on 127.0.0.1:5197. The repository mock-daemon/SSE harness provides synthetic session events; test handlers provide the workspace-scoped tool-calls and turn-index responses. This does not execute real tools, authenticate MCP, validate real daemon replay, or exercise Git mutations. Global CLI baseline command returned 0.22.0. Root agent owns install/build/bundle; this agent did not run them.

## Result

**2/2 browser tests passed (light and dark, 13.0 seconds).** No page errors in either test.

Verified in each theme:

- Standalone entry exposes the localized “查看工具调用” action; opening it displays four invocation rows.
- Built-in tool labels are localized, and invocation descriptions appear in rows rather than raw shell tool identifiers.
- Completed and cancelled states render, including 0ms for a recorded zero-duration cancellation, 249ms and 932ms subsecond calls, and rounded 4s for a 4200ms call.
- Hovering recorded elapsed time opens a tooltip with start/end values. The probe checks distinct millisecond timestamps ending 10.000 and 14.200, corresponding to the recorded 4200ms interval.
- Prompt selector uses the one known record and has no All-prompts option.
- Refresh adds exactly one tool-calls request and retains the four rows.
- MCP type filtering leaves one row; its badge has font-normal class and computed 11px size.
- Expanding MCP details shows separate JSON code blocks for arguments and results, including include_spaces and demo-user.
- All-tools selection restores four rows.
- A real browser page reload restores the open panel and selected durable record ID; all four calls remain displayed. Locale query parameters are ephemeral in the standalone route, so the post-reload assertion uses structural panel identity instead of assuming Chinese locale persists.

Recorded total requests over each full open/filter/refresh/reload scenario: 5 tool-calls and 2 turn-index reads. The tests separately assert that the explicit Refresh action adds exactly one read; total counts include lifecycle restoration. No live-running clock scenario is claimed in this particular capture pass.

## Screenshots and visual review

All images show synthetic mocked records in the actual rendered UI. Two compact PR images are recommended:

- `light-overview-panel.png`: 500×450, complete list, descriptions, localized labels, durations, cancelled status, prompt and type selectors.
- `dark-mcp-json-panel.png`: 500×673, MCP filter and expanded argument/result JSON blocks.

These exact final images were opened and visually inspected: labels, spacing and borders are readable; the two-line call layout is distinct; the warning-colored cancellation is visible; JSON syntax highlighting and both code blocks fit without clipping or overlap. Related full-page context is available in `light-overview.png` and `dark-mcp-json.png`. Additional light/dark variants are retained alongside them.

Initial harness retries addressed ESM config directory resolution and post-reload locale-neutral lookup; the final application assertions were not loosened. No application code or existing test file was modified.

## Re-run

From packages/web-shell:

```sh
npx playwright test --config ../../.qwen/scripts/turn-calls-redesign/merge-playwright.config.ts
```

Harness: `.qwen/scripts/turn-calls-redesign/merge-turn-calls.spec.ts`. Final log: `playwright.log`.

## PR evidence text

English: Browser E2E on the merged implementation passed in light and dark themes using a mock daemon. These screenshots show the actual Web Shell rendering synthetic invocation data, including localized labels, descriptions, recorded duration/status, MCP filtering, and JSON argument/result details. Reload restored the selected prompt and open panel. This frontend check does not represent real tool execution or real Git backend operations.

中文：合并后的实现已通过浅色和深色浏览器 E2E，使用模拟 daemon。截图来自真实 Web Shell 渲染的测试调用数据，展示国际化名称、描述、记录耗时与状态、MCP 筛选，以及 JSON 参数和结果。刷新页面后所选提示词和已打开的面板正常恢复。本前端验证不代表真实工具执行或真实 Git 后端操作。
