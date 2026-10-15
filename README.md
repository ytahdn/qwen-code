# Web Shell grouped deletion evidence / Web Shell 整组删除验证

These screenshots were captured by Playwright against the implemented Web Shell with simulated daemon HTTP/SSE responses, and visually inspected. They demonstrate UI behavior only; they do not prove actual backend persistence.

这些截图由 Playwright 在实现后的 Web Shell 中通过模拟 daemon HTTP/SSE 响应捕获，并经过目视检查。截图仅证明界面行为，不作为真实后端持久化的证明。

- menu.png: copy plus hover/click/keyboard action menu. / 复制及支持悬停、点击、键盘的操作菜单。
- selection.png: linked prompt/reply checkboxes, non-contiguous selection, content-width toolbar. / 用户消息与回复联动选择、非连续选择、与内容等宽的工具栏。
- after-deletion.png: selected groups disappear and the unselected middle group remains. / 所选组消失，未选中的中间组保留。
- mobile-selection.png: single-group selection at narrow viewport width. / 窄视口下选择唯一消息组。

Validation: root build/bundle/typecheck; focused core769, SDK529, CLI routes/errors253, Session28 and Web Shell472 unit cases;17/17 browser deletion/edit cases. Independent real daemon/ACP/JSONL verification used a deterministic local model, covering tool-group physical removal, later model requests, resume, delete-all, unchanged compression summaries, and active-prompt409. Separate actual filesystem tests cover legacy GET/DELETE malformed-lock/I/O/live-conflict cases; browser failure recovery uses simulated daemon responses.

验证包括根目录 build/bundle/typecheck，定向单测（core769、SDK529、CLI路由与错误253、Session28、Web Shell472），以及17/17条浏览器删除与编辑用例。独立的真实 daemon/ACP/JSONL 验证使用确定性的本地模型，覆盖工具整组物理删除、后续模型请求、恢复、全部删除、摘要不变以及活跃轮次409。真实文件系统测试另外覆盖 legacy GET/DELETE 的畸形锁、I/O与活跃锁冲突；浏览器失败恢复使用模拟 daemon 响应。

macOS/Node22 tested; Windows and Linux not tested locally. / 已验证 macOS/Node22；本地未验证 Windows 与 Linux。
