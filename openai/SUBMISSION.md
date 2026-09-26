# Soumission OpenAI — ChatGPT et Codex

Version du package : **1.2.0**. Portail :
[OpenAI Platform › Plugins](https://platform.openai.com/plugins), création
« With MCP ». Le package portable se trouve dans `openai/validature/` depuis
la racine du dépôt public des plugins. La soumission utilise le serveur HTTPS
et le bundle de skills ; aucun identifiant d'intégration inventé n'est requis.

## Fiche

| Champ | Valeur |
| --- | --- |
| Nom | Validature |
| Sous-titre | Documents, templates and Vault |
| Catégorie | Productivity |
| Serveur MCP | `https://validature.app/api/v1/mcp` |
| Description | Send documents for electronic signature, create and share reusable templates, follow signers, send reminders and retrieve signed files. Prepare confidential Vault requests and continue encryption, recipient setup and sending in the secure Validature browser. |
| Site | https://validature.com |
| Confidentialité | https://validature.app/privacy |
| Conditions | https://validature.app/terms |
| Assistance | contact@validature.com |
| Icône / logo | `openai/validature/assets/icon.svg`, `logo.svg` |
| Authentification | OAuth avec PKCE ; connexion au compte Validature ; aucune clé API demandée à l'utilisateur |

Dans le dépôt applicatif, `chatgpt-app-submission.json` contient les
annotations et justifications de chaque outil, cinq cas positifs et trois cas
hors périmètre. Ce fichier décrit le code candidat ; il ne prouve pas que
cette version est déjà en production. Charger le fichier quand le portail
propose l'import des informations de soumission.

## Vérifications avant le dépôt

1. Faire vérifier l'identité de l'organisation éditrice dans OpenAI Platform,
   avec les droits permettant de soumettre et publier le plugin.
2. Déployer le backend candidat par le workflow GitHub habituel après fusion
   et contrôles réussis. Vérifier le SHA actif, puis tester le serveur et les
   quatre parcours dans les clients réels.
3. Mettre à jour le miroir public des plugins en conservant la même version
   dans les manifestes Claude, OpenAI et la marketplace.
4. Publier **le jeton exact fourni par le portail** via `OPENAI_APPS_CHALLENGE`
   pour que `https://validature.app/.well-known/openai-apps-challenge` rende
   uniquement ce jeton. Le backend lit cette variable au runtime ; le frontend
   récupère la preuve publique par `/api/v1/oauth/openai-apps-challenge` lorsque
   son environnement isolé ne reçoit pas la variable. La configuration serveur
   passe par le circuit de déploiement autorisé. Ne pas remplacer le jeton d'un autre plugin actif.
5. Préparer le compte de revue et les données fictives décrits dans
   [../SUBMISSION.md](../SUBMISSION.md). Communiquer les accès dans les champs
   privés du portail, jamais dans Git.
6. Exécuter « Scan Tools », vérifier les scopes et les annotations, joindre
   les skills testées, terminer la soumission, puis suivre les retours. Une
   approbation puis une publication explicite sont nécessaires avant
   d'annoncer une disponibilité dans l'annuaire.

## Pièces jointes et confidentialité

`import_document` déclare `_meta["openai/fileParams"]: ["file"]`. Le schéma
comprend les quatre propriétés attendues : `download_url`, `file_id`,
`mime_type`, `file_name` ; seules les deux premières sont obligatoires.
Le serveur reçoit un document standard puis applique ses contrôles de dépôt.
Le dépôt navigateur reste disponible avec `prepare_document_upload` et
`get_document_upload` quand le client ne transmet pas la pièce jointe.

Les outils Vault ne reçoivent aucun fichier, destinataire, mot de passe, clé
ou phrase de récupération. `prepare_vault_request` prépare un brouillon et
rend un lien vers le navigateur authentifié ; `get_vault_request` ne retourne
que l'état structurel autorisé. Le protocole effectivement activé est
explicite dans la réponse. La prise en charge Vault ne doit pas être décrite
comme un envoi chiffré intégralement exécuté dans le chat.

Les outils de signature demandent des noms, emails et éventuellement un
numéro de téléphone lorsque nécessaire au parcours. Les liens de fichiers
sont temporaires et personnels. Ils ne doivent pas apparaître dans des
journaux de soumission ni dans des exemples publics réels.

Il n'y a pas de widget embarqué ni de CSP de widget à fournir pour cette
version. Les handoffs ouvrent les pages Validature dans le navigateur.

Sources : [soumission](https://developers.openai.com/plugins/deploy/submission),
[format de package](https://developers.openai.com/plugins/build/plugins),
[contrat fichiers](https://developers.openai.com/plugins/reference), vérifiés
le 27 septembre 2026.
