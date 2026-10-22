# Composer draft attachments — review-fix verification

Candidate source: f3c64bdf88a84059b09ff43db0c087ce9bf30838 (feature fix fe4cabad60; CI test fix f3c64bdf88), based on the user merged head 85ea625479. Verified files match the final 15-file SHA-256 manifest before/after browser runs; Git commit hooks left those bytes unchanged. macOS, Node 22, Chromium 149.

## Results

- 421/421 relevant Web Shell unit/DOM tests across ten files, including actual managed-admission callers and attachment deletion.
- 192/192 core extension tests; the durable-commit regression also passes with an actual state-file rename delayed 1250ms and without the delay.
- 9/9 complete Web Shell UI browser scenarios (simulated daemon): reload/session isolation and exact upload bytes; restore-time additions plus native same-name binary File contents; delayed acceptance protecting a new draft; one folded-text payload after an archive overlap; removal of visible overlapping image surviving release and reload; same-session main/split edits and reload; shared removal/clear; shared accepted submission; independent split sessions.
- 7/7 focused actual-hook DOM probes: managed-style fallback cleanup; held native-reader start through allocation; exact-text overlap with different-content control; overlapping-image removal; different new-chip removal retaining unread archive; genuinely loaded-chip removal; occurrence counts and unknown binary preservation.
- 9/9 additional actual-hook/native-browser fixed/control groups: old acceptance cannot abort a sibling reader; allocated pending/destination cleanup; removing submitted X while active/after leaving; adding Y or a reference tag while active/after leaving protects the whole draft; managed-style edit guard and image-only post-unmount archive cleanup.
- Root build, bundle, typecheck, final Web Shell rebuild/bundle, changed-file ESLint, Prettier and whitespace checks passed. Two final full-diff self-audit passes found no additional Critical.

## Evidence boundary

The four PR screenshots were visually inspected. They show actual Web Shell UI served by the worktree with a **simulated daemon**. File inputs, native IndexedDB transactions/structured cloning, reload, and exact serialized image/file upload bytes are real. They do not prove a real daemon/model request, backend session allocation or Git backend operation.

The separate race harness uses actual React/CodeMirror composer code and native browser IndexedDB/FileReader, but controls allocation/acceptance timing directly. Its managed-style guard case does not exercise a real Managed backend request. Mobile coverage is DOM textarea coverage, not a physical mobile-device run. The DOM IndexedDB stand-in deliberately does not model structured cloning, database versions or transaction-mode enforcement; native browser cases supply the corresponding persistence evidence.

## Explicit known gap and CI scope

R1-8 remains deferred and is excluded from the passing fix counts: submitting before workspace identity resolves, then resolving workspace before allocation and accepting after navigation, leaves the pending text/archive. The baseline already has the text-lifetime gap. This is documented in both design languages and the PR discussion under the repository repeated-review scope rule; the native-browser KNOWN_GAP witness remains preserved.

CI investigation and the complete pinned Node/Bun runtime run are reported separately in the PR. This browser report does not claim the full remote smoke suite is green. Attempt2 smoke traces show ERR_NETWORK_CHANGED while loading application modules. An additional local Excel-panel observation was retained separately from that boot failure; it was not represented as fixed by these composer changes.

## 中文说明

验证源码为 f3c64bdf88a84059b09ff43db0c087ce9bf30838，基于用户合并后的 85ea625479；功能修复为 fe4cabad60，CI 测试修复为 f3c64bdf88。浏览器测试首尾与 Git hook 执行后，15 个文件的冻结 SHA-256 一致。环境为 macOS、Node 22、Chromium 149。

通过结果：Web Shell 十个相关文件 421/421，包含托管接受调用方及附件删除；core 扩展模块 192/192，实际将状态文件 rename 延迟 1250ms 的对照也通过。9/9 条完整产品 UI 浏览器场景覆盖恢复、隔离、原生同名二进制文件内容、上传字节、新草稿保护、文字重叠去重、重叠删除后刷新、共享编辑/清空/发送及独立分屏。7/7 条专项 DOM probe 覆盖宿主清理、分配时待读取、重叠合并/删除、重复次数和未知二进制保留。另有 9/9 组实际 hook/原生浏览器修复及保护性对照，覆盖旧接受不取消新读取、迁移后的双 key 清理、删除已提交 X、新增 Y/标签、宿主编辑保护及卸载后的纯附件清理。全仓构建、bundle、类型检查、最终 Web Shell 重建/bundle、ESLint、格式和空白检查通过，两次最终完整 diff 自审未发现新增 Critical。

PR 选用的四张截图已目视检查，来自当前源码的实际 Web Shell UI，使用**模拟 daemon**。原生 File、IndexedDB 事务/结构化克隆、刷新及序列化上传字节为真实执行；不能证明真实 daemon/模型、后端会话分配或 Git 后端行为。独立竞态 harness 使用真实 React/CodeMirror hook 与浏览器存储/读取器，但直接控制分配和接受时序；其托管保护用例不是实际 Managed 后端请求。移动端仅为 textarea DOM 验证，未跑实体设备。DOM IndexedDB 替身不模拟结构化克隆、版本和事务模式限制，相关存储证据来自原生浏览器。

R1-8 仍是明确延后的已知缺口，不计入修复通过数：无工作区时提交，分配前确定工作区，再切走接受，会残留 pending 文字和归档。基线已经存在文字生命周期缺口；按仓库多轮 review 后收敛范围的规则，双语方案及 PR 讨论都已记录，保留原生浏览器 KNOWN_GAP 对照。CI 诊断及完整 Node/Bun 固定版本矩阵另在 PR 报告，此浏览器报告不宣称远端全量 smoke 全绿；attempt2 trace 的应用模块加载出现 ERR_NETWORK_CHANGED，另外一次本地 Excel 面板异常独立保留，未宣称被本次修复解决。
