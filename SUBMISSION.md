# Distribution Claude et vérification commune

## Fiche de soumission Claude

| Champ | Valeur |
| --- | --- |
| Nom | Validature |
| Description | Envoyez vos documents à signer, créez et partagez des modèles, suivez les signatures et retrouvez les documents signés. Préparez vos demandes Vault et terminez le chiffrement et l'envoi dans le navigateur sécurisé Validature. |
| Dépôt | https://github.com/blackjackparis/validature-plugins |
| Marketplace | `.claude-plugin/marketplace.json` |
| Package | `validature/`, version 1.2.0 |
| Serveur MCP | `https://validature.app/api/v1/mcp` |
| Authentification | OAuth avec PKCE, connexion au compte Validature |
| Confidentialité | https://validature.app/privacy |
| Conditions | https://validature.app/terms |
| Assistance | contact@validature.com |

Le [portail Claude](https://claude.ai/directory/manage/new) accepte la
soumission depuis un compte Claude payant. Sélectionner le bundle GitHub pour
inclure les skills ou le serveur MCP pour un connecteur seul. Le portail
valide le package, affiche les retours de revue, puis permet au titulaire de
publier après approbation. Ne pas confondre le miroir GitHub, l'installation
directe, la soumission et la publication officielle.

## Compte de démonstration à fournir hors du dépôt

Utiliser un compte de revue dédié, sur une offre Validature avec intégrations,
avec des données fictives et des boîtes email de test contrôlées :

- un document standard PDF et un document Word à déposer ;
- des modèles « NDA », « Devis » et « Bail », avec des rôles identifiables ;
- un collègue de test pour partager un modèle et retirer son accès ;
- une demande standard en cours et une demande terminée avec documents signés ;
- un compte autorisé à préparer un brouillon Vault, avec le protocole
  effectivement activé pour ce compte.

Donner les identifiants et consignes de connexion aux relecteurs uniquement
dans les champs privés du portail. Ne pas désactiver l'authentification des
comptes réels pour faciliter une revue.

## Vérification dans chaque client

| Parcours | Résultat à constater |
| --- | --- |
| Fichier joint ChatGPT | Import réel des octets, analyse puis brouillon ; après accord, invitation reçue dans la boîte de test |
| Fichier local Claude Code / Codex | Dépôt par le lien temporaire puis envoi du même document |
| Dépôt navigateur | Choix du fichier par l'utilisateur puis récupération du `documentId` avec `get_document_upload` |
| Modèle | Création depuis le fichier, configuration des rôles/champs, réutilisation du modèle dans une demande |
| Partage | Permissions du collègue conformes au droit accordé, puis refus d'accès après révocation |
| Vault | Brouillon ouvert dans l'éditeur authentifié ; fichier chiffré et envoi effectués dans le navigateur ; aucun contenu, nom, email ou secret dans `get_vault_request` |
| Documents signés | Liens valides du PDF, du certificat et du ZIP pour une demande terminée |
| Révocation OAuth | Retrait de l'assistant dans Réglages › Intégrations ; ses anciens appels et liens temporaires sont refusés |

Les tests unitaires prouvent les contrats serveur ; les observations ci-dessus
prouvent les parcours complets des clients. Conserver séparément la date, le
SHA backend, la version du package, le client testé et le résultat. N'inscrire
aucun résultat « réussi » avant d'avoir exécuté le parcours.

## Sources officielles vérifiées le 27 septembre 2026

- [Publication de plugins Claude](https://claude.com/blog/build-plugins-for-claude)
- [Manifeste Claude](https://code.claude.com/docs/en/plugins-reference)
- [Connecteurs personnalisés](https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities)
- [Package portable OpenAI](https://developers.openai.com/plugins/build/plugins)
- [Fichiers ChatGPT](https://developers.openai.com/plugins/reference)
- [Soumission OpenAI](https://developers.openai.com/plugins/deploy/submission)
