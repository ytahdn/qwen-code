# PR 11636 final Web Shell browser evidence / 最终浏览器证据

Date / 日期: 2026-09-14

Chromium; real Vite UI with mocked daemon routes/SSE; dedicated port 5196. No real daemon, model, shell task, or Git backend operations were exercised. The existing user daemon on 5174 was not touched.

Chromium 实际 Vite 页面，daemon 路由和 SSE 为模拟。独立使用 5196 端口，不涉及真实 daemon、模型、Shell 任务或 Git 后端操作，未触碰用户 5174 服务。

## Verification / 验证

From packages/web-shell:

```sh
PLAYWRIGHT_PORT=5196 npx playwright test --config playwright.config.ts client/e2e/web-shell.background-turn.spec.ts --project=chromium --workers=1
```

Existing cases: 2 passed (10.7s). Temporary evidence harness: same 2 cases passed (11.0s), viewport 1600×1000; screenshots disable animations, detail capture additionally waits until expanded tool row no longer overlaps final answer. Harness retained here; copy it beside original spec to rerun (relative mockDaemon import), remove after running.

既有用例 2/2 通过（10.7s）；临时证据 harness 同样 2/2 通过（11.0s），使用 1600×1000 视口，截图禁用动画，详情截图额外等待工具行与答案不重叠。复现时将本目录 harness 复制到原 spec 旁边以保持 mockDaemon 相对引用，执行后删除。

- two-agents-collapsed.png: one user row, returned results ordered Rendering then Ownership, separate full-width completion cards with Source/View details, final main-agent answer remains visible, intermediate response folded away.
- two-agents-details.png: View details opens the right panel, child final text and expanded file tool visible; main final answer retained. Source interaction subsequently expands original user steps (asserted, not shown here).
- background-sidebar-hover.png: background-only activity shows amber breathing dot before title; title hover keeps previous actions. Dot-hover also verified to hide other actions. Screenshot is a still frame, animation presence/opacity asserted separately.
- prompt-spinner-priority.png: active prompt hides the background-only indicator and shows ordinary running spinner; after all activity ends both indicators are absent (asserted).

- 收起图：仅一条用户轮次，后台通知按 Rendering / Ownership 返回顺序呈现，通栏卡片分开，来源/详情在右侧，最终主 agent 正文保留，中间正文收起。
- 详情图：查看详情打开右侧面板，子 agent 最终正文和展开的文件工具可见，主正文仍保留；来源可展开原轮次步骤（断言验证，截图未展示）。
- 侧栏图：仅后台活动时显示标题前琥珀呼吸点；悬停标题仍显示既有操作；悬停点隐藏其他操作也已断言。静态图片不能展示呼吸动画，另有动画/透明度断言。
- 优先级图：主 prompt 活跃时隐藏后台点、显示普通运行 spinner；全部结束后两者均消失（断言验证）。

All four final screenshots visually inspected: card gaps, full width, action alignment, right-panel content, indicator placement are clear; no steady-state overlap or clipped relevant content observed. An initial screenshot caught expansion animation and was replaced only after waiting for settled layout, without changing production code.

四张最终截图均已目视检查：卡片间距、通栏、入口对齐、详情内容和侧栏位置正确；未见稳定态重叠或相关内容截断。首次截图抓到了展开动画中间态，等待布局稳定后重拍，未修改生产代码。
