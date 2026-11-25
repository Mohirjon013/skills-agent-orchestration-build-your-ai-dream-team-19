# Project Pulse Implementation Plan

## Summary

This plan outlines the phased implementation of Mona's **Project Pulse** dashboard—a lightweight, contributor-friendly static web application that surfaces active projects, owners, current status, recent activity, and priority/risk levels.

## File Assignments and Responsibilities

| File | Owner | Responsibility |
| --- | --- | --- |
| `app/project-data.json` | **Coder** | Define structured JSON data with a top-level `"projects"` array where each item includes `name`, `owner`, `status`, `recentActivity`, and `priority`. |
| `app/index.html` | **Coder** | Build accessible semantic HTML with the exact title `"Project Pulse"`, link `styles.css`, fetch and render `project-data.json` into visible `.project-card` elements displaying status, recentActivity, and priority. |
| `app/styles.css` | **Designer** | Design a polished, responsive dashboard UI with `.dashboard` and `.project-card` selectors, `border-radius`, `box-shadow`, status badges, priority indicators, readable spacing, and accessible color contrast. |
| `.vscode/launch.json` | **Coder** | Create strict JSON (no comments) with a `"Run Project Pulse Dashboard"` configuration that serves from `${workspaceFolder}/app` via `python3 -m http.server 5500` and opens `http://localhost:%s/index.html` via `serverReadyAction`. |

## Implementation Phases

### Phase 1: Data Schema and Visual Direction (Parallel)
- **Coder** creates `app/project-data.json` with realistic Project Pulse sample projects.
- **Designer** defines the layout structure, card hierarchy, and styling tokens in `app/styles.css`.
- **Parallel work decision:** `app/project-data.json` and `app/styles.css` have no overlapping file scopes and can be authored in parallel once the shared field names (`name`, `owner`, `status`, `recentActivity`, `priority`) and CSS hooks (`.dashboard`, `.project-card`) are agreed upon.

### Phase 2: Dashboard Markup & Rendering (Sequential)
- **Coder** implements `app/index.html` to reference `styles.css`, load `project-data.json`, and render each project card with `.project-card` markup.
- **Dependencies:** `app/index.html` depends on the finalized JSON schema in `app/project-data.json` and the CSS class hooks (`.dashboard`, `.project-card`) established in `app/styles.css`.

### Phase 3: Launch Configuration (Parallel or Final)
- **Coder** creates `.vscode/launch.json` with the `"Run Project Pulse Dashboard"` configuration serving from `app/` and opening `index.html`.
- **Dependencies:** Depends on `app/index.html` existing as the entry point.

## Edge Cases to Handle

- Missing or failed `fetch('project-data.json')` should render an explicit, contributor-friendly error message instead of failing silently.
- Empty `projects` array should display an informative empty state.
- Long `recentActivity` strings should wrap cleanly without breaking card alignment on mobile or desktop viewports.

## Validation Expectations

- `app/project-data.json` and `.vscode/launch.json` must parse cleanly as strict JSON (`python3 -m json.tool`).
- `app/index.html` must render project cards in the browser with `Project Pulse` title, `styles.css` styling, and all five data fields (`name`, `owner`, `status`, `recentActivity`, `priority`).
- `app/styles.css` must include `.dashboard`, `.project-card`, `border-radius`, `box-shadow`, and responsive grid/flex behavior.
- Launching **Run Project Pulse Dashboard** must open `http://localhost:5500/index.html` showing the dashboard UI rather than a directory listing.
