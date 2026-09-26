# Distribution Claude et vérification commune

Procédure vérifiée le 27 septembre 2026. Le portail officiel est
[claude.ai/directory/manage](https://claude.ai/directory/manage).
Une marketplace GitHub permet l'installation directe ; elle ne constitue pas
une inscription dans l'annuaire Anthropic.

## Deux soumissions pour Validature

Soumettre d'abord le serveur comme **MCP connector**, puis le dossier du
plugin comme **Plugin bundle**, depuis la même organisation Claude. Le bundle
doit référencer exactement la même URL MCP pour permettre leur association et
éviter deux jeux d'outils. Le connecteur apporte sa fiche, sa configuration
d'authentification et son tableau de bord ; le bundle ajoute les quatre skills.
Il n'existe pas de demande séparée « Claude Marketplace ».
[Procédure officielle](https://claude.com/docs/directory/publish).

Le compte doit disposer de Pro, Max, Team ou Enterprise. Sur Team/Enterprise,
il faut être Owner ; Enterprise permet aussi un rôle doté de la permission
Directory. Choisir l'organisation qui détiendra durablement la fiche : la
première soumission réserve ce couple dépôt/dossier. Pour le bundle, connecter
un compte GitHub ayant le droit de pousser dans le dépôt ; le dépôt doit être
public au lancement. Ne pas soumettre une copie depuis un compte personnel
si la fiche doit appartenir à l'organisation.
[Accès et dépôt](https://claude.com/docs/plugins/submit).

## Matériel à préparer

| Champ | Valeur ou action |
| --- | --- |
| Nom | Validature |
| Accroche | Documents à signer, modèles réutilisables, suivi et parcours Vault sécurisé. |
| Dépôt | `https://github.com/blackjackparis/validature-plugins` |
| Dossier du plugin | `validature` — pas la racine de la marketplace |
| Branche suivie | `main`, après fusion de la version testée dans le miroir |
| Serveur MCP | `https://validature.app/api/v1/mcp` |
| Authentification | OAuth 2.0 public, DCR et PKCE ; connexion individuelle au compte Validature |
| Documentation publique | README du dossier `validature/` dans le miroir, après publication |
| Confidentialité et conditions | `https://validature.app/privacy` et `https://validature.app/terms` |
| Assistance produit | `contact@validature.com` — confirmer sa réception avant soumission |
| Contact légal et sécurité publié | `contact@logiks.fr` |
| Icône | Asset Validature `openai/validature/assets/icon.svg`, à fournir au portail |

Le dossier du plugin contient son propre README d'au moins 40 mots hors blocs
de code et sa licence. Le README décrit aussi les données envoyées, les
destinations et les limites Vault. Le validateur CLI ne remplace pas les
contrôles d'annuaire du bouton **Validate**.
[Checklist plugin](https://claude.com/docs/plugins/pre-submission-checklist).

Validature fournit actuellement des outils et des liens navigateur, sans
interface MCP App intégrée. Le carrousel n'est donc pas requis pour ce package.
Si une MCP App est ajoutée, préparer 3 à 5 PNG d'au moins 1 000 px de large,
cadrés sur sa réponse, avec les prompts fournis séparément ; pas de vidéo/GIF.
[Matériel connecteur](https://claude.com/docs/connectors/building/submission).

## Compte de revue

Fournir dans les champs privés du portail un compte dédié, pleinement alimenté
en données fictives, sur une offre autorisant les fonctionnalités testées :
PDF et Word standards, modèles NDA/Devis/Bail, collègue de test, demande en
cours, demande terminée avec documents signés et accès Vault effectivement
activé. Utiliser des boîtes email contrôlées et donner les étapes de connexion.
Ne placer aucun identifiant dans Git et ne désactiver aucun contrôle des
comptes réels. La revue exige des identifiants utilisables et une documentation
publique au plus tard à la publication.
[Checklist connecteur](https://claude.com/docs/connectors/building/review-criteria).

## Déroulé dans le portail

1. **MCP connector** : connecter l'URL, synchroniser les outils, compléter la
   fiche, les cas d'usage, la société, OAuth, le traitement des données et les
   accès de test. Confirmer uniquement les vérifications réellement effectuées
   et les engagements applicables, puis relire et soumettre. Un connecteur
   reçoit généralement le statut Community après scan ; Verified relève de
   la sélection d'Anthropic, sans demande séparée.
   [Soumettre le connecteur](https://claude.com/docs/connectors/building/submission).
2. **Plugin bundle** : renseigner dépôt, dossier `validature` et branche,
   sélectionner **Validate**, corriger chaque blocage puis **Re-validate**
   après tout nouveau commit. Vérifier la fiche issue du manifeste/README,
   répondre sur les données, confirmer les contacts et engagements, choisir
   le suivi des versions puis **Submit for review**. Le webhook GitHub est
   facultatif et exige un accès administrateur au dépôt ; le suivi planifié
   reste possible. Associer les fiches depuis la même organisation.
   [Soumettre le plugin](https://claude.com/docs/plugins/submit).
3. Suivre les retours et l'état de chaque soumission. Le bundle reçoit une
   validation et un scan par version ; une première fiche passe aussi par un
   relecteur. Ne pas annoncer de délai garanti ni de publication sur la seule
   base d'une PR fusionnée. Choisir explicitement le mode de publication des
   nouvelles versions et vérifier la version effectivement visible.
   [Revue et publication](https://claude.com/docs/directory/publish).

En cas de dossier existant, le reprendre au lieu d'en créer un doublon.
Pour les difficultés de soumission : `directory@anthropic.com` pour les plugins
et `mcp-review@anthropic.com` pour les connecteurs, selon leurs guides officiels.

## Vérification avant les deux soumissions

Depuis `plugins/`, exécuter `claude plugin validate validature` et
`claude plugin validate .`, puis utiliser **Validate** sur le dossier plugin
dans le portail. Tester chaque outil avec MCP Inspector et dans Claude comme
connecteur personnalisé. Tester aussi le bundle sur les surfaces annoncées :
ses skills se chargent dans chat, Cowork et Claude Code ; dans chat/Cowork,
connecter le serveur depuis l'onglet **Connectors** du plugin.
[Chargement par surface](https://claude.com/docs/plugins/platform-support).

| Parcours | Résultat à constater |
| --- | --- |
| Dépôt standard | Le fichier choisi est reçu et analysé ; l'assistant récupère le bon `documentId` |
| Modèle | Création, lecture, remplacement des champs, duplication et réutilisation sans déplacer les champs |
| Partage | Accès du collègue conforme, puis refus après révocation |
| Envoi | Brouillon relu ; après accord, invitation reçue dans la boîte de test ; pas de doublon après retry |
| Suivi | Statuts, relance autorisée et annulation cohérents avec l'application |
| Vault | Chiffrement et envoi dans le navigateur ; aucune identité, clé ou contenu dans le résultat MCP |
| Documents signés | PDF, certificat et ZIP utilisables pour une demande terminée |
| OAuth | Connexion, nouveaux scopes, refresh et révocation ; anciens appels et liens refusés après révocation |

Conserver date, SHA backend, SHA du miroir, version, client et observations.
Un test unitaire ou un validateur JSON ne prouve pas ces parcours dans Claude.
Ne confirmer aucun test non exécuté dans le portail.

Les [conditions de l'annuaire](https://support.claude.com/en/articles/13145338-anthropic-software-directory-terms)
et sa [politique](https://support.claude.com/en/articles/13145358-anthropic-software-directory-policy)
restent applicables. Les permissions doivent être limitées à l'action voulue,
les descriptions conformes au comportement livré, et les contacts/confidentialité
à jour. Le dépôt standard porte sur le fichier sélectionné pour cette action ;
il ne doit pas aspirer l'historique ou des fichiers sans rapport avec la demande.
