---
name: follow-signatures
description: Check where Validature signature requests stand, who opened or signed, and send reminders or cancel. Use when the user asks about the status of a contract, who still has to sign, or to chase signers.
---

# Follow signature requests in Validature

1. Find the request with `list_requests`: filter by `status` (sent, ongoing, completed, declined, expired, canceled), by part of the title (`search`) or by `recipientEmail`.
2. Call `get_request` for the details: for each recipient, whether they were notified, opened, signed or declined.
3. To chase the people who have not signed, call `send_reminder` after telling the user who will receive it.
4. To stop a request, confirm with the user, then call `cancel_request`. A canceled request cannot be signed anymore.

Summaries should name the signers and their state, and include the request link.
