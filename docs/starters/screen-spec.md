# Screen Spec: Project Board (Kanban View)

## Purpose

Displays all tasks for a project as cards grouped into status columns (To do, In progress, In review, Done). The primary workspace for a team to manage day-to-day work on a project.

## Primary Actions

- Add a new task to any column
- Drag a task card to a different column to update its status
- Open a task card to view its detail panel
- Filter tasks by assignee or label
- Switch to list or timeline view

## Layout

- **Header** — project name, view switcher (Board / List / Timeline), filter controls, invite member button
- **Sidebar** — global app nav (projects list, inbox, settings)
- **Main content** — horizontal scrolling column layout; each column has a header with status name and task count, a list of task cards, and an "Add task" button at the bottom
- **Right panel** — task detail drawer; slides in when a card is clicked without leaving the board

## Components

- `AppHeader`
- `AppSidebar`
- `BoardColumn`
- `TaskCard`
- `TaskDetailDrawer`
- `FilterBar`
- `UserAvatar`
- `EmptyState`

## Data Needed

- `project.id`, `project.name`, `project.members`
- `tasks[]` — `id`, `title`, `status`, `assignee`, `dueDate`, `labels`, `commentCount`
- Current user session (to pre-select assignee filter)

## States

- **Loading** — skeleton placeholders for columns and cards while data fetches
- **Empty** — no tasks exist yet; each column shows an "Add your first task" prompt
- **Loaded** — normal board with task cards
- **Error** — failed to load tasks; show an inline error with a retry button
- **Filtered** — some columns may show zero cards; retain column headers and show a "No matching tasks" message
- **Mobile** — columns stack vertically; only the active column is visible with swipe navigation

## Design Reference

[Figma — Project Board v2](https://figma.com/file/example/project-board-v2)

## Acceptance Criteria

| Criterion | Status | Notes |
|-----------|--------|-------|
| All task cards render in the correct column based on their status | To do | |
| Dragging a card to a new column updates the task status via the API immediately | To do | |
| Filtering by assignee hides non-matching cards without removing columns | To do | |
| Clicking a card opens the detail drawer without navigating away | To do | |
| The board is usable on mobile with column swipe navigation | To do | |
| Empty state is shown per-column when no tasks match the current filter | To do | |

## Implementation Constraints

- Use the existing `useDragAndDrop` hook — do not introduce a new DnD library.
- Task status updates must be optimistic with a rollback on API error.
- The board must handle up to 500 tasks without layout or scroll performance issues.
