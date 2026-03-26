---
keyword: ARCHITECTURE
triggers: [interface, module, save system, multiplayer, audio, infrastructure, DDD, design]
---

# Architecture Rules

## Design Principles

- Feature-based folder structure with shared Core
- Interfaces define contracts between modules
- `/design-an-interface` before any new module (3+ radically different designs)
- `/ubiquitous-language` for consistent terminology

## Core Decisions

<!-- Document your architectural decisions here. Examples: -->
- Save system behind an interface (local now, cloud later)
- Multiplayer stubs (server-authoritative sessions) — not implemented yet
- Three independent audio channels: Game SFX, Voice, Ambiance
- Future infra: Pulumi (TypeScript) in `/infra` folder
