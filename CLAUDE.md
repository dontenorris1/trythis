# CLAUDE.md

This file provides guidance for AI assistants working in this repository.

## Repository Overview

**trythis** is a minimal, self-contained single-page web application for mobile task management. The entire application lives in a single HTML file with no external dependencies, build tools, or backend.

## File Structure

```
/
├── index.html   # Complete SPA — HTML, CSS, and JS all in one file
├── README.md    # Placeholder readme
└── CLAUDE.md    # This file
```

## Application: index.html

The application is a mobile-first todo/task manager titled "Ultimate Mobile Tasks."

### Architecture

- **No dependencies** — pure vanilla HTML, CSS, and JavaScript
- **No build step** — open the file directly in a browser
- **Persistence** — tasks are stored in the browser's `localStorage`
- **Layout constraints** — max-width: 450px, designed for mobile screens

### Key JavaScript Functions

| Function | Purpose |
|---|---|
| `addTask()` | Creates a task object `{id, text, date, completed}` and saves it |
| `toggleComplete(id)` | Flips the `completed` flag for a task |
| `removeTask(id)` | Deletes a task by ID |
| `clearCompleted()` | Removes all completed tasks (with confirmation prompt) |
| `renderTasks()` | Re-renders the task list, applying search filter and sort order |
| `getStoredTasks()` | Reads the task array from `localStorage` |
| `saveTasks(tasks)` | Writes the task array to `localStorage` |

### Task Data Shape

```js
{
  id: Date.now(),       // numeric timestamp used as unique ID
  text: "Task name",    // string
  date: "2026-03-06T10:00",  // datetime-local string, optional
  completed: false      // boolean
}
```

### Render / Sort Order

`renderTasks()` displays tasks in this order:
1. Incomplete tasks first
2. Tasks with due dates sorted ascending by date
3. Completed tasks last (strikethrough + reduced opacity)

### CSS Variables

```css
--danger: #dc3545;   /* delete/destructive actions */
--gray:   #6c757d;   /* secondary/muted text */
```

## Development Workflow

### Running the App

No server required — open `index.html` directly in any modern browser:

```bash
# macOS
open index.html

# Linux
xdg-open index.html

# Or simply drag the file into a browser window
```

### Making Changes

1. Edit `index.html` directly — CSS and JS are embedded in `<style>` and `<script>` tags.
2. Reload the browser to see changes.
3. localStorage state persists across reloads; use DevTools → Application → localStorage to inspect or clear it.

### No Tests, No Linter, No CI

This repository has no automated tests, no linting configuration, and no CI/CD pipelines. There are no `npm test`, `make`, or other build commands to run.

## Git Conventions

- **Main branch:** `main` (and legacy `master`)
- **Feature branches:** prefix with `claude/` for AI-assisted work (e.g. `claude/add-claude-documentation-QbKif`)
- Commit messages use imperative style: `"Update index.html"`, `"Create README.md"`

### Push Command

```bash
git push -u origin <branch-name>
```

Branches must start with `claude/` for AI-assisted pushes.

## Key Conventions for AI Assistants

- **All changes go into `index.html`** — do not split CSS or JS into separate files unless explicitly asked.
- **No dependencies** — do not introduce npm, CDN links, or external libraries without explicit approval.
- **No build tooling** — do not add webpack, vite, parcel, or similar tools unless explicitly asked.
- **Mobile-first** — keep max-width at 450px and test layout at mobile viewport sizes.
- **localStorage schema** — the key is `"tasks"` and the value is a JSON-serialised array of task objects. Do not change this schema without migrating existing data.
- **IDs are timestamps** — `Date.now()` is used as the task ID; do not switch to UUIDs or other schemes without updating all ID references.
- **Confirmation before destructive bulk ops** — `clearCompleted()` uses `window.confirm()`; keep this pattern for any new bulk-delete features.
