# Plugins Validature pour assistants IA

Ce dossier contient les packages **1.2.0** pour Claude et OpenAI. Le miroir de
distribution est [blackjackparis/validature-plugins](https://github.com/blackjackparis/validature-plugins).
Les modifications de ce dossier doivent être reportées dans ce dépôt par PR.
Une version dans Git ne prouve ni son déploiement backend ni son acceptation
dans un annuaire officiel.

Les deux packages utilisent `https://validature.app/api/v1/mcp`, avec OAuth :
aucune clé à copier. Ils fournissent quatre parcours :

- `send-for-signature` : fichier joint ou local, dépôt dans le navigateur,
  modèle existant, brouillon et envoi ;
- `manage-templates` : création, modification, duplication et partage des
  modèles standards ;
- `follow-signatures` : statut, relances, annulation et documents signés ;
- `vault-signatures` : préparation d'un brouillon confidentiel, ouverture du
  navigateur sécurisé et suivi des métadonnées autorisées.

Vault conserve le choix et le chiffrement des fichiers, les destinataires et
l'envoi dans le navigateur authentifié. Les modèles Vault ne sont pas exposés.
Les invitations, relances, annulations et changements d'accès demandent une
autorisation explicite portant sur l'action présentée.

## Claude

`validature/` utilise `.claude-plugin/plugin.json`, `.mcp.json` et `skills/`.
La marketplace `.claude-plugin/marketplace.json` le référence.

Dans Claude Code, après publication de la version dans le miroir :

```text
/plugin marketplace add blackjackparis/validature-plugins
/plugin install validature@validature
```

Puis `/mcp` permet de se connecter. Sans plugin :

```sh
claude mcp add --transport http validature https://validature.app/api/v1/mcp
```

Dans Claude sur le web ou Cowork : **Customize › Connectors › + › Add custom
connector**, avec l'URL MCP. Un client qui ne peut pas transmettre le fichier
utilise le lien de dépôt navigateur rendu par `prepare_document_upload`.
Le connecteur seul fournit les outils, le package ajoute les quatre skills.

Le [portail de soumission Claude](https://claude.ai/directory/manage/new)
accepte un serveur MCP ou un bundle GitHub. L'acceptation et la publication
sont des étapes du portail ; elles ne résultent pas automatiquement d'un push.
Voir [SUBMISSION.md](SUBMISSION.md).

## ChatGPT et Codex

`openai/validature/` suit le format portable Agent Plugins : `plugin.json`,
`mcp.json`, `skills/`, `assets/` et `LICENSE`. Les données de présentation
OpenAI sont dans `extensions.com.openai`.

Dans Codex, la connexion directe fonctionne sans publication du package :

```sh
codex mcp add validature --url https://validature.app/api/v1/mcp
codex mcp login validature
```

ChatGPT transmet les pièces jointes à `import_document` via le contrat natif
`openai/fileParams`. Pour un client sans ce transport, utiliser le fichier
local ou le dépôt navigateur décrit dans la skill. Ne pas remplacer les
fichiers chiffrés Vault par ce dépôt standard.

La publication dans l'annuaire partagé ChatGPT/Codex se prépare dans
[openai/SUBMISSION.md](openai/SUBMISSION.md). Le titulaire de l'organisation
publie le jeton de domaine fourni par le portail avec le circuit de déploiement
normal, puis soumet la version testée.

## Validation avant distribution

Depuis la racine de ce dossier :

```sh
claude plugin validate validature
claude plugin validate .
```

Valider aussi `openai/validature/plugin.json` et `mcp.json` avec leurs schémas
Agent Plugins déclarés. Les quatre skills doivent rester identiques entre
les packages Claude et OpenAI. Après une évolution des scopes OAuth,
reconnecter une installation existante pour consentir aux nouvelles actions.
Le test avec les vrais clients doit couvrir les fichiers, les droits de
partage et la reprise du parcours Vault avant de déclarer une version prête
pour l'annuaire.
