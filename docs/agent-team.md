# Agent team

I will use GitHub Copilot CLI in a Codespace to orchestrate the custom agent team building Mona's Project Pulse dashboard:

| Agent | Target model | Responsibility | Definition |
| --- | --- | --- | --- |
| **Orchestrator** | Claude Opus 4.7 (copilot) | Coordinates the specialist agents, divides the work into phases, manages file ownership and dependencies, and verifies the integrated result. | `.github/agents/orchestrator.agent.md` |
| **Planner** | Claude Opus 4.7 (copilot) | Researches the repository, documentation, dependencies, risks, edge cases, and validation needs, then produces an implementation plan without writing code. | `.github/agents/planner.agent.md` |
| **Coder** | GPT-5.5 (copilot) | Implements the dashboard logic and runnable application support with clear, deterministic, explicit, and testable code. | `.github/agents/coder.agent.md` |
| **Designer** | Gemini 3.1 Pro (copilot) | Shapes the dashboard's UI/UX, accessibility, information hierarchy, responsive behavior, visual clarity, and polished Project Pulse styling. | `.github/agents/designer.agent.md` |
