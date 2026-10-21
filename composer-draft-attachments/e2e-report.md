# Composer draft attachments — verification evidence / 验证证据

Implementation commit / 实现提交: `9c3d7617db8c6848f6e82654f0d65ada5bc2fad5`.

Tested on macOS with Node.js 22, Chromium Playwright, React/CodeMirror, and native browser IndexedDB/File. Product sources were unchanged between the recorded final runs and this commit; the pre-commit formatting/lint checks passed. / 在 macOS、Node.js 22、Chromium Playwright、React/CodeMirror 和浏览器原生 IndexedDB/File 上验证。最终运行后至此提交，产品源码未变；提交前格式与 lint 检查通过。

## Automated results / 自动验证结果

| Check / 检查 | Result / 结果 |
| --- | --- |
| Related permanent tests, 8 files / 8 个文件中的相关永久测试 | 295/295, exit 0; latest complete review run 4.47s / 最近完整复审运行 4.47 秒 |
| Full root build, bundle, typecheck / 全仓构建、bundle、类型检查 | exit 0 |
| Changed-file ESLint, Prettier, diff check / 改动文件 lint、格式与 diff 检查 | passed / 通过 |
| Browser attachment scenarios / 浏览器附件场景 | 3/3, 20.6s |
| Browser shared-session scenarios / 浏览器同会话场景 | 4/4, 17.8s; zero page errors / 页面异常为零 |
| Migration acceptance DOM cases / 迁移接受确认 DOM 场景 | 4/4, 5.44s; includes exact-HEAD attachment control / 含精确 HEAD 附件对照 |
| Additional allocation/layout timing check / 额外分配与 layout 时序检查 | 3/3 across current, pre-fix snapshot and exact HEAD; candidate excluded / 当前、修复前快照和精确 HEAD 三版本通过，排除候选问题 |

## Browser scenarios / 浏览器场景

1. Reload restores text, PNG and native File; A/B navigation preserves separate drafts; accepted A admission clears its archive without changing B. / 刷新恢复文字、PNG 与原生 File；A/B 切换保持独立草稿；A 被接受后清理自己的存档，不改变 B。
2. A real native IndexedDB transaction holds restoration. Send and Enter remain blocked; a newly added same-name file and the archived file both survive with distinct names after release and reload. / 原生 IndexedDB 事务阻塞恢复期间，发送按钮与回车均不能提交；放行并刷新后，新增和存档的同名文件均保留，名称区分。
3. A mocked HTTP 202 is delayed while the user writes new text and adds Y. Acceptance and a B→A round trip preserve the new draft. / 模拟 HTTP 202 延迟期间输入新文字并添加 Y；接受确认及 B→A 切换后保留新草稿。
4. Main and same-session split share text and X/Y/Z immediately, then retain them after reload. Holding one native FileReader start blocks submission in the main view and the newly opened split; releasing the original reader restores the interactive composer's Send action. / 主视图与同会话分屏即时共享文字和 X/Y/Z，刷新后仍保留。控制一个原生 FileReader 的启动时机时，主视图及新开的分屏都阻止提交；放行原生读取后，当前可交互输入框恢复发送。
5. Real remove controls and text deletion empty both views; adding Z and reloading does not resurrect X/Y. / 实际删除控件与文字删除会清空两侧；之后添加 Z 并刷新，不恢复 X/Y。
6. Submission from a same-session split produces one prompt, clears both editors and the native archive, and stays empty after reload. / 同会话分屏提交仅产生一次 prompt，清空两侧输入框及原生存档，刷新后仍为空。
7. Two split sessions keep independent text, Files and removals, including Home/sidebar navigation. / 两个不同会话分屏的文字、File 与删除操作彼此独立，包含返回 Home 和侧栏切换。

## Exact payloads and screenshots / 精确载荷与截图

The accepted PNG upload was 10,689 bytes and matched the original byte-for-byte (SHA256 `daf02e424ed147c697a899510ce4ecd2b20c5541013396cc75cd35136bc37db5`). The accepted notes upload was 22 bytes with exact content `original notes payload`. Native stored same-name Files retained `new different content` (21 bytes) and `archived original content` (25 bytes). Shared-session upload/File contents were also independently checked. / 已接受的 PNG 上传为 10,689 字节，与原始数据逐字节一致（SHA256 同上）；notes 上传为 22 字节，内容精确为 `original notes payload`。原生存储的同名 File 分别保留 `new different content`（21 字节）和 `archived original content`（25 字节）。同会话场景的上传与 File 内容也单独核验。

All 17 final browser screenshots were individually inspected. Three representative actual UI captures are included on this independent assets branch: reload restoration, shared split X/Y/Z, and newer draft preserved after delayed acceptance. / 最终 17 张浏览器截图均已逐张目视检查。本独立素材分支包含三张代表性的实际 UI 截图：刷新恢复、同会话分屏 X/Y/Z，以及迟到接受确认后保留新草稿。

## Boundaries / 验证边界

Daemon HTTP/SSE, capabilities, upload responses and prompt HTTP 202 admission are simulated. Browser UI, navigation, File objects, original native FileReader after gate release, IndexedDB structured cloning/transactions, reloads and serialized upload bytes are real. These results do not verify a real daemon/model, Git backend or server-side stored payloads. Mobile coverage is textarea DOM regression coverage, not a mobile browser/device run. The focused migration/layout cases use the actual hook with jsdom/fake IndexedDB; they are not presented as browser capacity-dialog coverage. / daemon HTTP/SSE、能力信息、上传响应和 prompt HTTP 202 接受均为模拟；浏览器 UI、导航、File 对象、放行后的原生 FileReader、IndexedDB 结构化克隆与事务、刷新及序列化上传字节为真实执行。本结果不验证真实 daemon/模型、Git 后端或服务端保存载荷。移动端覆盖来自 textarea DOM 回归，不是移动浏览器或设备运行。迁移/layout 专项使用真实 hook 与 jsdom/fake IndexedDB，不作为浏览器容量恢复弹窗的验证。

Implementation changes merge cleanly with the fetched origin/main `021dc1fdd6dc0a31b3ee1f4277f640ab7ae3f63f` in a read-only merge-tree check. Full functional verification above ran on the PR head, whose parent is `731c8d6d252fee5b03a6a6d6a430c8d664571189`; the merged latest-main runtime was not rerun locally. / 只读 merge-tree 检查确认实现可与拉取的 origin/main `021dc1fdd6dc0a31b3ee1f4277f640ab7ae3f63f` 无冲突合并。上述完整功能验证运行于 PR head，父提交为 `731c8d6d252fee5b03a6a6d6a430c8d664571189`；本地未重跑与最新 main 合并后的运行时。
