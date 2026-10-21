---
title: "OrangeGel Architecture Overview"
description: "Inside the Rust + Tauri v2 backend, Unix PGID process supervisor, PathGuard, and Angular 19 signal state store."
date: 2026-10-20T12:30:00Z
draft: false
tags:
  - architecture
  - rust
  - tauri
  - angular
categories:
  - engineering
---

## Why Rust + Tauri v2 + Angular 19?

OrangeGel is designed from the ground up to eliminate orphan dev-server processes, front-matter corruption, and single-viewport preview limitations:

1. **`PathGuard` Canonical Containment** — Every file read, write, and content scaffold operation resolves canonical paths and rejects traversal or external symlinks.
2. **Unix PGID Process Group Supervision** — Child dev servers and Tailwind watchers spawn inside dedicated process groups (`process_group(0)`) and terminate cleanly via `SIGTERM` → 2s grace → `SIGKILL` to `-pgid`.
3. **Atomic Write-Then-Rename Persistence** — Both user documents and `.orangegel/project.json` use atomic temp-file persistence in the same directory.
4. **Multi-Device Preview Studio** — Switch instantaneously between [Multi-Device Preview](/features/multi-device-preview/) presets or inspect the [Top 20 SSGs](/features/top-20-ssgs/).

{{< mermaid >}}
sequenceDiagram
  participant UI as Angular 19 WorkspaceStore
  participant IPC as Tauri v2 Commands
  participant Sup as Rust PGID Supervisor
  participant SSG as Hugo / Top 20 SSG Server
  UI->>IPC: start_dev_server(includeDrafts: true)
  IPC->>Sup: spawn with process_group(0)
  Sup->>SSG: hugo server -D --port <free>
  SSG-->>Sup: stdout Ready URL
  Sup-->>UI: emit orangegel://ssg-status (Running)
{{< /mermaid >}}
