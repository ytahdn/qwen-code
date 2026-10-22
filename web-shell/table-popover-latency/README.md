# Table popup latency evidence

[English](README.md) | [简体中文](README.zh-CN.md)

## Sources and environment

Implementation commit: `d389055b6357f994987e2f3fe3725d97cceee661`. Before screenshots use the byte-verified original table module from `240eecf6178bb5be43061c0327e3cd62273a2695` inside the same current host. After screenshots use the actual implementation above. The image filenames identify each source and popup. These are browser E2E screenshots of the real local Web Shell UI using a simulated daemon and synthetic table data; they are not screenshots of a deployed DataWorks change or proof of real Git/backend operations.

Local platform: macOS arm64, Node.js 22.14.0, headless Chromium. Screenshot fixture: 76 rows × 3 columns, 1280 × 900 viewport, English, light theme. The committed functional suite also covers an 80-row/10-column table, ordinary and Shadow DOM portals, and inline/fullscreen modes.

## Observed results

Each of Copy, density, text operator and numeric operator sets body pointer-events to `none` and one scroll lock before the fix. The final implementation leaves pointer-events empty and adds no scroll lock. Cell-detail/fullscreen dialogs retain their intentional locks. The screenshot JSON records the exact open states and source/fixture provenance.

## Performance

A separate controlled run used the same 76 rows, all mounted, and the same actual built stylesheet (3,445,414 characters) for both table modules, after builds and functional tests were idle. Six openings per popup; warm medians omit the first opening. Timing measures native pointerdown to the second requestAnimationFrame after popup insertion, not live Event Timing or a guarantee of deployed latency. Style time uses CDP metrics. Raw samples are in `performance-samples.json`.

| Popup | Warm elapsed before→after(ms) | Warm style recalculation before→after(ms) |
| --- | --- | --- |
| Copy |272.1→74.9|258.8→65.4|
| Density |269.1→75.4|255.5→64.1|
| Text operator |191.3→15.5|171.2→2.6|
| Numeric operator |185.6→15.3|168.5→2.3|

## Validation

- Root `npm run build`, `npm run typecheck` and `npm run bundle`: passed.
- From `packages/web-shell`, `npx vitest run client/components/messages/EnhancedMarkdownTable.test.tsx`: 157 passed.
- From the same package, `PLAYWRIGHT_PORT=5197 npx playwright test --config playwright.config.ts client/e2e/web-shell.table-fullscreen.spec.ts --project=chromium --workers=1`: 16 passed, 1 intentional baseline-capture skip.
- Changed-file ESLint/Prettier, diff checks and bilingual links: passed.
- Independent popup ownership audit and the previously failing rapid Copy reopen/Escape regression: passed.
- Supplementary trusted native-touch test: 12 rapid selection/reopen cycles and 12 same-trigger close checks passed across all 4 menus. The 24 outside callbacks retained the original path containing their own trigger. Raw evidence is in `touch-observations.json`.
- Full 5-file review plus connected focus/state/portal/clipboard consumers: no actionable finding; implementation worktree remained clean.

## Limits

No deployed DataWorks build, Windows/Linux runtime, Safari/Firefox, React 18 host runtime or maximum 500-row × 50-column performance benchmark was tested. Screenshots document visible UI states; the body-lock assertions, functional suites and measured samples supply the behavior/performance evidence. These assets live on a separate evidence branch and are not part of the implementation branch.
