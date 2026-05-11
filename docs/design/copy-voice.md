# Copy & Voice

How the product sounds in UI, error messages, and email. Establishing voice rules early prevents copy decisions being made ad hoc at the component level.

The examples throughout this page come from a real product. The principles are general — the specific strings are a worked example to copy, adapt, or replace.

---

## Voice

**Calm, direct, and operational** — like a good incident channel, not a chirpy SaaS marketing page.

The key trade-off: **clarity over cleverness.** If a sentence makes the user think for an extra beat, rewrite it.

| Do | Don't |
|---|---|
| "We couldn't sign you in. Check your password." | "Whoops! Something went wrong. 😬" |
| "Demo workspaces are read-only." | "Sorry, you can't do that here." |
| "Note edits close after 15 minutes." | "You can no longer edit this note." |
| "Sign in" | "Login" |
| "Log out" | "Sign out" / "Logout" |
| "Workspace" | "Team" / "Org" / "Account" |
| "Owner" | "Admin" / "Manager" |

---

## Mechanical rules

- **Sentence case** for buttons, labels, and headings — *"Create workspace"*, not *"Create Workspace"*. Proper nouns keep their case.
- **Oxford comma** in lists.
- **Em dash** ( `—` ) for asides; no spaced hyphens.
- **No exclamation marks** in product copy.
- **No emoji** in product copy. Markdown notes and internal issues are fine.
- **Numbers:** spell out one through nine; numerals for 10+. Always numerals for time (`5 minutes`), money (`$5`), and versions (`v2.0`).
- **Time:** relative ("3 minutes ago") in lists; absolute UTC ISO 8601 in tooltips and detail pages. Never local time without an explicit "(your time)" suffix.
- **Feature names:** lowercase unless at the start of a sentence. *"Use roadmap to plan ahead."*

---

## Action verbs

Match the button label to the action — not the page, not the metaphor. Define these once and reference them consistently.

Destructive confirmations always restate the noun: *"Yes, delete it"* — not *"Yes, confirm"*.

!!! example "Example: action verbs for a multi-tenant SaaS"

    | Action | Button text |
    |---|---|
    | Create a feedback item | *Add feedback* |
    | Create a workspace | *Create workspace* |
    | Save form changes | *Save changes* |
    | Discard form changes | *Cancel* |
    | Permanently remove | *Delete* |
    | Soft-archive | *Archive* |
    | Send an invitation email | *Send invite* |
    | Sign in | *Sign in* |
    | Sign out | *Log out* |
    | Confirm a destructive action | *Yes, delete it* |
    | Acknowledge a non-destructive notice | *Got it* |

---

## Error messages

Pattern: **state what happened, then what to do.** No blame, no `Oops!`.

Messages exceed one sentence only when the user genuinely needs more context (e.g., a lockout that mentions the wait time).

!!! example "Example: error messages for an auth + workspace product"

    | Code | Message |
    |---|---|
    | `auth_required` | *Please sign in to continue.* |
    | `invalid_credentials` | *We couldn't sign you in. Check your email and password.* |
    | `email_not_verified` | *Verify your email before signing in. We sent a link — check your inbox.* |
    | `account_locked` | *Too many sign-in attempts. Try again in 15 minutes.* |
    | `password_too_weak` | *Use at least 12 characters with a mix of letters, numbers, and symbols.* |
    | `workspace_not_found` | *We can't find that workspace.* |
    | `workspace_slug_taken` | *That URL is already taken. Try another.* |
    | `role_insufficient` | *Only workspace owners can do that.* |
    | `demo_read_only` | *Demo workspaces are read-only. Sign up to make changes.* |
    | `note_edit_expired` | *Note edits close after 15 minutes.* |
    | `rate_limited` | *You're going a bit fast. Try again in a moment.* |
    | `internal_error` | *Something went wrong on our end. Please try again.* |

---

## Empty states

Every list page needs an empty state with three slots: **heading, body, primary action.** Tone is encouraging without being chirpy.

!!! example "Example: empty states for a triage product"

    | Page | Heading | Body | Primary action |
    |---|---|---|---|
    | Inbox | *Inbox zero.* | *Nothing waiting. New feedback shows up here.* | *Add feedback* |
    | All items | *No feedback yet.* | *Start collecting signals from your users.* | *Add feedback* |
    | Roadmap | *Roadmap is empty.* | *Mark feedback as planned to put it on the roadmap.* | *Open inbox* |
    | Changelog | *Nothing shipped yet.* | *When you mark feedback as shipped, it'll show up here.* | *Open feedback* |
    | Tags | *No tags yet.* | *Tags help group related feedback. Make a few to get started.* | *New tag* |
    | Insights | *Not enough data yet.* | *Insights need at least 20 feedback items.* | *Open inbox* |

---

## Microcopy patterns

**Confirmation toasts** — short, past-tense:

```text
Workspace created.
Note saved.
Invite sent.
```

**Loading states** — present-tense, three words or fewer:

```text
Loading…
Saving…
Sending invite…
```

**Destructive confirmations** — restate the noun and the verb, with a second line:

```text
Delete this feedback?
This can't be undone.
```

**Form help text** — one short sentence under the field. No validation hints in placeholders.

---

## Brand copy

Voice rules and copy examples from a worked example product. The principles (calm acknowledgement, verbs of clarity, no hype) apply to any product — the specific strings and domain language are yours to define.

### Voice rules (copy review checklist)

When writing any UI string:

- Prefer verbs of clarity: *capture, triage, prioritize, mark, merge, notify*.
- Prefer calm acknowledgement: *New item received. Status updated. Marked as planned.*
- Avoid hype: no *Awesome!!!*, no *Super-powered*, no *magic*.
- Avoid generic-tool wording: no *Submit your response*, no *Thanks for your input*.
- Empty states are factual. *No items match these filters.*
- Errors are direct. *Email already in use. Token expired.* No *Oops!*

!!! example

    **Good**

    ```text
    New signal received.
    Feedback merged.
    Marked as planned.
    Status updated.
    User notified.
    No matching feedback found.
    This item may be a duplicate.
    ```

    **Bad**

    ```text
    Awesome!!!
    Your amazing feedback has been processed!
    Super-powered AI magic!
    ```
