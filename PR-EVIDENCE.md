# Merge verification / 合并验证

Verified the merge of origin/main b9840886b8 into feat/web-shell-turn-calls-panel on macOS with Chromium, the built real daemon and bundled Web Shell. The model was a local scripted OpenAI-compatible service; shell/glob tools executed for real. No mock daemon or browser response interception. Screenshots were inspected visually.

- The sender prompt is selected and persisted while running; no tool-history polling occurs.
- Settlement reads history once and shows both calls. Replay returns recorded start timestamps and durations (shell 8239ms, glob 7ms) through the upstream started_at_ms recording path.
- Reopening from the original sender message adopts the durable record ID. Reload restores the panel and both completed rows; no browser page errors.
- The empty new-session index initially returned 404. Manual index refresh clears that notice without reading tool history. The running screenshot is taken after this refresh; sender-running.png retains the initial notice. This pre-existing behavior is documented, not claimed fixed.
- 3,395 scoped tests passed: Core/telemetry 538, ACP replay 144, SDK 414, CLI Session/emitter/route 1,135, Web Shell App/panel/trajectory 1,164. Two stale timing assertions from automatic merging were corrected and their 51-test trajectory suite rerun successfully. Full build, typecheck and bundle passed, as did formatting/lint for integration changes.

This does not verify production models, actual Git operations, Windows/Linux, or repeat the maintainer's large-session survey.

## 中文

在 macOS 上将 origin/main b9840886b8 合入功能分支后，使用 Chromium、构建后的真实 daemon 和打包 Web Shell 验证。本地脚本模型提供 OpenAI 兼容响应，shell/glob 工具真实执行；没有模拟 daemon 或浏览器响应拦截，截图已目视检查。

- 运行中默认选中发送端提示词并保存持久身份，不轮询工具历史。
- 结算后读取一次历史并显示两条调用。主分支 started_at_ms 记录链路正确回放开始时间及耗时（shell 8239ms、glob 7ms）。
- 从原发送消息重新打开会采用持久 record ID；刷新页面恢复面板与两条已完成调用，无浏览器页面错误。
- 空会话初始索引返回 404；手动刷新索引后提示消失，且不读取工具历史。运行中主截图拍摄于刷新后，sender-running.png 保留初始提示。本次未声称修复该既有行为。
- 3,395 项相关单测通过：Core/遥测 538、ACP 回放 144、SDK 414、CLI Session/发送器/接口 1,135、Web Shell App/面板/trajectory 1,164。自动合并遗留的两处计时断言已修正，对应 51 项 trajectory 测试复跑通过。完整构建、类型检查、打包及集成修改的格式/静态检查通过。

不代表生产模型、真实 Git 操作或 Windows/Linux 验证，也未重复维护者的大会话调查。
