---
name: vault-signatures
description: Prepare or resume a confidential Validature Vault signature request and check its safe progress. Use when the user asks for Vault, encrypted documents or a secure signature workflow. File encryption, recipients and sending are completed in Validature's authenticated browser.
---

# Use Validature Vault

Vault is a browser workflow. The assistant prepares a draft or checks structural progress; it must never collect the document, a decryption key, a recovery phrase or encrypted key material through MCP.

1. Call `prepare_vault_request` to create a draft, or include a known `requestId` to resume it. Supply `signatureLevel` (`SES` or `AES`) and `expirationDays` only when the user has specified them.
2. Respect a requested protocol. `zero-access-v2` requires the account's active rollout; do not silently use `legacy-v1` if zero-access is requested and unavailable. Without a protocol request, the server selects the available account configuration and returns the actual version and `metadataProtection`.
3. Give the returned `continuationUrl` to the user. Explain that they choose and encrypt the file, enter recipients, review fields and confirm sending in the authenticated Validature editor. The tool has prepared a draft, not sent an invitation.
4. After the browser step, call `get_vault_request` with `requestId` for the safe status, counts and timestamps. Report only the progress returned. If the user needs content, identities, detailed editing or signed files, open or provide the secure continuation link.

A draft link never establishes that sending is complete. Do not pass a Vault file to `import_document` or the standard upload, template or send tools. Never claim legacy Vault has the zero-access metadata guarantees of V2. Vault-specific reusable templates are not exposed by this integration; explain this limit if asked, without converting confidential content into a standard template.
