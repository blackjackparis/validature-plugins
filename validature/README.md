# Validature for Claude

Send documents for electronic signature, create and share reusable templates,
follow signature requests and retrieve signed files from Claude. This plugin
adds four skills and the Validature remote MCP connector. Each recipient
reviews and signs in Validature; Claude does not sign on anyone's behalf.

## Requirements

Use your own Validature account with an offer that includes integrations
(Standard or above). Template and Vault actions also require the corresponding
features and account permissions. Connect the MCP server with OAuth; no API
key or password is stored in this plugin. If an existing connection lacks new
template permissions, reconnect it and review the requested access.

## Install and connect

For Claude Code, install from the public Validature marketplace:

```text
/plugin marketplace add blackjackparis/validature-plugins
/plugin install validature@validature
```

Use `/mcp` to connect your Validature account. The version installed is the
version published in the marketplace repository; a change in the application
repository alone does not update that package.

In Claude chat or Cowork, add the plugin from **Customize > Plugins** when it
is available in your directory or marketplace, then open its **Connectors**
tab and connect Validature. Adding the plugin does not replace OAuth sign-in.
Organization policies can limit which plugins or connectors are available.

For the connector alone, use **Customize > Connectors > + > Add custom
connector** with `https://validature.app/api/v1/mcp`. On Team and Enterprise,
an organization Owner first adds it in **Organization settings > Connectors**.
The connector alone exposes the tools; the plugin also supplies the skills.
See Claude's [platform support](https://claude.com/docs/plugins/platform-support)
and [custom connector guide](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp).

## Example requests

- “Prepare this agreement for Alice to sign, and show me the draft.”
- “Create a reusable NDA model with a customer signature role.”
- “Share the NDA model with my colleague, after showing me their email.”
- “Which requests are waiting for a signature?”
- “Prepare a confidential Vault request and open its secure editor.”

For a standard file, use the browser upload link when Claude cannot pass the
file's bytes. Claude Code can upload a readable file that you selected using
the temporary upload command returned by Validature. Review the document,
recipients and message before authorizing an invitation, reminder or access
change. Draft creation does not send an invitation.

Vault files and encryption secrets stay in the authenticated Validature
browser workflow. The connector prepares or resumes a draft and reports safe
structural progress. File choice, encryption, recipients, field review and
sending are completed in that browser. Vault-specific templates and decrypted
Vault downloads are not exposed through this connector.

## Data, privacy and support

The declared MCP endpoint and its upload/download links use
`https://validature.app`. An authorized standard upload sends the selected
document to Validature for storage and processing. Tool calls can exchange
document and template metadata, recipient contact details, messages, signature
status and temporary download links. Invitations and reminders use
Validature's delivery services. The connector's results are visible to Claude
and processed under the terms of the Claude service you use. Never supply
unrelated conversation history, passwords or Vault secrets.

This package contains Markdown skills and JSON configuration; it installs no
local MCP executable, hook or background process. Document retention and
deletion follow the [Validature privacy policy](https://validature.app/privacy)
and [terms](https://validature.app/terms); the package does not promise a
different retention period. Revoke the connection in Validature's
**Settings > Integrations > AI assistants** to stop its future access.

For product support, contact **contact@validature.com**. For data rights and
security concerns, the published legal notice lists **contact@logiks.fr**.
Do not send credentials or confidential documents to support without an
appropriate secure process. Plugin source:
[blackjackparis/validature-plugins](https://github.com/blackjackparis/validature-plugins).
The plugin package is licensed under [MIT](LICENSE); the hosted service is
governed by its own terms.
