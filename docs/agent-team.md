# Agent team for Mona's Project Pulse dashboard

We will use a four-agent team defined in the repository's custom agent folder and orchestrated from GitHub Copilot CLI in a Codespace. The agent definitions live under `.github/agents/` and are tailored for a design-and-build workflow around the Project Pulse dashboard.

- Planner — Model: Claude Opus 5.5 (copilot)
  - Responsibility: researches the repo, reviews docs and dependencies, and produces a practical implementation plan with file assignments, sequencing, validation expectations, and edge cases.
  - Definition: `.github/agents/planner.agent.md`

- Orchestrator — Model: Claude Opus 5.5 (copilot)
  - Responsibility: coordinates the full build, breaks the work into phases, delegates responsibilities to specialist agents, and verifies the integrated result before reporting back.
  - Definition: `.github/agents/orchestrator.agent.md`

- Coder — Model: GPT-5.5 (copilot)
  - Responsibility: implements code, fixes bugs, creates app support files when needed, and validates behavior within the scoped files assigned by the orchestrator.
  - Definition: `.github/agents/coder.agent.md`

- Designer — Model: Gemini 3.7 Flash (copilot)
  - Responsibility: focuses on UI/UX, accessibility, layout, interaction flow, and polished dashboard styling for the Project Pulse frontend.
  - Definition: `.github/agents/designer.agent.md`

This setup uses GitHub Copilot CLI in a Codespace to orchestrate the work across planning, design, and implementation, keeping the team focused on the Project Pulse dashboard deliverable.