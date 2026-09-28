# Navigation rail PR screenshots

Captured from source commit `8301fce8b4354fd154b67630037f4aa5842575c6` after merging current origin/main. All 17 final images were individually opened with view_image and visually inspected by the test engineer. Actual Web Shell UI with Playwright mock daemon; Chromium 1440×1000, English/light theme, reduced-motion preference. Images show UI composition and navigation only; they do not establish real channel connectivity, filesystem grants, Live audio capture, model calls, or Git backend behavior.

| File | English | 中文 |
| --- | --- | --- |
| 01-home-expanded.png | Home combines the primary rail with the workspace/session column. | 首页组合一级导航栏与工作区/会话栏。 |
| 02-rail-collapsed.png | Collapsing the secondary column leaves only the 56px primary rail. | 收起二级栏后仅保留56px一级导航栏。 |
| 03-more-menu.png | More groups auxiliary actions and version information. | 更多菜单集中辅助功能与版本信息。 |
| 04-local-files.png | Local files opens a nested panel inside More. This fixture has no filesystem bridge. | 本地文件从更多菜单打开嵌套弹层；此模拟环境未提供文件系统桥接。 |
| 05-plugins.png | Plugins opens its existing management page from the primary rail. | 插件一级入口打开既有管理页面。 |
| 06-channels-settings.png | Channel settings retain the channel workspace/session column. | 频道设置与左侧频道工作区/会话列表并列展示。 |
| 07-channel-conversation.png | Selecting a channel session displays its detail while retaining the Channels section. | 选择频道会话后显示详情，同时保留频道导航栏。 |
| 08-live-settings-history.png | Live settings share the screen with the flat Live history list and call entry. | Live设置与平铺历史会话列表、通话入口并列展示。 |
| 09-live-empty.png | An empty Live list uses the centered muted inbox illustration. | Live暂无会话时显示水平居中的浅灰收纳盒空态。 |
| 10-scheduled-tasks.png | Scheduled Tasks uses the aligned functional-page header. | 定时任务页面使用统一对齐的功能页标题栏。 |
| 11-goals.png | Goals uses the aligned functional-page header. | 目标页面使用统一对齐的功能页标题栏。 |
| 12-session-overview.png | Session Overview remains accessible through More. | 会话总览仍可从更多菜单访问。 |
| 13-settings-live-fallback.png | Without a primary Live entry, global Settings retains the Live card and unified Save action. | 没有独立Live入口时，全局设置保留Live卡片和统一保存按钮。 |
| 14-home-only-expanded.png | A Home-only embedded host uses the single workspace/session column. | 仅有首页的嵌入宿主使用单个工作区/会话栏。 |
| 15-home-only-collapsed.png | Home-only collapse retains the legacy 56px strip and Expand control. | 仅首页模式收起后保留原有56px窄条和展开按钮。 |
| 16-narrow-host-drawer.png | A narrow embedded host opens its branded navigation as a contained drawer. | 窄嵌入宿主以受容器约束的抽屉显示品牌与导航。 |
| 17-desktop-relay.png | More retains the existing Use this computer panel; localhost relay probing is mocked and no connection is started. | 更多菜单保留“使用这台电脑”弹层；本机Relay探测使用模拟响应，未启动真实连接。 |


## Actual verification

Screenshot capture completed with zero page errors, Live mutations, media capture calls or Live sockets. Desktop Relay localhost probing was intercepted with a fixture response; this fixture lacks the daemon reverse-tool capability, so its visible panel correctly says “Unavailable here.” Local files likewise shows its unavailable state. The channel settings fixture is read-only and the displayed “Connected” status is mock data, not a real external connection. Channel session detail has no transcript events and retains the generic mock session header. These screenshots establish layout and entry visibility, not actual Git, filesystem, audio, channel or relay operations.

Latest merged-source E2E: navigation-rail 3, live-navigation 2, channels 3, session-overview 12, URL-navigation 12 — 32 distinct cases with passing evidence. Initial combined run had 31 passed and 1 Overview title-hover detail timeout; that identical case passed an isolated trace-enabled retry without source or test edits. Do not describe the initial run as fully green. Logs: `/tmp/navigation-final-merged-e2e.log`, `/tmp/navigation-merged-overview-retry.log`. Screenshot capture log: `/tmp/navigation-pr-captures-final.log`.

All diagnostic scripts and captures live in ignored `.qwen`; no implementation or formal test files were edited by the test engineer. No GitHub/upload action was performed by this agent.
