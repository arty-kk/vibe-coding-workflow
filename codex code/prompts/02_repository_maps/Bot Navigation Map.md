# Bot Navigation Map

## Mode

- Use the active `AGENTS.md` chain.
- Plan/documentation mode: create or update a repository map, not product behavior.

## Goal

Create or update `docs/nav_map.md` as a current map of bot entry points, states, transitions, commands, keyboards, and recovery paths.

## Inspect

Commands, message/callback handlers, routers, scenes/FSM states, keyboards, templates, middleware, auth/permissions, scheduled/proactive messages, deep links, persistence, tests, docs, platform config, and generated maps if present.

## Map content

### Evidence and IDs

- Write or update `docs/nav_map.md` when the environment allows it. If writing is unavailable, print the complete markdown content in chat.
- Use stable IDs and preserve existing IDs when refreshing: entry `E-*`, state `S-*`, transition `T-*`, keyboard `K-*`.
- Anchor every entry to current repository evidence with `path:line[-line]` plus symbol when possible.
- Distinguish source-of-truth implementation from generated docs, generated clients, stale docs, and inferred behavior.
- Capture unknowns only when they affect future audit or implementation.

### Coverage

Separate user-facing, admin/staff, group/private, and system/proactive states when present. Capture reachability, restart/recovery behavior, stale callback paths, and permission/chat-type boundaries.

### Entry details

For each entry/state/transition, capture trigger, owner symbol, guards/permissions, chat type, rendered copy or template source, keyboard/actions, next states, validation/errors, async/proactive behavior, persistence effects, tests, and known gaps.

## Markdown structure

Use a readable markdown hierarchy with summary first, then diagram or transition list, entry points, states, transitions, canonical commands per state, keyboards, cross-cutting behavior, reachability, unknowns, and assumptions. Omit sections that do not exist in the repo. Do not invent surfaces, states, commands, endpoints, or contracts.

## Final response

Respond in Russian with compact status sections: ✅ map created/updated, 📁 file, 🔎 strongest evidence anchors, 🧪 checks/spot-checks, ⚠️ assumptions/unknowns.
