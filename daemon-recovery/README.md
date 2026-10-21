# Daemon recovery browser evidence

Implementation commit: `929927576408a5b2242cbaf438cc921c74399d2f`. Captured on macOS arm64 with Node.js22.14.0, current local build and headless Chromium on 2026-10-21.

Real test-owned loopback daemon; no simulated backend. One provider, no chat session/model prompt. Termination was detected in3.431s; after detection,54.049s contained zero business requests, and health start gaps were5.004/15.003/30.000s. Same-address/token restart recovered automatically in26.113s without reload or Retry. The unsent draft survived, remained editable, and reopening Reference file performed a real directory GET200. All16 checks passed with no page errors. Browser network errors from initial authentication, outage discovery and failed health probes are preserved in the JSON; they are not claimed absent. Test-owned daemon/browser/runtime were cleaned up.

- `offline-after-backoff.png`: persistent offline banner and retained draft.
- `recovered-draft.png`: automatic recovery with banner removed and original draft visible.
- `recovered-directory-and-editable-draft.png`: successful directory browse and draft editing after recovery.
- `network-evidence.json`: sanitized request timeline and assertions; times are relative milliseconds from test start, fixture workspace paths are replaced.

The screenshots show states of the same changed build. They are not a baseline comparison and do not establish real Git mutations, active model session/SSE restoration, multiple panels, audio/LAN, or host success-rate metric filtering.

## 中文证据说明

实现提交为上面的固定提交。2026-10-21在macOS arm64、Node.js22.14.0和无头Chromium中运行当前本地构建，使用独立的真实loopback daemon，没有模拟后端。单Provider、无会话，未发送模型prompt。停机3.431秒后显示离线横幅；此后54.049秒业务请求为0，健康探针实际间隔5.004/15.003/30.000秒。同地址与token重启后26.113秒自动恢复，没有刷新页面或点击重试。草稿保留且可继续编辑，重新打开引用文件菜单实际完成目录GET200。16项检查全部通过，无浏览器pageerror；认证、首次断连和探针失败产生的网络错误仍保留在JSON中，并未声称它们不存在。自建daemon、浏览器与临时目录均已清理。

三张图片依次展示持续离线横幅与保留草稿、自动恢复后横幅消失与原草稿、恢复后实际目录读取与草稿编辑。JSON中的时间相对测试开始以毫秒表示，临时workspace路径已替换。截图来自同一修改后构建的不同状态，不是修改前后版本对照，也不能证明真实Git写操作、活动模型会话/SSE恢复、多面板、音频/LAN或宿主成功率指标过滤。
