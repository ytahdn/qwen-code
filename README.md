# Web Shell export artifact evidence

Source commit: b7ea5bf61f82e8c8c83d687fb1a70e9acee8a012. Captured and visually inspected on 2026-09-17.

Actual App/ArtifactPanel with simulated daemon/file responses and CDN assets. HTML rendering uses the production parent CSP applied to the test page; unmodified Vite development support is not claimed. Large HTML/Markdown screenshots show complete source tails after five 256 KiB requests; downloaded bytes match the 1,048,603-byte synthetic fixtures. The real-renderer screenshot uses actual local renderer JS/CSS and the real formatter/template with synthetic messages, delivered via mocked CDN. No user export data is included. Screenshots do not verify real Git backend operations or a published CDN release.

## 中文

源码提交：b7ea5bf61f82e8c8c83d687fb1a70e9acee8a012。2026-09-17 捕获并目视检查。使用实际 App/ArtifactPanel，daemon/文件响应及 CDN 为模拟数据。HTML 渲染验证为测试页面应用生产父页面 CSP，不声明原样 Vite 开发环境已支持。大 HTML/Markdown 截图展示经过五次 256 KiB 请求后的完整源码尾部；下载与 1,048,603 字节的合成文件逐字节一致。真实 renderer 截图使用本地真实 JS/CSS、格式化器和模板以及合成消息，通过模拟 CDN 传输。不包含用户导出数据，也不代表验证真实 Git 后端操作或已发布 CDN 资源。
