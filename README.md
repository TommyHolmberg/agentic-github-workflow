# Agentic Vibe Flow (Local-First) 🚀

A zero-bloat, privacy-focused developer experience for "Vibe Coding." No Postgres databases, no third-party cloud services, and no manual token management. 

This toolkit turns your existing **GitHub Issues** into a Kanban board and uses your local **authenticated GitHub CLI** as the engine.

## ⚠️ Use at Your Own Risk
This toolkit provides AI agents with access to your local terminal and GitHub repository via the `gh` CLI. 
- **AI can make mistakes:** Always review the `PLAN.md` and the final PR before merging.
- **Terminal Access:** By design, these agents can execute commands on your system. Only use this in environments where you trust the agent's underlying model.
- **No Warranty:** This setup is provided "as-is." The authors are not responsible for accidental deletions, overwritten code, or rogue git pushes. **Trust, but verify.**

## 🛠️ How it works
1. **GitHub is the Source of Truth:** Your tasks and "vibe-checked" plans live on GitHub Issues.
2. **Local Execution:** Your agents (Claude, Gemini, Copilot) run locally on your machine.
3. **PowerShell Native:** Optimized for Windows developers using the `gh` CLI.

## 🚀 Quick Start (Windows)

### 1. Prerequisites
- [GitHub CLI (gh)](https://cli.github.com/) installed.
- Authenticated via `gh auth login`.

### 2. Global Installation
1. Create a folder for your scripts (e.g., `C:\scripts`).
2. Download `init-agentic-flow.bat` and `agentic_development.md` into that folder.
3. Add `C:\scripts` to your **Windows Environment Variables (PATH)**.

### 3. Initialize a Project
In any project folder (PowerShell/CMD), just run:
```powershell
init-agentic-flow

## 📄 License
MIT
