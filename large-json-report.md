# PR12050 — large JSON / JSONL actual export verification

Runtime source: `f7df42c53f5a977571d65f227768b190d5b1973e` (built in isolated followup worktree; later `0b18d0588a` changes documentation only). Actual bundled daemon on 4197 and production-served Web Shell; Chrome 152, 1680×1050 viewport. No daemon, export-command, network or artifact mocks. No production edits.

An isolated persisted session was seeded with explicitly synthetic history: a constructed `read_file` result containing 6,273,055 UTF-8 bytes and a final sentinel. This is test data, not model-produced history or actual tool execution. Browser composer submitted real `/export json` and `/export jsonl`. Input responsiveness probes were unsent drafts; background suggestion `/generate` requests may occur, so this report does not claim zero model calls.

## Functional observations

Both actual commands wrote workspace files, emitted success text, and produced one artifact card per command. Both previews loaded the entire source; the CodeMirror document was compared byte-for-byte (UTF-8 source text) with the exported file, including final sentinel and closing content. UI downloads matched filesystem bytes. Reload retained exactly two cards without duplication. Screenshots show commands, cards and complete source tail; visually inspected.

- **JSON**: `qwen-code-export-2026-09-17T07-11-48-733Z.json`, 6,281,572 bytes; SHA-256 `f3d50d47027a4d2c374692a6d80b12dd189ee28db4ba7934c377449b094958e9`; download SHA-256 identical.
- **JSONL**: `qwen-code-export-2026-09-17T07-11-52-695Z.jsonl`, 6,281,243 bytes; SHA-256 `148227241ec470731468d8d99bf1194a9bd7bc55844ab5cf5e866843d6e97a31`; download SHA-256 identical.

## Responsiveness: bounded result, not blanket pass

A separate measurement run isolated (1) opening preview through 1.5 seconds after editor mount, (2) real editor jump to end plus 1.5 seconds, and (3) input plus 1 second after settling. Main-frame PerformanceObserver long tasks and requestAnimationFrame gaps were recorded. These windows exclude full-document inspection and cross-process transfer used by functional checks.

| Format | Open long task ≥50ms | Open frame gap >50ms | Jump to end | Settled input acknowledgement | Settled long tasks/gaps |
| --- | --- | --- | --- | --- | --- |
| JSON (6,281,572 bytes) | none observed | none observed | none observed | 14 ms | none observed |
| JSONL (6,281,243 bytes) | **818 ms** | **816.6 ms** | none observed | 8 ms | none observed |

**JSONL opening exhibits a noticeable temporary main-page stall.** The constructed history makes JSONL contain a roughly 6 MiB single line, matching the format's one-record-per-line behavior. No source attribution/profiler analysis was performed; this evidence establishes a stall, not its exact internal cause. Once settled, observed input and tail navigation remained responsive. JSON did not show a >50ms stall in this sample. Initial loading input acknowledgements were 14ms (JSON) / 10ms (JSONL), but occurred early and do not negate the later JSONL long task.

The first functional probe used an outdated CodeMirror property and timed out; replacing it with the current property corrected the test. A combined functional/performance window also recorded an 890ms JSONL long task; the independent isolated run above confirms the opening stall without that probe cost. These are local single-run measurements, not comparative benchmarks. They do not establish safety at 100 MiB, across devices, for every text format, split view, or multiple workspaces.

结论：约 6 MiB 的 JSON / JSONL 真实导出、卡片、完整源码、下载字节一致性与重载去重通过；JSONL 打开阶段实测约 0.8 秒主线程停顿，加载后未观察到持续卡顿。不能将这一结果描述为大文件性能全部通过或 100 MiB 安全。

Published evidence: [JSON screenshot](export-json-tail.png), [JSONL screenshot](export-jsonl-tail.png), and [isolated timing measurements](large-json-perf.json). Full functional results, exports and daemon logs remain local working data.
