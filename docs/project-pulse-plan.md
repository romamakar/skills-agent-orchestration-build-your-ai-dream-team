# Project Pulse Dashboard Implementation Plan

## Summary

Build a small, static Project Pulse dashboard that helps contributors scan project ownership, status, recent activity, and priority or risk. The repository currently has an empty `app/` directory, `.vscode/tasks.json` but no launch configuration, and custom Planner, Orchestrator, Designer, and Coder agent definitions. The project brief defines the required project fields but does not provide real project data or detailed conventions for summaries, statuses, or priorities; use clearly identified sample placeholders until those are confirmed.

## File ownership

| File | Owner | Responsibility |
| --- | --- | --- |
| `app/index.html` | Coder | Create the accessible page structure, link `styles.css`, load `project-data.json`, and render project cards with project details. Use the exact title “Project Pulse” and stable `.dashboard` / `.project-card` hooks that match the stylesheet. |
| `app/styles.css` | Designer | Own all styling and accessibility-related visual treatment: polished responsive card layout, typography and spacing, readable status badges, distinct priority or risk cues, contrast, and visible focus states. Include `.dashboard` and `.project-card` selectors. |
| `app/project-data.json` | Coder | Create valid JSON with a top-level `projects` array. Each sample project has `name`, `owner`, `status`, `recentActivity`, and `priority`. Label values as illustrative placeholders rather than implying they are Mona’s real projects. |
| `.vscode/launch.json` | Coder | Add strict JSON for a launch configuration named `Run Project Pulse Dashboard`. Set `cwd` to `${workspaceFolder}/app`, serve that directory with `python3 -m http.server 5500`, and open `index.html` at `http://localhost:%s/index.html` rather than the directory root. |

## Responsibilities

- **Designer:** Make design and accessibility decisions and implement only `app/styles.css`. Coordinate required class hooks and badge/priority treatment with the Orchestrator; do not edit markup or data.
- **Coder:** Implement only `app/index.html`, `app/project-data.json`, and `.vscode/launch.json`. Keep the page semantic and keyboard-friendly, render values from the data file, and ensure the launch config serves the app and opens its page.
- **Orchestrator:** Coordinate phases and handoffs, establish the markup/style contract, preserve the non-overlapping ownership above, integrate the files, run the validation checks, and report any unresolved data assumptions.

## Ordered phases and dependencies

1. **Confirm the interface and acceptance criteria — Orchestrator.** Use the brief’s required project fields and establish the shared `.dashboard` and `.project-card` hooks plus any badge and priority hooks before implementation. No deliverable files are changed in this coordination step.
2. **Create independent foundations — Designer and Coder, parallel.** Designer creates `app/styles.css`; Coder creates `app/project-data.json`. Both depend on phase 1’s agreed interface, but neither depends on the other’s implementation.
3. **Implement page and launch support — Coder.** Create `app/index.html` against the data fields and CSS hooks from phase 1. Create `.vscode/launch.json` with the specified working directory, server command, and page URL. The HTML depends on the agreed hooks and data contract; the launch configuration depends on the app path and serve/open requirements, not on styling details.
4. **Integrate and validate — Orchestrator with Designer and Coder as needed.** Check the complete dashboard and launch flow. Route fixes to the owner of the affected file; keep ownership non-overlapping.

## Parallel and sequential work decisions

- **Parallel:** After the interface contract is agreed, Designer’s stylesheet and Coder’s sample JSON can be built at the same time because they have distinct owners and no implementation dependency.
- **Sequential:** Agree on hooks before either side relies on them; finish the stylesheet and data contract before Coder completes the page integration. Validate only after all four files exist.
- **Launch configuration:** It is conceptually independent of the stylesheet and data, but remains Coder-owned and can be completed alongside Coder’s page work. Its preview must not be considered verified until `index.html` is present.
- **No shared-file editing:** Designer never changes HTML; Coder never changes CSS. Orchestrator coordinates but does not edit these deliverables.

## Implementation and edge cases

- The page should show multiple visible project cards and make project name, owner, status, recent activity, and priority easy to scan. Use distinct, readable status badges and priority/risk emphasis without relying on color alone.
- Ensure responsive layout at narrow and wide viewport sizes, sufficient color contrast, semantic headings/regions, and keyboard-visible focus.
- If `index.html` loads JSON with browser `fetch`, a `file://` preview will generally block that request. Use the HTTP launch configuration rather than asking learners to open the file directly. Confirm the served URL ends in `/index.html`, not `/`.
- Keep `launch.json` strict JSON (no comments), use the exact `${workspaceFolder}/app` working directory, and ensure the configured server serves that directory.
- Keep sample records syntactically valid and consistent with the agreed fields. Do not present invented data as actual team data.

## Validation expectations

- Confirm all assigned files exist and the page visibly presents the Project Pulse dashboard, not a server directory listing.
- Check that `app/index.html` has the exact “Project Pulse” title, references `styles.css` and `project-data.json`, and renders cards with `.project-card` and each required project field.
- Confirm `app/styles.css` defines `.dashboard` and `.project-card`, with responsive layout, rounded cards (`border-radius`), shadows (`box-shadow`), readable badges and priority treatment, and accessible contrast/focus styling.
- Parse `app/project-data.json` and `.vscode/launch.json` as JSON; verify the data has a top-level `projects` array and each record has `name`, `owner`, `status`, `recentActivity`, and `priority`.
- Inspect the launch configuration for the name `Run Project Pulse Dashboard`, strict JSON, `cwd` `${workspaceFolder}/app`, the HTTP server command, and a browser target ending in `/index.html`.
- Run the launch configuration and confirm it serves the dashboard over HTTP and opens the rendered UI. Stop the preview server after the check.

## Open questions

- What are the real project names, owners, statuses, recent activity, priorities, and contributor-friendly summaries? No actual project data has been supplied, so use conspicuously illustrative sample placeholders.
- Should each project include a separate `summary` property? The brief asks for a short contributor-friendly summary but its required data fields do not specify one.
- What controlled vocabulary and visual mapping should be used for `status` and `priority`/risk? Use clear sample values for now and confirm with the project owner before treating them as canonical.
