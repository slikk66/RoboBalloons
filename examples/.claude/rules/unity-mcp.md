---
keyword: UNITYMCP
triggers: [mcp__mcp-unity__*, "*.cs", "*.unity", "*.shader", "*.mat", Unity, scene]
---

# Unity & MCP Platform Rules

## MCP Tool Behavior

- `update_component` **ADDS** components if not found — it does NOT safely update. Before calling: verify component list via `get_gameobject`. Check component count. Never call repeatedly without checking.
- New script files need `Assets/Refresh` before MCP can reference them.
- Wait a few seconds after recompile before calling MCP tools.

## Scene Editing

- **Never make scene changes during play mode** — they revert on stop. Confirm with user or check `get_scene_info` first.
- **Audit scene state BEFORE making changes.** Check for anomalies (duplicate components, stale references, unexpected hierarchy). Fix anomalies before proceeding.
- **`save_scene` overwrites YAML edits.** If you edited the scene YAML directly, do NOT call `save_scene` — it will write Unity's in-memory state back to disk, destroying your edits. Use `load_scene` to reload from disk instead.
- When editing scene YAML directly, always `load_scene` afterward so Unity picks up the changes.

## Serialization

- **Serialized scene values override code defaults.** Changing a `[SerializeField]` default in code does NOT update the scene. For existing fields, edit the scene YAML directly. Only new (never-serialized) fields use code defaults.
- **Always verify with `grep` after changing serialized values.** Check both the code file AND the scene file to confirm they match.

## C# Conventions

- All MonoBehaviours should use `[DisallowMultipleComponent]` unless multiples are intentional.
- New C# module? Run `/design-an-interface` first.
- Testable logic? `/tdd` is mandatory.
