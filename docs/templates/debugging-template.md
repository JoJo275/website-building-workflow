# Debugging Template

## Problem

The contact form submits successfully (200 response from the API) but the user sees an error toast and the form fields are not cleared.

## Expected Behaviour

After a successful form submission, the error toast should not appear, and all form fields should reset to their empty state.

## Actual Behaviour

The API returns `200 OK` with `{ success: true }`, but the UI displays "Something went wrong. Please try again." and the form fields retain their values.

## Steps to Reproduce

1. Navigate to `/contact`
2. Fill in all required fields with valid data
3. Click **Send Message**
4. Observe the toast notification and form state

## Environment

- Browser / runtime version: Chrome 124, Node 20.12
- OS: macOS 14.4
- Relevant config: `NEXT_PUBLIC_API_URL=https://api.example.com`

## Hypotheses

List possible causes before investigating:

1. The response handler is checking `res.ok` but the API returns a non-2xx status code despite the body saying `success: true`
2. The error state is set before the async response is awaited, causing a race condition
3. The form reset is called before the submit handler resolves, so it appears to do nothing

## Investigation Log

| Hypothesis | Test | Result |
|---|---|---|
| Non-2xx status code | Checked Network tab in DevTools | Status is `200` — ruled out |
| Race condition on error state | Added `console.log` before and after `setError` call | Error is set synchronously before `await res.json()` resolves — confirmed |
| Form reset timing | Checked order of `reset()` and `await` calls | Not the cause |

## Root Cause

`setError(true)` was called unconditionally at the start of the submit handler before the response was awaited, rather than inside the error branch. Because React batches state updates, the error toast rendered after the successful response.

## Fix Applied

Moved `setError(false)` to the top of the handler to clear any previous error, and moved `setError(true)` inside the `catch` block and the failure branch only.

## Prevention

- Add an integration test that asserts the error toast is **not** shown on a successful submission.
- Lint rule or code review note: error state should only be set inside error branches, never as a default at the top of an async handler.
