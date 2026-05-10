# Feature Spec: In-App Notifications

## Goal

Allow users to receive real-time notifications inside the app when a teammate assigns them a task, mentions them in a comment, or completes a task they are watching.

## Background

Users currently miss important project updates unless they check their email. Adding in-app notifications will reduce context switching and keep users engaged within the product. This is the most-requested feature in our Q1 user survey.

## User Stories

- As a project member, I want to see a badge on the notification bell when I have unread notifications so that I know to check them.
- As a project member, I want to click a notification and be taken directly to the relevant task or comment so that I can respond quickly.
- As a user, I want to mark all notifications as read in one click so that I can clear the badge without opening each one.

## Scope

### In Scope

- Notification bell icon in the header with an unread count badge
- Dropdown panel listing the 20 most recent notifications
- Notification types: task assigned, mentioned in comment, watched task completed
- Mark individual notifications as read on click
- Mark all as read button
- Persist notification read state per user in the database

### Out of Scope

- Push notifications (browser or mobile)
- Email digests or email notification preferences
- Notification filtering or categories
- Real-time delivery via WebSockets (polling is acceptable for v1)

## Technical Notes

- New `notifications` table: `id`, `user_id`, `type`, `payload` (JSONB), `read_at`, `created_at`
- New API endpoints: `GET /api/notifications`, `PATCH /api/notifications/:id/read`, `PATCH /api/notifications/read-all`
- Notification records created server-side via a service function called from existing task and comment mutations
- Poll interval: 30 seconds using `setInterval` in a React context provider
- No third-party services required for v1

## Acceptance Criteria

| Criterion | Status | Notes |
|-----------|--------|-------|
| Bell icon shows a badge with the correct unread count | To do | |
| Badge disappears when all notifications are marked as read | To do | |
| Clicking a notification marks it as read and navigates to the correct page | To do | |
| "Mark all as read" clears all badges and updates all records | To do | |
| Notifications panel shows the 20 most recent notifications, newest first | To do | |
| Notification panel is keyboard navigable and accessible | To do | |
| Polling does not cause visible UI flicker | To do | |

## Open Questions

- Should notifications older than 90 days be automatically deleted, or archived?
- Do we need a separate notifications settings page for v1, or can that come later?
