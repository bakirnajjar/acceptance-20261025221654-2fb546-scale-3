# Password reset requirements map

## Evidence and scope

- Full pinned story (no end marker): “As a customer I want to reset my password. Apply the curated recovery standard.” `{"source_type":"user_story","source_id":"user_story","locator":"characters 0-8000"}`
- Applicable run-matched account recovery standard, ACC-STD-01–03: `{"source_type":"knowledge","source_id":"59efeb19-83f2-4ec6-bfd3-b4aeb7142930","locator":"v1, chunk 0"}`
- No attachments or approved prior outputs were supplied. A substantively identical result from another library adds no policy; the run-matched source above is used below.

## Atomic requirements and acceptance criteria

### REQ-001 — Complete a password reset

**Statement:** A customer can successfully reset the password for their account, replacing its existing password with a newly selected password.

**Acceptance criteria:** Given a customer is able to complete an authorized password reset for their account, when they complete the reset with a new password, then the account password is changed to the new password.

**Sources:** `{"source_type":"user_story","source_id":"user_story","locator":"characters 0-8000"}`

### REQ-002 — Show the reset entry point

**Statement:** The sign-in page displays a “Forgot password?” link.

**Acceptance criteria:** Given the sign-in page is displayed, when a customer views it, then a “Forgot password?” link is available.

**Sources:** `{"source_type":"user_story","source_id":"user_story","locator":"characters 0-8000"}`; `{"source_type":"knowledge","source_id":"59efeb19-83f2-4ec6-bfd3-b4aeb7142930","locator":"v1, chunk 0"}` (ACC-STD-01).

### REQ-003 — Start the reset request

**Statement:** Activating the “Forgot password?” link starts the password reset request flow.

**Acceptance criteria:** Given the sign-in page shows the “Forgot password?” link, when a customer activates it, then the customer can begin a password reset request.

**Sources:** `{"source_type":"user_story","source_id":"user_story","locator":"characters 0-8000"}`; `{"source_type":"knowledge","source_id":"59efeb19-83f2-4ec6-bfd3-b4aeb7142930","locator":"v1, chunk 0"}` (ACC-STD-01).

### REQ-004 — Make request responses account-existence neutral

**Statement:** The response to a password reset request is identical whether the requested account exists or does not exist.

**Acceptance criteria:** Given equivalent password reset requests differing only in whether the account exists, when each request is submitted under the same applicable conditions, then their customer-visible responses are identical.

**Sources:** `{"source_type":"knowledge","source_id":"59efeb19-83f2-4ec6-bfd3-b4aeb7142930","locator":"v1, chunk 0"}` (ACC-STD-01).

### REQ-005 — Limit reset requests

**Statement:** Password reset requests are limited to five per account per hour.

**Acceptance criteria:** Given five password reset requests for an account have been permitted in a one-hour period, when another request for that account is submitted within that period, then it is not permitted as an additional reset request; the account-existence-neutral response requirement still applies.

**Sources:** `{"source_type":"knowledge","source_id":"59efeb19-83f2-4ec6-bfd3-b4aeb7142930","locator":"v1, chunk 0"}` (ACC-STD-01).

### REQ-006 — Use a reset link only once

**Statement:** Each reset link can complete no more than one password reset.

**Acceptance criteria:** Given a reset link has been used to complete a reset, when it is used again, then it cannot complete another reset.

**Sources:** `{"source_type":"knowledge","source_id":"59efeb19-83f2-4ec6-bfd3-b4aeb7142930","locator":"v1, chunk 0"}` (ACC-STD-02).

### REQ-007 — Expire reset links

**Statement:** Reset links expire 30 minutes after issuance.

**Acceptance criteria:** Given a reset link was issued 30 minutes ago, when it is used to attempt a reset, then it cannot complete that reset because it has expired.

**Sources:** `{"source_type":"knowledge","source_id":"59efeb19-83f2-4ec6-bfd3-b4aeb7142930","locator":"v1, chunk 0"}` (ACC-STD-02).

### REQ-008 — End every active session after reset

**Statement:** Completing a password reset signs the account out of every active session.

**Acceptance criteria:** Given an account has active sessions, when its password reset completes, then none of those sessions remains signed in to that account.

**Sources:** `{"source_type":"knowledge","source_id":"59efeb19-83f2-4ec6-bfd3-b4aeb7142930","locator":"v1, chunk 0"}` (ACC-STD-02).

### REQ-009 — Notify the account owner

**Statement:** The account owner is notified after every successful password reset.

**Acceptance criteria:** Given an account owner has completed a successful password reset, when the reset completes, then a notification of that reset is sent to that account owner; each subsequent successful reset also produces its own notification.

**Sources:** `{"source_type":"knowledge","source_id":"59efeb19-83f2-4ec6-bfd3-b4aeb7142930","locator":"v1, chunk 0"}` (ACC-STD-03).

## Assumptions

- acceptance-20261025221654-2fb546-skill-sentinel — the acceptance requirements skill produced this map.
- The complete pinned story has no end marker; there are no supplied attachments and thus no acceptance attachment marker.
- The mechanism for verifying account ownership is unspecified; “authorized” in REQ-001 denotes a valid, permitted reset, without prescribing how authorization is established.
- The reset link delivery channel is unspecified; acceptance tests can use an issued link without assuming a particular channel.
- The five-per-account-per-hour quota is tested for an existing account; whether and how nonexistent accounts are internally counted is unspecified. This does not relax identical customer-visible responses.
- No fixed response text is assumed; equivalent existing- and nonexistent-account requests must produce identical customer-visible responses.
- Notification delivery channel is unspecified; REQ-009 tests that the owner is notified without choosing a medium.

## Open questions (non-blocking)

| Question | Working assumption pending clarification |
| --- | --- |
| How is account ownership verified before permitting a reset? | Require an authorized reset, without selecting a verification method. |
| Through what channel is a reset link delivered? | Test with an issued link; do not constrain delivery channel. |
| How are reset requests for nonexistent accounts treated for rate-limit accounting? | Apply the per-account quota to existing accounts; preserve account-existence-neutral responses and leave unknown-account internal accounting unspecified. |
| What exact wording should the reset request response use? | Any wording is acceptable if responses under equivalent conditions are identical for existing and nonexistent accounts. |
| Through what channel is the account owner notified? | Any channel that notifies the owner after each successful reset is acceptable. |
