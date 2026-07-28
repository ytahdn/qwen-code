# ToolSearch MCP preload threshold

## Problem

MCP tools are unconditionally deferred behind ToolSearch (`shouldDefer=true`
hardcoded in `DiscoveredMCPTool`). Deferral saves prompt tokens when many MCP
servers are attached, but it is not free: every mid-session reveal rewrites the
function-declaration list, which sits at the front of the tools→system→messages
prefix, so a single ToolSearch load invalidates the entire prompt KV cache. For
a small MCP set the deferral saves little and the cache damage plus the extra
ToolSearch round-trip make it a net loss.

Claude Code models this tradeoff with `ENABLE_TOOL_SEARCH=auto`: tools load
upfront if they fit within 10% of the context window, deferred otherwise. This
change adds the equivalent gate.

## Design

New setting `tools.toolSearch.threshold` (number, percent, default `10`).

At session start (`GeminiClient.startChat`, before the deferred-tools reminder
is resolved), when ToolSearch is registered and the threshold is > 0:

- Estimate the combined token footprint of every deferred MCP tool schema
  (`JSON.stringify(tool.schema).length / CHARS_PER_TOKEN`).
- If the total fits within `threshold`% of the context window
  (`contentGeneratorConfig.contextWindowSize`, falling back to
  `tokenLimit(model)`), reveal them all via the existing
  `revealDeferredTool` mechanism. All-or-nothing — a partial reveal would
  leave an arbitrary subset behind ToolSearch.
- Otherwise everything stays deferred (previous behavior). `threshold: 0`
  restores the old behavior unconditionally.

Preloaded tools therefore land in the initial declaration list, are filtered
out of the startup deferred-tools reminder, and the declaration list stays
stable for the whole session.

## Decisions

- **Session start only, never `setTools()`.** Revealing a tool the startup
  reminder already announced would make `queueAddedMcpToolsReminder` flag it
  as "removed", and a mid-session declaration change busts the very cache the
  preload exists to protect. Tools from servers that connect later stay
  deferred (announced via the added-tools reminder, reachable through
  ToolSearch) until the next session start. `/clear` clears the revealed set
  and re-runs the decision.
- **MCP tools only.** Bundled deferred tools (web_fetch, cron, monitor, …) are
  a deliberate curation of the initial declaration list, independent of MCP
  set size; they keep their existing behavior.
- **Already-revealed MCP tools count toward the budget** so repeated session
  starts (compression also passes through `startChat`) cannot ratchet the
  revealed set past the budget as servers come and go.
- **No preload when ToolSearch is unavailable** — the existing eager-reveal
  branch in `resolveDeferredToolsForReminder` already exposes everything.
