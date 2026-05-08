# Copilot Implementation Checklist

## Before Asking AI to Edit Code

- [ ] Task goal is clearly written in one or two sentences
- [ ] Relevant files are listed
- [ ] Constraints are listed (what not to change, what not to add)
- [ ] Acceptance criteria are written
- [ ] Design reference is linked if applicable
- [ ] Existing APIs and data models are described
- [ ] Non-goals are listed

## During Implementation

- [ ] Ask for a plan first — review it before code is written
- [ ] Keep changes small and focused on one task
- [ ] Avoid unrelated refactors in the same diff
- [ ] Ask AI to list files it intends to edit before making changes
- [ ] Run tests, lint, and typecheck after each change

## After Implementation

- [ ] Review the diff manually line by line
- [ ] Ask AI for a critical review of the output
- [ ] Confirm all acceptance criteria are met
- [ ] Commit with a clear, descriptive message
