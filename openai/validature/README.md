# Validature for ChatGPT and Codex

Validature, published by LOGIKS, sends documents for electronic signature and
manages reusable templates. This package includes four workflows: send a file
or template, create and share templates, follow requests, and prepare or resume
a confidential Vault request. Recipients sign in Validature themselves.

The remote MCP server is `https://validature.app/api/v1/mcp`. Sign in to your
existing Validature account through OAuth and approve the requested scopes.
Your account must include the integrations feature. Template changes and
sharing also require the corresponding permissions. After scope changes,
reconnect and review consent.

ChatGPT can provide a native attachment object to `import_document`. Clients
with local file access can use the generated upload command. Otherwise,
`prepare_document_upload` provides a browser upload link. Check the upload with
`get_document_upload` before sending. A draft does not send invitations.

Vault files, recipients and encryption keys remain in the authenticated
browser workflow. The plugin returns a continuation link and structural status;
it does not expose Vault templates, decrypt files or sign on anyone's behalf.
Do not send restricted personal data or authentication secrets through the
plugin, including by switching to an upload or Vault link.

This is a portable Agent Plugins package: `plugin.json`, `mcp.json`, four
`skills/` directories and local brand assets. Package version: **1.2.0**.
Publication in the OpenAI directory is a separate reviewed portal process;
a package in Git does not establish approval or production availability.

[Website](https://validature.com) · [Support](https://validature.com/contact/) ·
[Privacy](https://validature.app/privacy) · [Terms](https://validature.app/terms)

See [the submission guide](../SUBMISSION.md) in the source repository for
review prerequisites and portal steps. The package is distributed under the
included MIT license.
