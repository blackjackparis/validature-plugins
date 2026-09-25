---
name: send-for-signature
description: Send a document for electronic signature with Validature from one of the account templates. Use when the user asks to send a contract, NDA, quote, lease or any document to someone for signature.
---

# Send a document for signature with Validature

Use the Validature MCP tools. Validature sends the invitation emails itself; the recipients sign on Validature, never through you.

1. Find the template: call `list_templates` (with a `search` term when the user names the document). If several templates match, ask which one.
2. Read its recipient roles with `get_template`. Each role has a `roleKey`; fixed roles are prefilled and may be left as they are.
3. Get each recipient’s email address. Use `search_contacts` when the user gives a name. Never invent or guess an address; ask the user when it is missing or ambiguous.
4. Show a short summary before sending: template, request title, and every recipient with name, email and role. Wait for an explicit “yes”.
5. Call `send_template` with the `templateId` and one entry per role (`roleKey`, `email`, `firstName`, `lastName`). Use `send: false` when the user wants a draft to review in Validature first; `send_draft` sends it later.
6. Report the result with the request link returned by the tool.

If a tool answers that the plan does not include integrations, tell the user integrations start with the Standard plan.
