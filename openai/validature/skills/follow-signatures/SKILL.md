---
name: follow-signatures
description: Check Validature signature requests, identify outstanding signers, send reminders, cancel a request and retrieve signed documents and certificates. Use for status, follow-up, cancellation or signed PDF requests. Encrypted Vault content stays in the secure browser.
---

# Follow signature requests in Validature

1. Find a standard request with `list_requests`, using its title (`search`), `status` or `recipientEmail`. If multiple requests match, identify the correct one before any action.
2. Call `get_request` for signer details and current status. Include the request link in the summary.
3. For reminders, show who will receive the email and obtain explicit authorization, then call `send_reminder`. Report only the recipients the tool confirms were reminded.
4. Before `cancel_request`, identify the request and explain that recipients will no longer be able to sign it. Obtain explicit authorization and report the returned outcome.
5. For a completed standard request, call `get_signed_documents`. Return its personal links to the signed files, certificate and ZIP. They expire after 30 minutes. Download them only when the user wants saved copies; avoid exposing their tokens in logs or unrelated messages.

For Vault requests, use `get_vault_request` with a known request ID and give its secure browser continuation link. The tool exposes structural progress only. Do not infer identities, titles or document contents from redacted metadata; do not ask for decryption keys. Reading encrypted files, sending or retrieving Vault documents happens in the browser using the `vault-signatures` skill.

Never claim a document was signed merely because its invitation was sent or opened. If a write result is uncertain, read the current request state before attempting it again.

## OpenAI data boundary

When running in ChatGPT or Codex, do not collect, import, retrieve or process documents containing payment-card data subject to PCI DSS, protected health information, government identifiers or authentication secrets. If the user identifies such contents, explain the restriction without requesting the sensitive values; do not use browser upload or Vault as a workaround. For other regulated sensitive data, require the legally adequate consent and prominent collection notice required by the host policy. This rule does not require reading an otherwise unopened file merely to classify it.
