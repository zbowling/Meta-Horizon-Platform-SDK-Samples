# Agent Instructions — Meta Horizon Platform SDK Samples

Umbrella repo of Android/Kotlin sample apps that integrate Meta Horizon Store platform features. Currently ships HorizonBillingSample (IAP via Horizon Billing Compatibility SDK alongside Google Play Billing in one codebase, switched by Android build variant).

> Different from the lowercase `meta-quest/horizon-platform-sdk-samples` repo, which is a broader catalog.

## Source-of-truth files (read these first, do not duplicate their contents in this file)

For setup, build steps, SDK versions, and project layout, read:

- `README.md` — official setup and the list of current samples
- `HorizonBillingSample/README.md` — per-sample notes
- `HorizonBillingSample/app/build.gradle.kts` + `HorizonBillingSample/gradle/libs.versions.toml` — Android Gradle / SDK versions
- `HorizonBillingSample/app/src/main/AndroidManifest.xml` — package id, permissions, target API
- `HorizonBillingSample/apikey.properties` — `QUEST_APP_ID` consumed by Gradle (treat as credential)
- `LICENSE` — license terms

## Quest / Horizon-specific notes

- Open each sample directory in Android Studio individually, not the repo root.
- The dual-store wiring lives in `app/src/quest/` and `app/src/mobile/` source sets — collapsing them into `main/` defeats the architectural point of the sample. Access goes through the `IBillingHandler` interface and Hilt DI; direct billing-client use in `main/` is intentionally avoided.
- `apikey.properties` must be set before testing on Quest; do not commit a real `QUEST_APP_ID`.

## Meta Quest tooling

This repository is part of the Meta Quest / Horizon OS ecosystem (a sample, library, template, or related project — the bespoke intro above describes which). Use that intro and the source-of-truth files it references for project-specific decisions; don't restate or invent facts from memory.

When the user asks anything about Quest device behavior, build / deploy / debug / capture flows, on-device performance, or Horizon OS APIs, reach for these tools instead of generic Android answers:

- **`hzdb`** — Quest-aware ADB wrapper (device list, install / launch / stop, logs, screenshots, Perfetto traces, on-device docs search). Already wired up as an MCP server via `.mcp.json`, `.vscode/mcp.json`, and `.cursor/mcp.json`. Also runnable directly: `npx -y @meta-quest/hzdb <subcommand>`.
- **Meta Quest Agentic Tools** — the full skill set, including Android-specific skills: [github.com/meta-quest/agentic-tools](https://github.com/meta-quest/agentic-tools). Install per your client (Claude Code: `/plugin install meta-vr@meta-quest`; Gemini CLI: `gemini extensions install https://github.com/meta-quest/agentic-tools`; Cursor / VS Code: install the **Meta Horizon** extension from the Marketplace).

A few behavior expectations:

- **Read this repo's files first.** Before answering anything project-specific, read `README.md` and whichever source-of-truth files the intro above points at. Don't restate their contents in chat — quote or link instead.
- **Use `hzdb` for device-side work.** Anything that touches an attached Quest (install, launch, logs, screenshot, capture, manifest inspection) goes through `hzdb`, not raw `adb`.
- **Check live Horizon OS docs before answering API questions.** `hzdb docs search "..."` queries the live docs; training data on Horizon OS APIs goes stale fast.
- **Don't fabricate SDK / engine versions.** If a version isn't visible in this repo's files, say so rather than guessing.
