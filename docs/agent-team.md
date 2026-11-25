# Project Pulse Agent Team

This document summarizes the custom agent team defined in `.github/agents/` that will work together to plan, design, implement, and validate Mona's **Project Pulse** dashboard.

## Team Overview

| Agent | Model | Definition File | Responsibility |
| --- | --- | --- | --- |
| **Orchestrator** | Claude Opus 5.5 | `.github/agents/orchestrator.agent.md` | Coordinates the overall request, breaks work into phases based on the plan, delegates explicit file scopes to specialists, runs non-overlapping work in parallel, and verifies the integrated result. Does not write implementation code directly. |
| **Planner** | Claude Opus 5.5 | `.github/agents/planner.agent.md` | Researches the repository, identifies dependencies, edge cases, and risks, and produces an ordered implementation plan with explicit file ownership and validation expectations. Does not write code. |
| **Designer** | Gemini 3.7 Flash | `.github/agents/designer.agent.md` | Guides UI/UX, accessibility, information hierarchy, responsive behavior, and visual styling for Project Pulse (including polished project cards, status badges, priority treatment, and `.dashboard` / `.project-card` styles). |
| **Coder** | GPT-5.5 | `.github/agents/coder.agent.md` | Implements the static application logic, HTML structure, JSON data, and runnable app configuration (such as `.vscode/launch.json`) within its assigned file scope and validates the changes. |

## How the Team Works Together

1. **Coordination (Orchestrator):** Receives the Project Pulse dashboard request and delegates planning first rather than writing files in a single undifferentiated prompt.
2. **Planning (Planner):** Inspects `.github/project-pulse-brief.md` and repository structure, then outputs phases, file assignments, dependencies, parallel vs. sequential work decisions, and validation criteria.
3. **Implementation & Design (Designer & Coder):** Guided by the Orchestrator using non-overlapping file scopes:
   - **Coder** builds `app/index.html`, `app/project-data.json`, and `.vscode/launch.json`.
   - **Designer** crafts `app/styles.css` and guides visual hierarchy, accessibility, and card/badge polish.
4. **Validation & Handoff (Orchestrator):** Verifies that all files integrate cleanly, validates the dashboard and launch configuration, and prepares the final handoff.
