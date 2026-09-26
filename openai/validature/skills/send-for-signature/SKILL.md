---
name: send-for-signature
description: Send a document for electronic signature with Validature, from an attached or local PDF, Word or RTF file or an existing template. Use for contracts, NDAs, quotes, leases, drafts and sending an existing draft. For encrypted Vault documents, use the vault-signatures skill.
---

# Send a document for signature with Validature

Use the Validature MCP tools. Validature sends invitation emails; each recipient signs on Validature. Never sign for someone else or invent contact details.

## Choose the document

For a standard document, use the first available method:

1. **Conversation attachment:** if the host supplies a file object, call `import_document` with that object. ChatGPT supplies `download_url` and `file_id`, and may supply `file_name` and `mime_type`. Do not invent these values or turn a local file path into an internet URL. Keep temporary attachment links out of user-facing summaries.
2. **Readable local file:** call `prepare_document_upload` with the path in `fileName`, then run the returned upload command with that file. The upload response contains `documentId`.
3. **Browser upload:** if the assistant cannot access the bytes, call `prepare_document_upload` and give the user its `browserUrl`. They choose the file on that page. Keep `uploadId` and call `get_document_upload` when the user has finished; continue when it returns a `documentId`. A waiting upload is not a completed upload. If the link expires, prepare another.

Use `list_templates` and `get_template` instead when the user wants an existing reusable template. Read each recipient `roleKey` and fixed recipient before composing the request.

For a confidential Vault document, switch to `vault-signatures` before uploading. Vault files, keys and recovery material must stay in the secure browser flow.

## Prepare and send

1. Collect the title and each recipient's first name, last name and email. Look up names with `search_contacts`; ask for clarification if a name is ambiguous or an email is missing. Read template roles with `get_template` and map each recipient to a role.
2. Show the concrete file or template, request title, recipients with email addresses, message and signing order before sending. Obtain explicit authorization for that exact send. An earlier approval of the same summary is sufficient; a changed recipient or document needs a new approval.
3. For an uploaded document, call `send_document` with `documentId` and the recipients. Use `signingOrder: "sequential"` only when ordered signing is requested. For a template, call `send_template` with `templateId`, the role assignments and a fresh UUID v4 `idempotencyKey` for this intentional request. Keep that same key and identical arguments on retries; use a new key only for a separately authorized new request, even if its recipients and content match an earlier one. Omitting the key deduplicates identical account, connection and request inputs.
4. Use `send: false` to create a draft without emails. Return its request link for review. For an existing draft, use `get_request` to confirm its details, then `send_draft` after authorization.
5. Report the returned request link and actual outcome: draft, sent or already sent. Mention fallback signature placement at the bottom of the last page when the tool reports it, so the user can review the placement.

If `send_document` says antivirus analysis is pending, retry with the same arguments after a short wait. Do not claim success before the tool confirms it. For an uncertain `send_template` result, retry the same key and arguments or inspect recent requests; do not mint a new key merely because a response was interrupted.

The integration requires a Validature plan with integrations (Standard or above). A missing OAuth scope requires reconnecting the assistant and consenting to the requested access; do not work around it with a password or API key.

## OpenAI data boundary

When running in ChatGPT or Codex, do not collect, import, retrieve or process documents containing payment-card data subject to PCI DSS, protected health information, government identifiers or authentication secrets. If the user identifies such contents, explain the restriction without requesting the sensitive values; do not use browser upload or Vault as a workaround. For other regulated sensitive data, require the legally adequate consent and prominent collection notice required by the host policy. This rule does not require reading an otherwise unopened file merely to classify it.
