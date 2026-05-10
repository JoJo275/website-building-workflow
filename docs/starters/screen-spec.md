# Screen Spec

A screen spec is a written description of a single page or major view. Write one per major screen before building it. It gives you a clear reference while coding and gives Copilot the context it needs to generate useful output — layout, components, data, states, and constraints — rather than guessing from a vague prompt.

## Template

```markdown
## Screen: [Name]

**Route:** /path
**Auth:** Required / Public

### Purpose

One sentence. What does this screen do for the user?

### Primary Actions

- Action 1
- Action 2

### Layout

- **Region name** — what it contains

### Components

- `ComponentName`

### Data Needed

- `field_name` — description

### States

- **Loading** —
- **Empty** —
- **Loaded** —
- **Error** —
- **Filtered** — (if applicable)
- **Mobile** —

### Connected Screens

- Links to: /path
- Opened from: /path

### Acceptance Criteria

| Criterion | Status | Notes |
|-----------|--------|-------|
| | To do | |

### Implementation Constraints

-
```

---

## Example: Project Board (Kanban View)

**Route:** /projects/:id/board
**Auth:** Required

### Purpose

Displays all tasks for a project as cards grouped into status columns (To do, In progress, In review, Done). The primary workspace for a team to manage day-to-day work on a project.

### Primary Actions

- Add a new task to any column
- Drag a task card to a different column to update its status
- Open a task card to view its detail panel
- Filter tasks by assignee or label
- Switch to list or timeline view

### Layout

- **Header** — project name, view switcher (Board / List / Timeline), filter controls, invite member button
- **Sidebar** — global app nav (projects list, inbox, settings)
- **Main content** — horizontal scrolling column layout; each column has a header with status name and task count, a list of task cards, and an "Add task" button at the bottom
- **Right panel** — task detail drawer; slides in when a card is clicked without leaving the board

### Components

- `AppHeader`
- `AppSidebar`
- `BoardColumn`
- `TaskCard`
- `TaskDetailDrawer`
- `FilterBar`
- `UserAvatar`
- `EmptyState`

### Data Needed

- `project.id`, `project.name`, `project.members`
- `tasks[]` — `id`, `title`, `status`, `assignee`, `dueDate`, `labels`, `commentCount`
- Current user session (to pre-select assignee filter)

### States

- **Loading** — skeleton placeholders for columns and cards while data fetches
- **Empty** — no tasks exist yet; each column shows an "Add your first task" prompt
- **Loaded** — normal board with task cards
- **Error** — failed to load tasks; show an inline error with a retry button
- **Filtered** — some columns may show zero cards; retain column headers and show a "No matching tasks" message
- **Mobile** — columns stack vertically; only the active column is visible with swipe navigation

### Acceptance Criteria

| Criterion | Status | Notes |
|-----------|--------|-------|
| All task cards render in the correct column based on their status | To do | |
| Dragging a card to a new column updates the task status via the API immediately | To do | |
| Filtering by assignee hides non-matching cards without removing columns | To do | |
| Clicking a card opens the detail drawer without navigating away | To do | |
| The board is usable on mobile with column swipe navigation | To do | |
| Empty state is shown per-column when no tasks match the current filter | To do | |

### Implementation Constraints

- Use the existing `useDragAndDrop` hook — do not introduce a new DnD library.
- Task status updates must be optimistic with a rollback on API error.
- The board must handle up to 500 tasks without layout or scroll performance issues.

### Connected Screens

- Links to: /projects/:id/tasks/:taskId (task detail)
- Links to: /projects/:id/list, /projects/:id/timeline (view switcher)
- Opened from: /projects (project list)

---

## Example: Dashboard

**Route:** /dashboard
**Auth:** Required

### Purpose

Give users a quick overview of feedback health and what needs attention.

### Primary Actions

- Open new feedback
- Filter feedback
- View urgent / unresolved items
- Go to analytics
- Go to settings

### Layout

- **Left sidebar** — global app nav
- **Top header** — page title, primary actions
- **Main dashboard grid** — metric cards
- **Recent feedback section** — latest incoming items
- **Optional insight panel** — trends or highlights

### Components

- `AppShell`
- `MetricCard`
- `FeedbackList`
- `FeedbackCard`
- `TagPill`
- `StatusBadge`

### Data Needed

- `total_feedback_count`
- `unresolved_count`
- `urgent_count`
- `average_sentiment`
- `recent_feedback_items[]`

### States

- **Loading** — skeleton placeholders while data fetches
- **Empty** — no feedback yet; prompt to connect a source or add feedback
- **Loaded** — normal dashboard with metrics and recent items
- **Error** — failed to load; show an inline error with a retry button
- **Mobile** — single column layout; sidebar collapses to a bottom nav or drawer

### Acceptance Criteria

| Criterion | Status | Notes |
|-----------|--------|-------|
| Metric cards display correct counts from the API | To do | |
| Recent feedback list shows the latest items in chronological order | To do | |
| Empty state renders when no feedback items exist | To do | |
| Error state renders with a retry action when the API fails | To do | |
| Layout is usable on mobile at 375px | To do | |

### Implementation Constraints

- Use existing API routes if available. Do not create backend endpoints unless requested.
- Use Tailwind and design tokens. Avoid inline styles unless necessary.

### Connected Screens

- Links to: /feedback/:id (feedback detail)
- Links to: /analytics, /settings
- Opened from: / (root redirect after login)
