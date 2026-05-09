# PR Review Checklist

**PR:** Add user notification bell and dropdown — #214
**Author:** @sarah
**Reviewer:** @james
**Branch:** `feature/notifications` → `main`

Review the diff for:

- [x] Correctness bugs
- [x] Edge cases not handled
- [x] Security issues
- [x] Unnecessary complexity
- [x] Missing tests
- [ ] Unclear naming
- [x] Broken existing behaviour
- [ ] Accessibility problems
- [x] Performance regressions

## Issues Found

---

### Issue 1

- **File:** `src/api/notifications.ts`, line 42
- **Problem:** The `GET /api/notifications` endpoint does not scope results to the authenticated user — it queries all notifications with no `WHERE user_id = ?` filter.
- **Why it matters:** Any authenticated user can read another user's notifications.
- **Fix:** Add `where: { userId: session.user.id }` to the Prisma query.

---

### Issue 2

- **File:** `src/components/NotificationDropdown.tsx`, line 18
- **Problem:** The polling interval is created with `setInterval` but never cleared. If the component unmounts and remounts (e.g. during navigation), multiple intervals stack up.
- **Why it matters:** Causes duplicate API calls and a memory leak over time.
- **Fix:** Return a cleanup function from `useEffect` that calls `clearInterval`.

---

### Issue 3

- **File:** `src/components/NotificationDropdown.tsx`, line 67
- **Problem:** The dropdown is not keyboard accessible — it can only be opened by clicking the bell icon. There is no `onKeyDown` handler and no `role="button"` or `<button>` wrapper.
- **Why it matters:** Fails WCAG 2.1 SC 2.1.1 (Keyboard).
- **Fix:** Wrap the bell icon in a `<button>` element; the dropdown trigger behaviour then works for free.

## Issue Format

For each issue found, include:

1. File and line number
2. Description of the problem
3. Why it matters
4. Suggested fix
