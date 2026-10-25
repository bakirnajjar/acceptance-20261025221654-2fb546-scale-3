# Password reset requirements analysis

## Evidence

- **Story:** "As a customer I want to reset my password. Apply the curated recovery standard." Source: `user_story` / `user_story` / `characters 0-8000`.
- **Curated account recovery standard (ACC-STD-01–03):** Source: `knowledge` / `59efeb19-83f2-4ec6-bfd3-b4aeb7142930` / `v1, chunk 0`.
- No attachments or approved prior-stage outputs were supplied.

## Requirements

### REQ-001 — Complete a password reset

A customer can complete an authorized password reset that changes their account password to a newly selected password.

**Acceptance:** Given a customer is able to complete an authorized password reset for their account, when they complete the reset with a new password, then the account password is changed to the new password.

**Source:** Story.

### REQ-002 — Show the reset entry point

The sign-in page displays a "Forgot password?" link.

**Acceptance:** Given the sign-in page is displayed, when a customer views it, then a "Forgot password?" link is available.

**Sources:** Story; ACC-STD-01.

### REQ-003 — Start the reset request

Activating the "Forgot password?" link starts the password reset request flow.

**Acceptance:** Given the sign-in page shows the "Forgot password?" link, when a customer activates it, then the customer can begin a password reset request.

**Sources:** Story; ACC-STD-01.

### REQ-004 — Make request responses account-existence neutral

The response to a password reset request is identical whether the requested account exists or does not exist.

**Acceptance:** Given equivalent password reset requests differing only in whether the account exists, when each request is submitted under the same applicable conditions, then their customer-visible responses are identical.

**Source:** ACC-STD-01.

### REQ-005 — Limit reset requests

Password reset requests are limited to five per account per hour.

**Acceptance:** Given five password reset requests for an account have been permitted in a one-hour period, when another request for that account is submitted within that period, then it is not permitted as an additional reset request and the account-existence-neutral response requirement still applies.

**Source:** ACC-STD-01.

### REQ-006 — Use a reset link only once

Each reset link can complete no more than one password reset.

**Acceptance:** Given a reset link has been used to complete a reset, when it is used again, then it cannot complete another reset.

**Source:** ACC-STD-02.

### REQ-007 — Expire reset links

Reset links expire 30 minutes after issuance.

**Acceptance:** Given a reset link was issued 30 minutes ago, when it is used to attempt a reset, then it cannot complete that reset because it has expired.

**Source:** ACC-STD-02.

### REQ-008 — End every active session after reset

Completing a password reset signs the account out of every active session.

**Acceptance:** Given an account has active sessions, when its password reset completes, then none of those sessions remains signed in to that account.

**Source:** ACC-STD-02.

### REQ-009 — Notify the account owner

The account owner is notified after every successful password reset.

**Acceptance:** Given an account owner has completed a successful password reset, when the reset completes, then a notification of that reset is sent to that account owner; each subsequent successful reset also produces its own notification.

**Source:** ACC-STD-03.

## Assumptions

- acceptance-20261025221654-2fb546-skill-sentinel: the acceptance requirements skill produced this output.
- The supplied story has no end marker, and there are no supplied attachments or attachment markers.
- A valid authorized reset is assumed for testing the customer's ability to change their password; the method of verifying account ownership is unspecified.
- An issued reset link can be provided to a test without assuming a delivery channel.
- The five-per-account-per-hour quota is tested for an existing account; handling of nonexistent accounts in internal rate-limit accounting is unspecified and does not relax identical customer-visible responses.
- No exact reset-request response wording is assumed; equivalent requests for existing and nonexistent accounts must yield identical customer-visible responses.
- Owner notification is tested without assuming a notification channel.

## Open questions (non-blocking)

| Question | Working assumption |
| --- | --- |
| How is account ownership verified before permitting a password reset? | Assume a valid authorized reset for acceptance testing without specifying the verification method. |
| Through which channel is a reset link delivered? | Use an issued link in acceptance testing without choosing a delivery channel. |
| How are reset requests for nonexistent accounts treated in internal rate-limit accounting? | Test the per-account quota for existing accounts while preserving identical customer-visible responses. |
| What wording should the password-reset request response use? | Do not prescribe wording; responses to equivalent requests must be identical whether or not an account exists. |
| Through which channel is the account owner notified after a successful password reset? | Verify owner notification after each successful reset without choosing a delivery channel. |
