## Agent Onboarding and Initialization Requirements

This project follows a Specification-Driven Development paradigm and uses [GitHub Spec Kit](https://github.com/github/spec-kit/) as the primary framework for specification, planning, task decomposition, and agentic delivery.

The baseline project context is defined by:

- [.specify/memory/constitution.md](.specify/memory/constitution.md)
- [.specify/memory/progress.md](.specify/memory/progress.md)

Before performing any work on this repository, agents MUST load and interpret these documents and treat them as the authoritative source of project policies, constraints, and implemented system state.

## Shell Selection (Windows)

- If `bash` is on `PATH` (i.e., `bash --version` succeeds) → **MUST use Bash**
- Otherwise → **use PowerShell**
- Mixing shells is forbidden

## Desktop Boundary Rules

_(Only applies when implementing a desktop app)_

- Keep Electron-owned code in `electron/` or runtime boundary modules under `src/platform/` and `src/persistence/runtime/`.
- Renderer-facing modules under `src/` MUST NOT import `electron`, `node:fs`, or other Node/Electron-only APIs for desktop behavior.
- Desktop-only renderer access MUST flow through a typed `window.desktopApi` bridge exposed by preload.
- Desktop validation must preserve the browser-first fallback path: validate `npm run dev:web` before assuming a regression belongs to Electron.
- Preserve a pure browser workflow alongside desktop work; browser-mode changes must remain runnable without Electron.
