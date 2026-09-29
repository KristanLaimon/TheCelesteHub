# Agent Knowledge & Tooling (`.agents/`)

This directory contains knowledge base files, design specs, feature roadmaps, and automated post-code-change verification hooks for developer and AI agent workflows in **TheCelesteTracker Desktop**.

---

## Directory Structure

```text
.agents/
├── brain/                  # Second Brain knowledge base (numbered thought/learning files)
│   ├── 01-second-brain-convention.md
│   └── ...
├── DESIGN.md               # UI design specification & layout architecture
├── TODO.md                 # Project roadmap & pending feature tasks
├── settings.json           # Agent hooks and plugin settings
├── hooks.json              # Hook definitions for automated agent systems
├── post-code-change.js     # Cross-platform post-change verification runner (Bun)
├── post-code-change.ps1    # PowerShell post-change verification runner (Windows)
├── post-code-change.sh     # Bash post-change verification runner (Linux / WSL / macOS)
└── README.md               # Directory overview & usage instructions
```

---

## Available Hooks & Scripts

- `post-code-change.ps1`: PowerShell execution script (Windows native).
- `post-code-change.sh`: Bash execution script (Linux / WSL / macOS).
- `post-code-change.js`: Cross-platform JS script executable with `bun .agents/post-code-change.js`.
- `hooks.json`: Agent hook definitions file for automated agents.

## Automated Verification Flow

The scripts execute the mandatory 4-step post-flow verification process sequentially (as defined in [AGENTS.md](../AGENTS.md)):

1. `bun test`: Runs unit and integration tests under the Bun test runner.
2. `bun run check`: Performs Svelte component and TypeScript type checking (`svelte-check` + `tsc`).
3. `bun run lint:fix`: Runs Biome code auto-fixing (`biome check . --write --unsafe`).
4. `bun run check`: Re-verifies type correctness after formatting and auto-fixes.

## How to Run

```bash
# Via Bun (Cross-platform)
bun .agents/post-code-change.js

# Via PowerShell (Windows)
powershell -ExecutionPolicy Bypass -File .agents/post-code-change.ps1

# Via Bash (Linux/Mac/WSL)
bash .agents/post-code-change.sh
```
