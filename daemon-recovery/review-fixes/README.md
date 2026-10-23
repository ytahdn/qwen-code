# Recovery UI evidence / 恢复界面证据

Fixed implementation commit / 固定实现提交: `ac9491fea4ff5d2799ea86c57c8ccbec775d4019`.

Actual Chromium screenshots of the source Web Shell App/main and actual JavaManagedAgentProvider, served by an isolated Vite instance. Daemon and Managed HTTP/SSE responses are deterministic browser mocks. No real daemon, model, Java service or Git operation is verified. Ten selected browser checks passed; screenshots were visually inspected. Browser and test-owned Vite exited, and its port was released.

真实 Chromium 截图，渲染源码中的 Web Shell App/main 和实际 JavaManagedAgentProvider，使用独立 Vite 实例。Daemon 与 Managed HTTP/SSE 均为确定性浏览器模拟响应，不代表验证真实 daemon、模型、Java 服务或 Git 操作。10 项选定浏览器检查通过，截图已目视检查。浏览器与测试自建 Vite 已退出，端口已释放。

- `diagnostic-cold-offline-mock.png`: First Status-page mount occurs after actual shared controller check(true) encounters mocked health failure. It shows a localized service error and connection form, rather than indefinite Loading. / 实际共享 controller 的 check(true) 遇到模拟健康检查失败后，首次打开状态页；显示服务错误及连接表单，不再持续 Loading。
- `diagnostic-recovered-mock.png`: Clicking the actual Retry connection button completes health/capabilities and default-summary/full reads. The banner disappears and mock connected/healthy report data renders. No business write is replayed. / 点击实际重试连接按钮后完成健康、能力及概要/完整报告读取；横幅消失，显示模拟的已连接及健康状态。本次恢复是手动重试，无业务写入重放。
- `managed-narrow-offline-banner-mock.png`: At 900px width, the actual Local file-preview drawer was open. A programmatic DOM click on the actual Managed Agents button behind the modal switches the real App to its real Managed Provider. The drawer disappears and the service banner remains. This controlled transition verifies rendering conditions; it does not establish that ordinary users can click a modal-covered button. / 900px 窄屏中先打开实际 Local 文件预览抽屉，再对被 modal 遮挡的实际 Managed Agents 按钮执行程序 DOM 点击，让真实 App 切换到实际 Managed Provider。抽屉隐藏，服务横幅保留。这是验证显示条件的受控切换，不声称用户可以常规点击被遮挡的按钮。

`verification.json` contains sanitized checks and screenshot hashes. Zero browser JavaScript errors; expected resource-console failures from the injected outage and auxiliary mock 401 routes are retained as counts, rather than claiming a silent console. A tiny test init helper supports names in tsx-serialized official SSE fixture functions. No product components or render state were replaced.

`verification.json` 包含脱敏检查与图片哈希。浏览器 JavaScript 错误为零；注入断线及辅助 mock 401 路由产生的资源控制台错误按计数如实保留，不宣称控制台零错误。测试初始化补充了 tsx 序列化官方 SSE fixture 时所需的命名辅助函数，未替换产品组件或伪造渲染状态。
