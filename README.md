# Web Shell SSE reconnect scroll evidence

Implementation: 08ecf651fa2abb89b98f723f0e7e0a7efa55ac28. Baseline: 731c8d6d252fee5b03a6a6d6a430c8d664571189.

Actual Chromium screenshots, visually inspected. Daemon HTTP/SSE are mocked. Baseline uses current-source Vite UI; fixed verification uses the built node dist/cli.js UI. Mouse-wheel input places the reader 2000 px above the bottom. After reconnect/replay_complete, baseline jumps to the bottom, while the fix preserves scrollTop=1257 and distance=2000. Captures demonstrate UI behavior, not real network, model, or Git backend operations. The fixed capture and initial reading capture are byte-identical.

实际 Chromium 截图，已目视检查；daemon HTTP/SSE 为模拟。基线使用源码 Vite UI，修复后使用 node dist/cli.js 打包 UI。鼠标滚轮将阅读位置置于距底 2000px；重连回放完成后，基线跳底，修复后保持 scrollTop=1257、距底 2000px。截图仅证明 UI 行为，不证明真实网络、模型或 Git 后端操作。修复后截图与初始阅读截图的字节完全一致。
