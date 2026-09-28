# PR #12943 review-fix screenshots / 评审修复截图

Only the following seven images are selected for PR upload. Other diagnostic captures in this directory are not selected. / 仅上传以下七张已目视检查的图片；同目录其他诊断截图不在清单内。

Captured from current source Vite5187 with mocked daemon responses, English UI and light theme. Source implementation commit: f74f4c18fef748673ba2158f9a70b24340dd46c8. / 使用当前源码 Vite5187 和模拟 daemon 截图，英文界面、浅色主题。对应实现提交：f74f4c18fef748673ba2158f9a70b24340dd46c8。

| Image | English evidence | 中文说明 |
| --- | --- | --- |
| `conversation-search-entry-light.png` | 1280px standalone transcript keeps a visible conversation-search entry. | 1280px 独立页面中，会话搜索入口可见。 |
| `conversation-search-dialog-light.png` | The search entry opens a dialog and finds the loaded fixture answer. | 点击搜索入口可打开弹窗，并找到已加载的模拟答案。 |
| `mcp-home-fixed.png` | The /mcp local panel preserves Home navigation and its session column. | /mcp 本地面板保留首页导航选中态及会话栏。 |
| `url-host-omitted-fixed.png` | An embedded host without sidebar configuration retains its Settings URL and panel. | 未传侧栏配置的嵌入宿主保留 Settings URL 及设置面板。 |
| `live-conflict-warning.png` | A refreshed conflicting saved value preserves the draft, shows a warning and disables Save. | 刷新发现已保存值发生冲突时保留草稿、显示提示并禁用保存。 |
| `live-key-clear-visible-fixed.png` | Pending API-key removal remains visible after enabling Live and can be undone. | 重新开启 Live 后，待移除密钥的提示仍可见并可撤销。 |
| `live-disabled-empty-fixed.png` | Disabled Live with no Live workspace renders the empty-session state. | Live 禁用且没有 Live 工作区时显示无会话空态。 |

## Boundaries / 验证边界

All seven selected images are visually inspected. Browser assertions separately verified the behavior, including the12 default-host deep-link/local-command combinations and key-removal undo. Screenshots do not prove real concurrent persistence, Git backends, external channel operations, provider calls or audio behavior. No real key is present. The search fixture intentionally covers loaded messages only, so its fallback notice is expected. MCP status and runtime readiness are synthetic, and its initialization request is mocked; MCP administration was not exercised.

七张入选图均逐张目视检查，并另有浏览器断言验证行为，包括12种默认宿主深链/命令路径与密钥移除撤销。截图不作为真实并发持久化、Git 后端、外部频道、模型调用或音频行为的证明，没有真实密钥。搜索 fixture 仅覆盖已加载消息，因此保留对应提示。MCP 状态和运行时就绪为模拟数据，初始化请求由 mock 响应，未操作真实 MCP 管理。
