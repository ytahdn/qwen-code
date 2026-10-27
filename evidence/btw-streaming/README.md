# Web Shell BTW streaming evidence

Implementation: ytahdn/qwen-code@3b186376e455ab07566a3a813cb5035407daf644, based on QwenLM/qwen-code main dd243bd019.

The after screenshots show the actual browser UI with mocked daemon snapshots. They do not validate real provider or Git operations. Screenshot 00 is a historical before-auto-follow baseline with streaming already present, not the old JSON BTW endpoint. Screenshots 02/03 show paused/resumed following; 05 shows a resumed answer; 06 preserves partial text after an error. Final implementation browser checks: 12 permanent desktop/mobile BTW cases plus one default-follow capture, all passed. Screenshots were visually inspected.

实现提交：3b186376e455ab07566a3a813cb5035407daf644。After 截图为实际浏览器 UI 配合模拟 daemon，并非真实模型提供商或 Git 操作验证。00 是已有流式输出、尚未实现自动跟随时的历史基线，不是旧 JSON BTW 接口。02/03 展示暂停和恢复跟随，05 展示重连后的答案，06 展示错误后保留部分文本。最终实现的 12 项桌面/移动端 BTW 测试和 1 项默认跟随截图测试均通过，截图已目视检查。
