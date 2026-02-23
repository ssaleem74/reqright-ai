# ReqRight AI

**LLM-powered systems engineering workbench** — INCOSE GtWR v4 · 42 Rules · Smart Rewrite · Requirement Generation

> 🔀 **This is the AI development branch** of [ReqRight](https://github.com/ssaleem74/reqright). The stable v2.6.0 release lives in the original repo.

---

## What's Different Here

ReqRight AI extends the core workbench with optional LLM integration:

| Feature | ReqRight (stable) | ReqRight AI (this repo) |
|---------|:-:|:-:|
| 42-rule quality analysis | ✅ | ✅ |
| Rule-based auto-fix (offline) | ✅ | ✅ |
| 6 integrated modules | ✅ | ✅ |
| **LLM-powered smart rewrite** | ❌ | 🚧 |
| **Generate from natural language** | ❌ | 🚧 |
| **Requirement decomposition** | ❌ | 🚧 |
| **AI risk/decision suggestions** | ❌ | 🚧 |

### Design Principles

- **Opt-in only** — LLM features require the user to provide their own API key
- **Offline-first preserved** — all core features work without internet
- **Privacy-first** — API key stored locally, never exported, user controls data flow
- **Provider-agnostic** — supports Anthropic Claude and OpenAI (more later)

---

## Implementation Roadmap

| Phase | Feature | Status |
|:-----:|---------|:------:|
| 1 | Settings panel — API key, provider, model, connection test | 🔲 |
| 2 | LLM smart rewrite (single requirement) | 🔲 |
| 3 | Batch rewrite (fix all low-scoring requirements) | 🔲 |
| 4 | Generate requirement from natural language description | 🔲 |
| 5 | Decompose into child requirements | 🔲 |
| 6 | AI risk/decision suggestion from requirements | 🔲 |

---

## Architecture

```
Browser (reqright.html)
  │
  ├── Core Engine (offline, always available)
  │   ├── 42-rule quality scoring
  │   ├── Rule-based auto-fix
  │   └── All 6 modules
  │
  └── LLM Layer (opt-in, requires API key)
      ├── Settings panel (key, provider, model)
      ├── Smart rewrite (context-aware)
      ├── Requirement generation
      ├── Decomposition
      └── Risk/decision suggestions
      │
      ▼
  External API (user's key)
  ├── Anthropic Claude API
  └── OpenAI API
```

All API calls are made directly from the browser — no backend proxy needed.

---

## Base Version

Built on ReqRight v2.6.0 which includes:

- **42-Rule Quality Engine** with custom weights and 5 presets
- **36 Requirement Templates** across 9 categories
- **Excel Import** with column mapping and multi-sheet support
- **Comments & Review** workflow with auto-status updates
- **Version History** with field-level change tracking
- **6 Modules**: Requirements, Risks, Decisions, Stakeholders, Interfaces, Use Cases
- **PDF Reports** with 3 layout options
- **Export**: JSON, CSV, ReqIF

---

## Getting Started

1. Open `reqright.html` in any modern browser
2. Everything works immediately (offline, no setup)
3. For LLM features: open Settings → add your API key → test connection

---

## Example Projects

| Project | Domain | File |
|---------|--------|------|
| AegisGuard Smart Home Security | Consumer IoT | `SmartHome_Security_System_TestData.json` |
| SkyNav X200 UAV Flight Control | Aerospace / Defence | `example-aerospace-uav.json` |
| VitaMonitor Pro Patient Monitor | Medical Device | `example-medical-device.json` |

---

## Links

- **Stable release**: [github.com/ssaleem74/reqright](https://github.com/ssaleem74/reqright)
- **Landing page**: [ssaleem74.github.io/reqright](https://ssaleem74.github.io/reqright)
- **User Guide**: [ssaleem74.github.io/reqright/user-guide.html](https://ssaleem74.github.io/reqright/user-guide.html)

---

## License

MIT — see [LICENSE](LICENSE)

Based on INCOSE® Guide to Writing Requirements v4. INCOSE® is a registered trademark of the International Council on Systems Engineering. This is an independent educational project.
