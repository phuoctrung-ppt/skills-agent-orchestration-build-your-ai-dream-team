# Mona's Project Pulse Dashboard Implementation Plan

## Summary

Build a lightweight static dashboard that lets contributors quickly understand active projects, ownership, current status, recent activity, priority or risk, and a short contributor-friendly summary. The app will use plain HTML, CSS, and JSON with no framework, build step, or runtime dependency.

The implementation must follow `.github/project-pulse-brief.md`, open `app/index.html` through the VS Code **Run Project Pulse Dashboard** configuration, and show the dashboard UI rather than a server directory listing.

## File assignments

| Owner | Files | Responsibility |
| --- | --- | --- |
| Planner | `docs/project-pulse-plan.md` | Define phases, ownership, dependencies, parallel work, risks, edge cases, and validation expectations. |
| Designer | `app/styles.css` | Create the polished responsive visual system, layout, spacing, typography, accessible contrast and focus states, status and priority treatments, and styling for `.dashboard` and `.project-card`. |
| Coder | `app/index.html` | Build the semantic dashboard shell, load the JSON data, render project cards, and display each project's name, owner, status, recent activity, priority, and summary. |
| Coder | `app/project-data.json` | Provide deterministic sample data in a top-level `projects` array. Every project must include `name`, `owner`, `status`, `recentActivity`, and `priority`; include `summary` for contributor context. |
| Coder | `.vscode/launch.json` | Create strict JSON for **Run Project Pulse Dashboard**, serve from `${workspaceFolder}/app`, run `python3 -m http.server 5500`, and open `index.html`. |
| Orchestrator | Integrated review | Coordinate the specialists, enforce file ownership, resolve interface decisions, and verify the integrated result. |

## Agent responsibilities

### Planner

Research the repository, brief, documentation, dependencies, edge cases, risks, and validation needs. Produce the ordered implementation plan and shared contracts without writing application code.

### Designer

Create a polished Project Pulse dashboard experience rather than a bare HTML page. Use visible project cards, readable spacing, rounded corners, shadows, clear status badges, priority treatment, responsive behavior, accessible contrast, keyboard focus states, and deterministic `.dashboard` and `.project-card` hooks. Stay within `app/styles.css`.

### Coder

Implement the static dashboard within the assigned files. Keep the data deterministic and valid, use semantic and accessible markup, render safe text from the project data, provide loading/empty/error states, and create the strict launch configuration with the correct working directory and URL. Validate the implementation before reporting completion.

### Orchestrator

Coordinate the Planner, Designer, and Coder in phases with explicit file ownership. Review consistency between the HTML, CSS selectors, JSON schema, and launch configuration, then perform the integrated validation and report the handoff.

## Ordered implementation steps

1. **Confirm the shared contract.** Agree that the JSON shape is `{ "projects": [...] }`, establish the required fields and CSS hooks, and confirm that `index.html` is the integration surface.
2. **Design the presentation.** The Designer creates `app/styles.css` with the responsive dashboard layout, project-card styling, accessible states, and clear status and priority affordances.
3. **Prepare data and launch support.** The Coder creates `app/project-data.json` and drafts `.vscode/launch.json` with the required launch name, `cwd`, server command, and `/index.html` target.
4. **Implement the dashboard.** After the shared contract is settled, the Coder creates `app/index.html`, references the stylesheet and data, and renders one visible card per project with all required fields and a summary.
5. **Integrate and review.** The Orchestrator checks selectors, field names, paths, accessibility, responsive behavior, error handling, JSON syntax, and absence of unrelated changes.

## Dependencies

- The shared contract must define CSS hooks and JSON field names before final HTML integration.
- Designer and Coder may work independently on `app/styles.css`, `app/project-data.json`, and the initial `.vscode/launch.json`.
- `app/index.html` depends on the agreed CSS hooks and finalized JSON schema.
- Browser and launch validation depend on all four implementation files existing.
- The final handoff depends on successful integrated review and validation.

## Parallel work decisions

### Can run in parallel

- Designer creates `app/styles.css`.
- Coder creates `app/project-data.json`.
- Coder drafts `.vscode/launch.json`.
- Planner documents the implementation contract while repository research is complete.

These tasks have separate file scopes once the shared contract is established.

### Must remain sequential

- Shared contract before implementation.
- Final `app/index.html` integration after the CSS hooks and JSON schema are agreed.
- Integrated validation after all app files and launch configuration are present.
- Final Orchestrator handoff after validation.

Designer and Coder must not edit the same file in the same phase.

## Validation expectations

### Static validation

- Parse `app/project-data.json` and `.vscode/launch.json` with `python3 -m json.tool`.
- Confirm the JSON has a top-level `projects` array and required fields on every project.
- Confirm `app/index.html` contains `Project Pulse`, references `styles.css` and `project-data.json`, uses `.dashboard` and `project-card`, and renders `name`, `owner`, `status`, `recentActivity`, `priority`, and `summary`.
- Confirm `app/styles.css` contains `.dashboard`, `.project-card`, `border-radius`, and `box-shadow`.
- Run the repository's existing `bash scripts/validate-exercise.sh`.

### Runtime validation

- Start **Run Project Pulse Dashboard** from VS Code.
- Confirm the server runs from `app/` and the browser opens `http://localhost:5500/index.html`.
- Confirm the first view shows the Project Pulse UI, not a directory listing.
- Confirm multiple cards display all required project fields and summaries.
- Test narrow and wide viewports, keyboard focus, readable contrast, long text wrapping, empty data, and malformed or unavailable data states.
- Stop the preview server after the smoke test.

## Edge cases, risks, and open questions

- Use the HTTP server for validation because `file://` may block JSON loading.
- Missing or malformed data must show an explicit error; an empty array must show a useful empty state.
- Unknown status or priority values should use a readable neutral treatment.
- Long names, activity text, and summaries must wrap without horizontal scrolling.
- Port `5500` may be occupied; surface the conflict rather than silently changing the configured behavior.
- The brief does not require `summary` as a mandatory JSON field, but it should be included on every project to satisfy the contributor-friendly summary requirement.
- No formal brand palette or target browser is specified; use a restrained accessible palette and broadly supported web features.
- Live APIs, authentication, editing, filtering, sorting, and other framework dependencies are out of scope.
