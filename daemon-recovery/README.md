# Service recovery browser evidence

Implementation commit: `df78833baca69679b198c1a0412ebc52be048a5f`. Captured on macOS arm64 with Node.js22.14.0, the current local0.25.3 build and headless Chromium on2026-10-21.

Real test-owned loopback service; no simulated backend. One provider, no chat session or submitted model prompt. Shutdown was detected in3.473s; the complete54.056s after banner detection contained zero business requests, and health start gaps were5.004/15.002/30.002s. Same-address/token restart recovered automatically in25.944s without reload or Retry. The unsent draft survived, remained editable, and reopening Reference file performed a real directory GET200. All16 checks passed with no page errors. Browser network errors from initial authentication, outage discovery and failed health probes remain recorded; they are not claimed absent. Test-owned service/browser/runtime were cleaned up.

- `offline-after-backoff.png`: persistent “无法连接服务” banner and retained draft.
- `recovered-draft.png`: automatic recovery with banner removed and original draft visible.
- `recovered-directory-and-editable-draft.png`: successful directory browse and draft editing after recovery.
- `network-evidence.json`: sanitized request timeline and assertions; elapsedMs is relative to test start, fixture workspace paths are replaced.

The screenshots show different states of the same changed build. They are not a baseline comparison and do not establish real Git mutations, active model session/SSE restoration, multiple panels, audio/LAN, or host success-rate metric filtering.

## 中文证据说明

实现提交为上面的固定提交。2026-10-21在macOS arm64、Node.js22.14.0、当前本地0.25.3构建和无头Chromium中验证，使用独立真实loopback服务，没有模拟后端。单Provider、无会话，未发送模型prompt。停机3.473秒后显示“无法连接服务”的横幅；横幅出现后的完整54.056秒内业务请求为0，探针实际间隔5.004/15.002/30.002秒。同地址与token重启后25.944秒自动恢复，没有刷新页面或点击重试。草稿保留且可继续编辑，重新打开引用文件菜单实际完成目录GET200。16项检查全部通过，无浏览器pageerror；初始认证、首次断连和探针失败产生的网络错误仍保留在JSON中，并未声称它们不存在。自建服务、浏览器与临时目录均已清理。

三张图片依次展示持续离线横幅与保留草稿、自动恢复后横幅消失与原草稿、恢复后实际目录读取与草稿编辑。JSON中的elapsedMs相对测试开始以毫秒表示，临时workspace路径已替换。截图来自同一修改后构建的不同状态，不是修改前后版本对照，也不能证明真实Git写操作、活动模型会话/SSE恢复、多面板、音频/LAN或宿主成功率指标过滤。

## Initial-load explicit Retry

The workspace and standalone initial error pages were also checked in the actual built UI against the real test-owned service, with Playwright injecting only the initial capabilities HTTP502 and health HTTP503. Removing these injected failures and clicking Retry sent health then capabilities after31ms /17ms, before the pending5s backoff. Both error pages cleared and the editor remained editable. All16 checks passed with zero writes/model prompts and no page errors. Mounting the recovered App also performed normal capabilities reads (2 total for workspace,3 for standalone); this is not claimed to be a single total request. The4 initial-error/recovered PNGs document these two fault-injected paths; they do not establish backend fault handling without injection.

## 首次加载失败后的手动重试

另外在实际构建UI与独立真实服务上验证了工作区和独立会话两种首次加载错误页；仅使用Playwright注入首次capabilities HTTP502和health HTTP503。解除注入后点击重试，31ms /17ms内先发health再发capabilities，未等待原定5s退避。两种错误页均消失，编辑器可输入；16项检查通过，写请求/模型prompt为0且无pageerror。恢复后挂载App还会正常读取capabilities（工作区合计2次，独立会话3次），不能宣称整个恢复过程只有1个请求。4张首次错误/恢复PNG记录这两条故障注入路径，不能据此声称未注入的真实后端发生过同类故障。
