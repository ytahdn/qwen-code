# Review regression UI evidence / Review 修复 UI 证据

All screenshots were captured through Playwright against the implemented Web Shell merged with main 87dcc4a7, using simulated daemon HTTP/SSE responses, and visually inspected. They show the message menu, linked selection, retained middle group, corrected single-group mobile copy, unsupported-storage explanation, disabled confirmation during a peer turn, and cleared selection/dialog after peer deletion.

全部截图由 Playwright 在实现后的 Web Shell 合并 main 87dcc4a7 后捕获，使用模拟 daemon HTTP/SSE 响应，且已目视检查。依次展示消息菜单、联动选择、删除后保留中间组、单数文案正确的移动端选择、不支持存储的提示、他端轮次进行中禁用确认、他端删除后清空选择与对话框。

Browser evidence validates UI behavior only, not real JSONL deletion or model context. The final permanent deletion smoke suite passed 24/24; the independent review reproduction/verification passed 9/9 before and after correction. Filesystem mode preservation was verified separately by the actual replacement unit test.

浏览器证据仅验证 UI，不证明真实 JSONL 删除或模型上下文。最终正式删除 smoke 24/24 通过，独立 review 复现与修复验收均为 9/9。文件权限保留另由真实文件替换单测验证。

Images live only on this independent fork asset branch. / 图片仅存于 fork 的独立素材分支。
