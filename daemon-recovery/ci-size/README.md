# HTML export build verification / HTML 导出构建验证

Commit / 提交: `d68ff796481a3bee45bcf9bb96d538f6ca2cf2f6`.

The six current CI failures stopped at one shared prerequisite: renderer size 2,050,022 bytes against a 2,050,000-byte budget. Under the same dependencies, merged main 65051590d9 measures 2,048,235 bytes. Both builds have identical 2,174 input paths and unchanged third-party sources. The budget becomes 2,052,000 bytes, preserving the forbidden-dependency guard. Full local build, typecheck, CLI bundle and 18 related tests passed.

The screenshot is actual Chromium rendering of product HTML exported by the compiled CLI formatter from synthetic user/assistant records. Version-bound unpkg renderer/CSS requests were fulfilled with the exact local build bytes, retaining CSP/SRI. All nine checks passed, including visible Markdown and no JavaScript/console errors. The screenshot was visually inspected. This does not validate CDN publication, the interactive /export command, a real model or live backend. The browser closed; no services were started or operated. The full Web Shell suite was not rerun for this build-only change; the previously recorded local split-hover failure remains unresolved.

本轮六个 CI 失败都发生在同一个前置构建：渲染器 2,050,022 字节，超过原预算 2,050,000 字节。在相同依赖下，合入主线 65051590d9 为 2,048,235 字节。两次构建均有相同的 2,174 个输入路径，第三方源码未变。预算调整至 2,052,000 字节，禁止依赖的检查保留。完整本地构建、类型检查、CLI 打包与 18 项相关测试通过。

截图来自真实 Chromium，展示编译后的 CLI 产品导出器对合成用户/助理记录生成的实际 HTML。版本固定的 unpkg 渲染器和 CSS 请求由本地构建原字节响应，保留 CSP/SRI。9 项检查通过，包括 Markdown 可见、无 JavaScript/控制台错误；截图已目视检查。不代表验证 CDN 发布、交互式 /export、真实模型或活动后端。浏览器已关闭，未启动或操作服务。本次仅修改构建预算，没有重跑完整 Web Shell 套件；此前记录的本地分屏悬停失败仍未解决。

- `export-transcript-local-renderer.png`: actual screenshot / 实际截图。
- `verification.json`: exact scope, checks, hashes and cleanup / 准确范围、检查、哈希与清理。
