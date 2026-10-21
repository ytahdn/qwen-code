# Directory recovery UI evidence

Implementation: bf91f648e79580d7db4da5d8704863ec0927d441.

Actual Web Shell browser captures against an isolated loopback mock daemon. Both show the same synthetic completed session. The real interruption detector produces interrupted_prompt without directory provenance and none with provenance; the mock serves those statuses to the UI. Before shows the interruption banner and Continue action, after shows neither, with the completed transcript still visible. These images verify UI rendering/refresh, not real daemon relocation, real Git operations or real provider responses. No original session was accessed, real token read, prompt submitted, or model called.

# 中文说明

使用独立 loopback 模拟 daemon 捕获的实际 Web Shell 浏览器截图。两图展示同一个模拟已完成会话；真实中断分类器在没有目录来源标记时得到 interrupted_prompt，有标记时得到 none，模拟服务将对应状态提供给界面。修复前显示中断横幅及继续执行按钮，修复后两者都消失，已完成会话内容保持可见。这些图片验证 UI 展示和刷新，不代表真实 daemon 目录恢复、真实 Git 操作或真实模型响应验证。没有访问原会话、读取真实 token、提交 prompt 或调用模型。
