# 表格弹窗延迟验证证据

[English](README.md) | [简体中文](README.zh-CN.md)

## 来源与环境

实现提交：`d389055b6357f994987e2f3fe3725d97cceee661`。优化前截图在相同的当前宿主中使用经逐字节核对、来自`240eecf6178bb5be43061c0327e3cd62273a2695`的原始表格模块；优化后截图使用上述真实实现。图片文件名标识版本和弹窗。这些是本地真实 Web Shell UI 的浏览器 E2E 截图，使用模拟 daemon 与合成表格数据；它们不是已部署 DataWorks 改动的截图，也不证明真实 Git／后端操作。

本地平台：macOS arm64、Node.js22.14.0、无头 Chromium。截图场景：76行×3列、1280×900视口、英文、浅色主题。提交中的功能测试还覆盖80行／10列表格、普通及 Shadow DOM portal、行内及全屏模式。

## 观察结果

优化前，复制、密度、文本运算符和数值运算符菜单都会把 body 的 pointer-events 设为`none`并增加一个滚动锁。最终实现保留空的 pointer-events，不新增滚动锁。单元格详情／全屏对话框保留应有的锁。截图 JSON 记录准确的展开状态及源码／场景来源。

## 性能

独立对照在构建和功能测试空闲后进行：两个表格模块使用相同76行，全部保留挂载，以及相同的实际生产样式表（3445414字符）。每个菜单展开6次；预热后中位数排除首次展开。测量从原生 pointerdown 到插入菜单后的第二次 requestAnimationFrame，不能当作线上 Event Timing 或已部署延迟保证；样式耗时来自 CDP 指标。原始采样见`performance-samples.json`。

| 菜单 | 预热后展开耗时：优化前→后(ms) | 预热后样式重算：优化前→后(ms) |
| --- | --- | --- |
| 复制 |272.1→74.9|258.8→65.4|
| 密度 |269.1→75.4|255.5→64.1|
| 文本运算符 |191.3→15.5|171.2→2.6|
| 数值运算符 |185.6→15.3|168.5→2.3|

## 验证

- 根目录`npm run build`、`npm run typecheck`和`npm run bundle`：通过。
- 在`packages/web-shell`运行`npx vitest run client/components/messages/EnhancedMarkdownTable.test.tsx`：157项通过。
- 同包运行`PLAYWRIGHT_PORT=5197 npx playwright test --config playwright.config.ts client/e2e/web-shell.table-fullscreen.spec.ts --project=chromium --workers=1`：16项通过，1项仅用于基线截图而按设计跳过。
- 改动文件 ESLint／Prettier、差异检查和双语链接：通过。
- 独立弹窗锁审计，以及此前失败的连续复制重开／Escape 焦点回归：通过。
- 额外原生触屏测试：四类菜单共12轮快速选择后重开、12轮点击同按钮关闭均通过；24次外部交互回调都保留了包含自身触发按钮的原始事件路径。原始证据见`touch-observations.json`。
- 全部5个文件及相关焦点／状态／portal／剪贴板调用链审查：未发现需修改问题，实现 worktree 保持干净。

## 限制

未验证已部署 DataWorks、Windows／Linux 运行环境、Safari／Firefox、React18宿主运行时或最大500行×50列的性能压力场景。截图记录可见 UI 状态；body 锁断言、功能测试及实测采样提供行为／性能证据。素材位于独立证据分支，不进入实现分支。
