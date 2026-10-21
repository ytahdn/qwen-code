# Mock health contract smoke regression evidence

Source commit: `bfdaa131107e24eec64bd13a147b8e722bca7acb`. macOS arm64, Node.js22.14.0, formal original Playwright specs with Chromium and both configured mobile browser projects. The service is mocked. The only source change corrects the mock shallow `/health` response to match the real process-global route: `{"status":"ok"}` instead of invented `ok/healthy` fields. Production logic, test actions/assertions and CI definitions are unchanged.

The original4 failing cases were reproduced; overriding only the health response made all4 pass. Formal focused verification and a fixed-commit screenshot run each passed4/4. The complete original Smoke suite recorded **345 passed /1 failed**, workers4/retries0, no skips/retries. All four original CI failures passed. The separate local failure was a narrow-pane title-hover dialog timeout; five isolated runs produced4 passes /1 timeout, and one old-health-response control passed. These samples do not establish its root cause or prove it pre-existing/flaky. The original full and isolated failures are preserved, not relabeled as a clean run. No title logic, timeouts or assertions were changed. No wrapper or copied spec participated in formal verification. Public verification.json records the summary; raw traces containing local paths stay private.

The light/dark context screenshots show live usage15%, remaining85k and retained64% historical snapshot. The deletion screenshot shows Question3 removed and the reopen explanation. The sidebar screenshot shows the recovered Previous Session. All4 screenshots are actual final UI states from the passing formal cases and were visually inspected. A temporary toast from the deliberately injected503 can remain; this is not a claim that no errors occurred. Prompts/deletions are simulated by Playwright; these screenshots do not verify a real model, persisted backend or Git mutations. Existing real stop/restart evidence remains separately pinned to its actually verified implementation commit.

## 中文说明

源提交为上面的固定提交。macOS arm64、Node.js22.14.0，使用正式原始Playwright用例与实际Web Shell界面，覆盖Chromium及原配置的两个移动端浏览器项目，服务为模拟服务。本轮源码仅修正一行浅层`/health`模拟响应，使其与真实进程级接口一致：返回`{"status":"ok"}`，移除虚构的ok/healthy字段。生产逻辑、测试步骤/断言和CI定义均未改动。

原4个失败均已复现；仅覆盖健康响应的对照4/4通过。正式定向验证及固定提交截图验证分别4/4通过；完整原始Smoke套件记录为**345通过/1失败**，workers4/retries0，无跳过或重试；原4个CI失败全部通过。另一个本地窄分屏标题悬停弹窗超时，在5次独立运行中4次通过/1次超时，旧健康响应的1次对照通过；样本不足以确认其根因，也不能证明是既有flaky。首次全量与独立失败均保留，不改写成全绿。本轮没有修改标题逻辑、超时或断言。正式验证没有使用wrapper或复制的spec。verification.json记录脱敏摘要，带本机路径的原始trace不公开上传。

浅色/深色上下文图显示实时用量15%、剩余85k及保留的64%历史快照；删除图显示Question3消失并保留重新打开会话的提示；侧边栏图显示Previous Session恢复。4图均取自通过后的实际最终UI并已目视检查。主动注入503产生的短暂toast可能仍在，不能描述为从未报错。prompt/删除由Playwright模拟，截图不能证明真实模型、后端持久化或Git写操作；既有真实停机/重启证据仍按其实际验证提交独立保留。
