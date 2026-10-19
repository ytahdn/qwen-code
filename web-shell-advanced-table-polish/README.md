# Final PR screenshots — main 81e83de6b6

Latest refresh: the toolbar trigger caption is **Copy / 复制**. All six after images and the four comparable baseline images were recaptured; the six browser screenshot cases passed in 34.6 s. Latest log: `/tmp/table-pr-final-copy-label-scoped.log`.

最新刷新：工具栏触发器文案为 **Copy / 复制**。六张 after 图与四张可比基线图均已重新捕获，六项浏览器截图场景全部通过（34.6 秒）；最新日志为 `/tmp/table-pr-final-copy-label-scoped.log`。

All ten images were captured with real Chromium browser E2E and visually checked. The daemon is simulated and provides a deterministic transcript only. Baseline uses the exact table component and CSS from main `81e83de6b6ec92684548314d1acd511fe301f1fa` inside the synchronized host. These images do not verify real Git/backend operations. Source/image hashes and dimensions are in `capture-metadata.json`.

全部十张截图均由真实 Chromium 浏览器 E2E 捕获并已目视检查，使用模拟 daemon 提供固定转录数据。基线为 main `81e83de6b6ec92684548314d1acd511fe301f1fa` 的原始表格组件与 CSS，在同步后的同一宿主内渲染；截图不代表真实 Git 或后端操作验证。源码、图片哈希及尺寸见 `capture-metadata.json`。

| Image | English evidence caption | 中文证据说明 |
| --- | --- | --- |
| main-desktop-toolbar.png | Main baseline: table toolbar with the previous density Select and direct copy action. | main 基线：旧密度 Select 与直接复制按钮。 |
| current-desktop-toolbar.png | Current toolbar: the Copy trigger, shared controls, and header actions next to labels. | 当前工具栏：“复制”触发器及统一控件，表头操作紧邻字段名称。 |
| main-desktop-density.png | Main baseline: selected-item-aligned density Select overlaps the trigger area. | main 基线：密度 Select 按选中项对齐，弹层覆盖触发器区域。 |
| current-desktop-density.png | Current: density dropdown opens below the trigger and retains a single checked option. | 当前：密度下拉菜单位于按钮下方，保留单选勾选标记。 |
| current-desktop-copy-menu.png | Current: Copy opens the menu with Copy text and Copy Markdown. | 当前：“复制”打开菜单，提供“复制文本”和“复制 Markdown”。 |
| main-390-inline.png | Main baseline at 390 px: the expand control still shows its text label. | main 基线，390px：展开控件仍显示文字。 |
| current-390-inline.png | Current at 390 px: copy and expand controls use icons while retaining accessible names. | 当前，390px：复制与展开控件仅显示图标并保留可访问名称。 |
| current-390-fullscreen.png | Current 390 px fullscreen table with the compact toolbar visible. | 当前 390px 全屏表格，紧凑工具栏保持可见。 |
| main-fullscreen-sort-drag.png | Main baseline: descending sort and held left-edge selection; sampled scrolling/range stays fixed. | main 基线：降序排序后按住拖选至左侧边缘，采样滚动位置与选区未继续推进。 |
| current-fullscreen-sort-drag.png | Current: descending sort and the same held-edge scenario; scrolling and selected rows advance. | 当前：降序排序下执行相同边缘拖选，滚动及选区持续推进。 |

Legacy clipboard was separately validated by forwarding the real native execCommand and reading the actual Chromium clipboard from an independent secure probe: ordinary inline / Shadow fullscreen × text / Markdown, 4 passed. The unavailable Clipboard API was emulated on loopback; a real non-loopback HTTP origin and native macOS paste were not tested.

另通过真实原生 execCommand 与独立安全页读取实际 Chromium 剪贴板验证 legacy 复制：普通内联 / Shadow 全屏 × 文本 / Markdown，共四项通过。测试在 loopback 页面模拟 Clipboard API 不可用，未宣称验证真实非 loopback HTTP 来源或原生 macOS 应用粘贴。

Implementation commit / 实现提交: [`3731df651c2d7acf36689ff2929d5bac92b26a4c`](https://github.com/ytahdn/qwen-code/commit/3731df651c2d7acf36689ff2929d5bac92b26a4c). Captured after-source hashes match this commit / 捕获时的 after 源码哈希与此提交一致。
