# Files tree upload UI evidence / 文件树上传界面证据

Actual browser E2E, actual Pierre tree, simulated daemon. These images document UI only; they do not verify filesystem or Git operations. / 实际浏览器 E2E、实际 Pierre 树、模拟 daemon。截图仅说明界面，不验证文件系统或 Git 操作。

- before.png: before dropping files / 拖放前。
- progress.png: one of two equal-size root files completed; bottom bar at 50% / 两个等大小根目录文件之一完成，底部进度50%。
- completed.png: root and nested uploaded files inserted / 根目录及嵌套文件已插入。
- collapsed-progress.png: progress remains visible at panel bottom with tree collapsed / 收起树后面板底部进度仍可见。
- collapsed-error.png: simulated HTTP403 error remains visible and dismissible with tree collapsed / 收起树后模拟HTTP403错误仍可见且可关闭。

Synthetic cancelable drag events verify defaultPrevented on Files DOM surfaces. Embedded iframe documents and native OS drag navigation were not tested. / 通过可取消的合成拖放事件验证文件面板DOM上的defaultPrevented，未测试iframe内部文档或真实操作系统拖放导航。
