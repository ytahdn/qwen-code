# Issue 15996 browser evidence

Implementation revision: `04d27f916680bf3c8a0278d1103d6b8d0b3d30d6`.

Captured on macOS with Node.js 22.14.0 and Playwright Chromium 149.0.7827.55. The built frontend was served by `node dist/cli.js serve`; deterministic daemon API responses came from the repository's browser test fixture.

- `touch-session-switch.png`: returned chat after selecting an existing session, 390 × 844 touch emulation.
- `touch-settings-return.png`: returned chat after closing Settings, 390 × 844 touch emulation.
- `desktop-settings-return.png`: returned chat after closing Settings, 1280 × 900 desktop profile.
- `touch-settings-during-load.png`: Settings remains focused when an earlier session load completes, 390 × 844 touch emulation.

The screenshots were visually inspected. Browser assertions recorded the non-editable chat pane as the active element and zero composer focus events after touch session switching, Plugins browser Back, and Settings Back. Settings kept focus on its Back button when an earlier session load finished. Desktop navigation still focused the editable composer. New-session focus and direct typing passed in both profiles.

Screenshots show the returned UI. They do not establish physical Android/iOS keyboard behavior, screen-reader behavior, real session persistence, or Git backend operations. Split folding, cockpit return, and approval resolution have unit regression coverage rather than browser coverage in this run.

## 中文说明

实现版本：`04d27f916680bf3c8a0278d1103d6b8d0b3d30d6`。

截图在 macOS、Node.js 22.14.0 和 Playwright Chromium 149.0.7827.55 下采集。构建后的前端通过 `node dist/cli.js serve` 提供，确定性的 daemon API 响应由仓库的浏览器测试夹具模拟。

- `touch-session-switch.png`：选择已有会话后返回聊天，390 × 844 触屏模拟。
- `touch-settings-return.png`：关闭 Settings 后返回聊天，390 × 844 触屏模拟。
- `desktop-settings-return.png`：关闭 Settings 后返回聊天，1280 × 900 桌面配置。
- `touch-settings-during-load.png`：先前的会话加载完成后，Settings 仍保留焦点，390 × 844 触屏模拟。

截图均已目视检查。浏览器断言确认：触屏上切换会话、从 Plugins 通过浏览器后退返回、从 Settings 返回后，活动元素均为不可编辑的聊天区域，输入框焦点事件数为零。先前会话加载结束时，Settings 的返回按钮保留焦点。桌面导航仍会聚焦可编辑输入框。两种配置下的新建会话聚焦和直接输入均通过。

截图展示返回后的 UI，不能证明 Android/iOS 真机键盘、读屏软件、真实会话持久化或 Git 后端行为。本次分栏折叠、cockpit 返回和审批结束路径由单元回归测试覆盖，未做浏览器验证。
