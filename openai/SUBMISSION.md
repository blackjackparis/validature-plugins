# Soumission OpenAI — ChatGPT et Codex

Package **1.2.0**, format portable Agent Plugins, dossier `openai/validature/`
dans le dépôt public. Portail : [OpenAI Platform › Plugins](https://platform.openai.com/plugins).
La voie publique est **Create plugin › With MCP › Universal**, avec le serveur
HTTPS et les quatre skills. Un dépôt Git, un connecteur de développement ou un
fichier de soumission validé ne vaut pas publication officielle.

## Fiche à saisir

| Champ | Valeur |
| --- | --- |
| Nom public | Validature |
| Éditeur | LOGIKS, société exploitant la marque Validature ; sélectionner son identité vérifiée dans le portail |
| Sous-titre | Documents, templates and Vault |
| Catégorie | Productivity |
| Serveur MCP universel | `https://validature.app/api/v1/mcp` |
| Description | Send documents for electronic signature, create and share reusable templates, follow signers, send reminders and retrieve signed files. Prepare confidential Vault requests and continue encryption, recipient setup and sending in the secure Validature browser. |
| Site | https://validature.com |
| Assistance publique | https://validature.com/contact/ |
| Contact de support | contact@validature.com |
| Confidentialité | https://validature.app/privacy |
| Conditions | https://validature.app/terms |
| Icône / logo | `openai/validature/assets/icon.svg`, `logo.svg` ; SVG carrés |
| Authentification | OAuth, code d'autorisation et PKCE S256 ; connexion au compte Validature |

La page de contact et les mentions légales publiques identifient LOGIKS comme
éditeur de Validature. Les politiques applicatives indiquent aussi LOGIKS et
`contact@logiks.fr` pour les droits et réclamations. Le compte de soumission doit
prouver cette identité ; une marque produit seule ne prouve pas une identité
vérifiée. Vérifier que les deux adresses de contact restent opérationnelles.

Le dossier `chatgpt-app-submission.json` contient les annotations justifiées,
cinq cas positifs et trois négatifs. Il décrit le candidat et ne constitue ni
un résultat de test en production ni un remplacement de tous les champs privés
du portail. L'importer uniquement là où le portail propose cet import.

## Préparer les preuves réelles

1. Faire vérifier l'identité LOGIKS dans la bonne organisation OpenAI Platform.
   Le déposant doit avoir **Apps Management: Write** ; un propriétaire dispose
   déjà de ces droits. Ne pas déclarer l'identité vérifiée sans confirmation du portail.
2. Livrer le backend par le workflow GitHub habituel après fusion et contrôles,
   puis rapprocher le SHA actif et la version testée. Synchroniser le miroir
   public par PR avec les mêmes fichiers et versions.
3. Préparer un compte de revue complet, des contacts fictifs contrôlés, un collègue
   éligible au partage, un fichier standard non sensible, une demande en attente
   et une demande standard terminée. Les cinq tests doivent être reproductibles
   sans accès au réseau interne, inscription, code SMS, confirmation email ou MFA.
   Renseigner les identifiants uniquement dans les champs privés du portail.
4. Exécuter les cas avec les clients ChatGPT et Codex réellement annoncés,
   y compris OAuth, import natif, dépôt navigateur, modèles, partage, relance,
   fichier signé et retour Vault. Un test unitaire ou HTTP ne remplace pas ces essais.
   Joindre les fichiers de test fictifs nécessaires : les URL actuellement
   `null` dans le JSON ne fournissent aucune pièce jointe aux évaluateurs.
5. Enregistrer une démonstration des principaux outils et parcours sur les
   plateformes prises en charge. Fournir l'URL accessible aux évaluateurs dans
   le champ **demo recording**. Aucune vidéo ni URL de démonstration n'est
   fabriquée ou fournie par ce dossier.

## Remplir et soumettre le portail

1. **Info** : saisir la fiche ci-dessus et sélectionner l'identité vérifiée.
   Nom et sous-titre : 30 caractères maximum chacun ; description : 4 000 ;
   nom développeur : 80. Utiliser des URL HTTPS publiques pour site, support,
   confidentialité et conditions. Le package contient trois amorces, chacune
   sous 128 caractères, sans mention MCP.
2. **MCP** : choisir **Universal**, saisir l'URL de production et l'authentification,
   puis les accès de revue. Ne pas saisir un ancien identifiant d'intégration.
   Le serveur propose PKCE et DCR/CIMD : tester le mode effectivement sélectionné.
3. **Verify Domain** : publier le jeton exact du portail via `OPENAI_APPS_CHALLENGE`
   au travers du circuit de configuration et déploiement autorisé. L'URL
   `https://validature.app/.well-known/openai-apps-challenge` doit répondre avec
   ce seul jeton. Le backend le lit au runtime ; le frontend utilise son pont
   public `/api/v1/oauth/openai-apps-challenge`. Pas de JSON, de liste ou de
   jeton inventé. Ne pas écraser la preuve d'un autre plugin actif : utiliser
   une origine parente autorisée ou un hôte distinct avec OpenAI si nécessaire.
4. **Scan Tools** : scanner la version réellement déployée, corriger les erreurs
   et rescanner. Vérifier tous les outils, leurs schémas et les trois annotations.
   Les justifications du JSON doivent correspondre au scan courant.
5. **Skills** : joindre les quatre skills finales du package. Ce serveur ne les
   expose pas via l'extension MCP de skills : Scan Tools ne les importe donc
   pas automatiquement. Attendre le succès des scans de sécurité/politique.
6. **Prompts / Testing** : renseigner les trois amorces puis exactement cinq cas
   positifs et trois négatifs avec résultats attendus et données de reproduction.
   Confirmer les preuves du compte et de la vidéo. Sans widget, ne pas ajouter
   de captures d'écran de l'application au champ screenshots.
7. **Global / Submit** : choisir seulement les pays où produit, conditions et
   support sont prêts ; ajouter les notes de version et les limites Vault.
   Remplir les attestations après vérification, puis **Submit for Review**.
8. Après approbation OpenAI, publier explicitement dans le portail. Cette
   publication rend le plugin disponible dans l'annuaire commun ChatGPT/Codex.
   Les changements de fiche ou de skills nécessitent une nouvelle version revue.

## Contrats techniques et limites

Le format courant est `plugin.json` + `mcp.json` + `skills/`, avec la présentation
dans `extensions.com.openai`. L'ancien `.codex-plugin/plugin.json` reste un format
de compatibilité ; il n'est pas requis ici. Les SVG sont acceptés pour les
marques si carrés et au moins 48 × 48 ; chaque fichier reste sous 5 Mio.

`import_document` utilise `_meta["openai/fileParams"]: ["file"]`.
`download_url` et `file_id` sont obligatoires ; `mime_type` et `file_name` sont
facultatifs. Le client doit fournir l'objet réel. À défaut, le dépôt navigateur
et `get_document_upload` continuent le parcours. Ne jamais inventer un lien de fichier.

Les mutations, invitations, relances et révocations portent des annotations
conformes à leurs effets réels. Un outil en lecture ne doit pas cacher de
mutation. Les schémas de sortie génériques acceptent les objets retournés mais
ne remplacent pas une vérification des réponses et de leur minimisation.

Les outils Vault ne reçoivent ni fichiers, ni destinataires, ni clés. Ils
préparent un brouillon, ouvrent le navigateur authentifié et lisent seulement
l'état structurel. Le protocole et sa protection de métadonnées sont explicites.
Ne pas promettre un envoi Vault complet dans le chat, des modèles Vault ou les
garanties zero-access V2 pour un compte qui utilise V1.

L'authentification OAuth générale ne nécessite pas de revendiquer OpenID Connect.
La protection **Enterprise workspace domain restrictions** est distincte : elle
requiert une vraie identité email vérifiée, UserInfo et des scopes `openid` et
`email` annoncés et utilisables. Elle n'est pas qualifiée dans cette version.
Ne pas ajouter ces scopes ni affirmer `email_verified: true` sans preuve et
prise en charge complète. Le domaine vérifié du plugin n'est pas cette protection.

## Politique des parcours

Le plugin transmet des invitations ; il ne signe jamais à la place d'un tiers
et ne donne pas une certification juridique générale. Les politiques OpenAI
ne prohibent pas globalement l'envoi de contrats, mais interdisent la fraude,
l'usurpation et la falsification. Les documents contenant des données PCI,
des informations de santé protégées, des identifiants gouvernementaux ou des
secrets d'authentification ne doivent pas être collectés ou traités par le
plugin. Un lien d'upload ou Vault ne doit pas servir à contourner cette règle.
Les autres données sensibles exigent les conditions de consentement et
information prescrites par les politiques applicables.

L'accès à un compte déjà abonné est autorisé. Le plugin peut expliquer une
fonction non incluse ; il ne doit vendre ni promouvoir un abonnement, des
crédits ou une montée en gamme. Les liens de fichiers personnels ne doivent
pas apparaître dans une vidéo publique, des logs ou les fixtures du dossier.

Cette version n'a pas d'interface MCP embarquée : aucune CSP de widget ni
capture de widget n'est nécessaire. Les liens de continuation ouvrent le
navigateur. La revue finale doit confronter les données effectivement rendues
aux catégories, destinataires, durées et droits décrits dans la politique publique.

## État restant à confirmer

La vérification d'identité, le jeton du portail, les identifiants de revue,
les pièces jointes et enregistrements de démonstration, les essais dans les
clients, le scan distant, les attestations et la publication ne sont pas
établis par ces fichiers. Les compléter et conserver leur preuve avant de
qualifier la soumission de prête ou le plugin de publié.

## Sources primaires

Vérifiées le 27 septembre 2026 :

- [Package portable et compatibilité](https://developers.openai.com/plugins/build/plugins)
- [Soumettre puis publier](https://developers.openai.com/plugins/deploy/submission)
- [Limites et erreurs de validation](https://developers.openai.com/plugins/deploy/submission-errors)
- [OAuth et domaines Enterprise](https://developers.openai.com/plugins/build/auth)
- [Fichiers joints et métadonnées](https://developers.openai.com/plugins/reference)
- [Conditions et données interdites](https://developers.openai.com/plugins/app-guidelines)
- [Revue du serveur MCP](https://developers.openai.com/plugins/deploy/app-review)
- [Éditeur Validature](https://validature.com/mentions-legales/)
