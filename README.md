# Validature plugins for AI assistants

Electronic signature from your AI assistant: send documents for signature from your
[Validature](https://validature.app) templates, follow who signed, and send reminders.
Validature is hosted in France and follows eIDAS.

Everything goes through the Validature remote MCP server, `https://validature.app/api/v1/mcp`,
with OAuth: no API key to copy. Recipients always sign on Validature, never through the assistant,
and the assistant asks for your confirmation before sending anything.

## Claude Code and Claude Cowork

```
/plugin marketplace add blackjackparis/validature-plugins
/plugin install validature@validature
```

Then run `/mcp` and sign in to Validature when prompted.

The plugin bundles the MCP server and two skills:

- `send-for-signature`: pick a template, fill in the recipients, confirm, send.
- `follow-signatures`: status of your requests, who still has to sign, reminders, signed documents.

## ChatGPT and Codex

`openai/validature/` contains the same plugin in the Agent Plugins format.

## Requirements

A Validature account on a plan that includes integrations (Standard or above).
Encrypted (Vault) requests stay readable by their recipients only: the assistant sees neither
their title nor their documents.

## Support

contact@validature.com · https://validature.app

---

# Plugins Validature pour assistants IA

Signature électronique depuis votre assistant IA : envoyez des documents à signer depuis vos
modèles Validature, suivez les signatures et relancez. Connexion par OAuth au serveur MCP
`https://validature.app/api/v1/mcp`, sans clé à copier. Les destinataires signent toujours sur
Validature, et l'assistant demande votre accord avant chaque envoi.
