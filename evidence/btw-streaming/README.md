# Web Shell BTW streaming evidence

Implementation: ytahdn/qwen-code@6086e475338eaf3c8fea499769473a4ca8a3d77b, based on QwenLM/qwen-code main8d4e2d4f32, including the existing history-smoke budget fix067090d195 (#15656). The BTW patch is unchanged from3b186376e4.

After screenshots were freshly captured and visually inspected at this implementation head using the real browser UI with mock daemon snapshots. They do not validate real model providers or Git operations. Screenshot00 is the historical before-auto-follow baseline, when BTW streaming already existed; it is not the old JSON endpoint.02/03 show paused/resumed following;05 shows a resumed answer;06 preserves partial text after error.12 permanent BTW cases and one default-follow capture passed. The unchanged4x CPU/2400-record history scenario plus16-record control passed4 repeated runs with upstream's300s budget.

实现提交：6086e475338eaf3c8fea499769473a4ca8a3d77b，基于main8d4e2d4f32，已包含上游既有历史导航smoke预算修复067090d195 (#15656)；BTW补丁与3b186376e4一致。After图片均在此head重新捕获、目视检查，使用实际浏览器UI和模拟daemon，不代表真实模型提供商或Git操作。00为自动跟随修改前、已有流式输出的历史基线，不是旧JSON接口。02/03为暂停/恢复跟随，05为重连后的答案，06为错误后保留部分文本。12项永久BTW用例及1项默认跟随截图均通过。保留4倍CPU/2400条记录的历史场景及16条对照，在上游300秒预算下重复验证4次通过。
