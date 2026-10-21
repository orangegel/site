---
title: "OrangeGel Studio — Native Static Site IDE"
description: "Modern Tauri v2 Static Site IDE & Multi-Device Preview Studio with Hugo as the preferred default and full support for the Top 20 Static Site Generators."
date: 2026-10-20T12:00:00Z
draft: false
tags:
  - tauri
  - hugo
  - angular
  - static-sites
categories:
  - studio
---

## Welcome to OrangeGel Studio

**OrangeGel** is a native desktop IDE and multi-device preview studio engineered with **Rust + Tauri v2** and **Angular 19 + Tailwind CSS + Three.js + Anime.js**. It succeeds [LycheeBox](https://github.com/orangegel/orangegel/blob/main/LYCHEEBOX.md) by replacing Go + Wails v2 with a memory-safe, process-group-isolated Rust supervisor and a responsive multi-viewport browser stage.

Explore key pages in this site:

- [Multi-Device Preview Studio](/features/multi-device-preview/) — Inspect Desktop, Tablet, Mobile, and 3-Up Split Matrix viewports simultaneously.
- [Top 20 Static Site Generators](/features/top-20-ssgs/) — First-class **Hugo** workflow plus 19 additional static site frameworks.
- [Architecture Overview](/posts/architecture-overview/) — Deep dive into the Rust process supervisor, `PathGuard`, and Angular signal store.

{{< mermaid >}}
flowchart LR
  A["Monaco Editor + Front-Matter Inspector"] --> B["Tauri v2 Typed IPC + PathGuard"]
  B --> C["Unix PGID Dev Server Supervisor"]
  C --> D["Multi-Device Preview Studio (Desktop / Tablet / Mobile / Split)"]
  B --> E["Firebase Hosting + Cloud Run Deploy Pipeline"]
{{< /mermaid >}}
