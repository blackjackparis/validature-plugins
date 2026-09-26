---
name: manage-templates
description: Create, inspect, duplicate, edit, archive and share reusable Validature signature templates. Use when the user asks for a model, reusable contract, recipient roles, signature fields or template access for a colleague. Supports standard documents; Vault stays in the secure browser workflow.
---

# Manage reusable templates in Validature

A template stores reusable documents, recipient roles and fields. Creating or sharing one does not send it for signature. Use `send-for-signature` for invitations.

## Create or duplicate

1. For a new file, use `import_document` or `prepare_document_upload` followed by the upload and, when needed, `get_document_upload`, as described in `send-for-signature`.
2. Call `create_template` with a name, one new UUID v4 `idempotencyKey` and exactly one source: `documentIds` or an existing standard `requestId`.
3. For `documentIds`, describe each recipient role with `roleKey`, `label` and optional `role` (`signer`, `approver`, `reader`). Omit `email` for a reusable variable role. Supply a fixed email only when the user explicitly wants that person in every future use. Without custom roles, the server creates a variable signer.
4. For `requestId`, the server derives roles, order and fields from the original documents, without carrying over fixed recipient emails or security codes. Do not also supply roles, fields or signing order. Do not use a signed output PDF as a reusable source.
5. When fields are omitted for uploaded documents, the server places signature fields automatically. Return the template ID and describe the available roles; use `get_template` to review document IDs and fields before fine-tuning.
6. To copy an existing template, call `duplicate_template` with `templateId`, the new name and a new `idempotencyKey`. Sharing is managed separately.

Retain the same idempotency key and identical arguments when retrying the same create or duplicate operation. Use a new key for a distinct model. Do not pass encrypted Vault documents to these tools.

## Edit and archive

Use `list_templates` to locate a template, then `get_template` to inspect it. Use `update_template` for its name, description, active or archived state. Show the change before overwriting existing settings; obtain the user's authorization for archiving or disabling a shared template.

`set_template_fields` replaces the **entire** field list. First read `get_template` and check `fieldCoordinateUnit`. Only `pdf-points` fields can be retained unchanged. For `legacy-unmarked`, do not guess or relabel the coordinates: ask the user to review and save the model in Validature, or replace the complete list with independently measured PDF points. Preserve the fields the user wants to keep and explain the replacement. Pass `fieldCoordinateUnit: "pdf-points"` explicitly. Each field uses a document ID from this template, a known recipient `roleKey`, a 1-based page and coordinates in PDF points from the top-left. Do not guess page geometry. If reliable coordinates are unavailable, have the user review fields in the Validature editor. An empty field list removes all fields and requires explicit approval.

## Share with a colleague

1. Call `list_template_shares` to inspect existing access. This operation and access changes require the template owner or an organization administrator.
2. Identify one existing organization member by exact `email` or verified `userId`. Never guess either value. Sharing follows the account's organization and domain restrictions; it is not a public link or an invitation to an arbitrary external address.
3. State which template and which member will gain access, then obtain explicit authorization. Call `share_template` with exactly one of `email` or `userId`.
4. To remove access, state the affected member and template, obtain explicit authorization, then call `revoke_template_share`. Confirm the result through the returned share state or `list_template_shares`.

Template mutation uses `templates:write`; sharing uses `templates:share`. If an existing assistant connection lacks a scope, ask the user to reconnect and approve the new scope. The account also needs the templates feature. Never fall back to a more privileged credential.
