# LAB-00 – Environnement agentique

**Jalon** M0 · **Durée** ≈ 6 h · **Niveau** facile · **Livrable** `exercises/lab-00-agentic-workflow/` (mini-API) + fichier d'instructions + `docs/agentic-workflow.md`

## Objectif
Travailler avec un assistant de code agentique de façon **reproductible et sûre** : instructions de projet, spécification avant code, relecture systématique, CI comme filet de sécurité. C'est une compétence explicitement demandée dans les offres (« AI-augmented developer », Claude Code, Copilot, Cursor), et le mode de travail de tout le reste du plan.

Ce TP ne cherche pas à produire une belle application : il sert à **apprendre où l'agent se trompe** et à construire les garde-fous qui le détectent.

## Prérequis
JDK 21, Node 20+, Docker, Git, compte GitHub, accès à GitHub Copilot (agent mode) et/ou Claude Code. Choisir **un** outil principal pour ce TP ; le second est facultatif.

## Principe à retenir
Un fichier d'instructions **guide** le modèle, il ne **garantit** rien. Les contrôles réels restent les tests, la CI et la relecture humaine. Un bon fichier est court, spécifique et vérifié : mieux vaut 15 règles que l'agent applique que 150 qu'il ignore.

## Où mettre les instructions

| Besoin | GitHub Copilot | Claude Code |
|---|---|---|
| Instructions de projet (toujours chargées) | `.github/copilot-instructions.md` ou `AGENTS.md` | `CLAUDE.md` (lit aussi `AGENTS.md`) |
| Règles ciblées par chemin (tests, front…) | `.github/instructions/*.instructions.md` avec `applyTo: '**/*.java'` | `.claude/rules/*.md` |
| Préférences personnelles, non commitées | réglages utilisateur | `CLAUDE.local.md` (à ignorer dans `.gitignore`) |
| Rôles spécialisés | agents personnalisés (`.github/agents/`) | sous-agents (`.claude/agents/`) |

`AGENTS.md` est un format multi-outils : s'il est lu par vos deux outils, c'est le choix le plus simple pour ne pas maintenir deux copies.

## Étapes
Les durées sont indicatives : respectez-les, c'est un TP de méthode.

1. **Installer et configurer** (45 min). Assistant dans l'éditeur et le terminal. Vérifier qu'il lit bien le dépôt, qu'il peut lancer les tests, et comment il demande les autorisations (commandes, écritures de fichiers). Désactiver tout mode « tout autoriser ».
2. **Partir d'un modèle existant, ne pas écrire de zéro** (45 min). Lister, sans copier à l'aveugle :
   - le catalogue communautaire [github/awesome-copilot](https://github.com/github/awesome-copilot/tree/main/instructions), qui propose des `*.instructions.md` par techno. Pertinents pour ce plan : `springboot`, `java-junit5-assertions`, `java-mcp-server`, `python-mcp-server`, `langchain-python`, `playwright-typescript`, `github-actions-ci-cd-best-practices`, `containerization-docker-best-practices`, `kubernetes-manifests`, `terraform`, `security-and-owasp`. Vérifier si un modèle React ou Python générique existe au moment où vous le faites ;
   - la génération automatique (`/init` dans Claude Code, ou l'éditeur de personnalisations de VS Code) à partir du dépôt existant.

   Pour chaque modèle retenu, **lire, supprimer ce qui ne s'applique pas** (versions, frameworks absents, règles contradictoires) et ne garder que ce qui change le comportement de l'agent. Noter dans `docs/agentic-workflow.md` ce que vous avez retiré et pourquoi.
3. **Écrire votre fichier d'instructions racine** (45 min), en une page : stack et versions, commandes exactes de build/test/lint, conventions de code (nommage, couches, gestion d'erreurs), structure du dépôt, règles « jamais » (secrets, données clients ou d'employeur, modifications hors périmètre, suppression de tests pour « faire passer »). Ajouter, si utile, un fichier ciblé par techno (`applyTo`) reprenant un modèle de l'étape 2. Squelette :

   ```markdown
   # Instructions du projet
   ## Stack
   Java 21, Spring Boot, Maven wrapper. Données 100 % synthétiques.
   ## Commandes
   - Build + tests : `./mvnw -B verify`
   - Un seul test : `./mvnw -Dtest=NomTest test`
   ## Conventions
   - Domaine sans dépendance au framework ; erreurs HTTP au format ProblemDetail.
   - Toute modification de comportement s'accompagne d'un test.
   ## Interdits
   - Ne jamais commiter de secret ni lire `.env`.
   - Ne jamais modifier ou supprimer un test pour le faire passer.
   - Ne jamais toucher aux fichiers hors du périmètre de la spec.
   ## Avant de conclure
   Lancer build + tests et lister ce qui a été modifié.
   ```
4. **Tester que le fichier sert vraiment** (30 min). Dans une **nouvelle** conversation, sans répéter les règles dans le prompt, demander une petite tâche où elles comptent (ex. ajouter un endpoint). Vérifier : le fichier est-il cité dans les références ? Les conventions et la commande de test sont-elles respectées ? Refaire la même tâche **sans** le fichier et noter l'écart. Corriger ou supprimer les règles ignorées.
5. **Workflow spec d'abord** (30 min). Dans `specs/`, écrire pour la tâche une spec courte : objectif, règles métier, cas limites, critères d'acceptation vérifiables, hors périmètre. Demander un **plan** à l'agent, le relire et le corriger **avant** toute écriture de code, puis implémenter par petits commits (un comportement = un commit avec ses tests).
6. **Mini-projet piloté par l'agent** (1 h 30). API Spring Boot « tâches de conformité » (spec ci-dessous), tests de service et d'API, couverture JaCoCo. **Vous êtes le relecteur** : lire chaque diff, poser des questions sur ce que vous ne comprenez pas, refuser ce qui sort du périmètre. À chaque erreur de l'agent, la consigner dans le tableau d'incidents (voir plus bas).
7. **CI** (30 min). Workflow GitHub Actions (`.github/workflows/ci.yml`) : JDK 21, cache Maven, `./mvnw -B verify`, publication du rapport de couverture. Faire échouer volontairement la CI (test cassé) pour vérifier qu'elle bloque.
8. **Rôles et points d'arrêt humains** (30 min). Définir dans le fichier d'instructions (ou en agents personnalisés) des rôles invoqués tour à tour : architecte, développeur, QA, sécurité, relecteur. Pour chacun : fichiers modifiables, fichiers interdits, sortie attendue. Fixer les **validations obligatoires** (build, tests, lint) et les **arrêts humains** avant toute opération sensible : suppression, publication, secrets, changement de dépendances, de CI ou de schéma. Aucune modification n'est validée sans tests exécutés et relecture.
9. **Rétrospective** (15 min). Rédiger `docs/agentic-workflow.md` : ce qui a marché, ce qui a échoué, tableau d'incidents, garde-fous conservés, règles ajoutées au fichier d'instructions après coup.

## Spec du mini-projet : tâches de conformité
Volontairement piégeuse : ces règles métier sont celles où un agent a tendance à improviser.

- Une tâche : `id`, `title` (3 à 120 caractères), `dueDate`, `status`.
- Création : `dueDate` ne peut pas être dans le passé ; statut initial `OPEN`.
- Transitions autorisées : `OPEN → IN_PROGRESS → DONE`, et `OPEN` ou `IN_PROGRESS → CANCELLED`. `DONE` et `CANCELLED` sont **définitifs** ; toute autre transition est refusée (409).
- `GET /tasks?status=` avec pagination ; `PATCH /tasks/{id}/status` ; `POST /tasks`.
- Erreurs au format ProblemDetail (400 validation, 404, 409 transition invalide), jamais de stack trace.
- Hors périmètre : authentification, base externe (H2 ou mémoire suffit).

## Tableau d'incidents (à tenir pendant le TP)

| # | Ce que l'agent a fait | Comment je l'ai détecté (test, relecture, CI) | Correction | Règle ajoutée aux instructions ? |
|---|---|---|---|---|

Familles d'erreurs à guetter : règle métier inventée ou oubliée, test écrit pour valider le code plutôt que la spec, dépendance ou API qui n'existe pas, modification hors périmètre, secret ou donnée réelle injectée, « tout est vert » annoncé sans avoir lancé les tests.

## Critères d'acceptation
- [ ] Le fichier d'instructions est commité, tient en une page et a été testé avec/sans (écart noté)
- [ ] Les modèles réutilisés ont été relus et élagués, leur provenance est notée
- [ ] La spec et le plan relu précèdent le code ; l'historique Git montre de petits commits
- [ ] Le mini-projet a ≥ 80 % de couverture sur la logique métier, y compris les transitions interdites
- [ ] La CI est verte, et a été vue rouge une fois (échec volontaire)
- [ ] Chaque commit produit par l'agent a été relu (vous pouvez expliquer le code)
- [ ] Le tableau d'incidents contient ≥ 3 erreurs de l'agent avec leur mode de détection
- [ ] Rôles, validations obligatoires et points d'arrêt humains sont définis dans le fichier d'instructions

## Pour aller plus loin
- Essayer une fois une méthode structurée de développement piloté par spec ([BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD)) sur une nouvelle fonctionnalité et noter votre avis : gain, lourdeur, cas où elle vaut le coût.
- Brancher un serveur MCP existant dans votre assistant (préparation de [LAB-03](../lab-03-mcp-server-java/README.md)).
- Ajouter un contrôle de CI qui signale tout commit modifiant à la fois un test et le code testé, pour relecture renforcée.

## Ressources
- Instructions dans VS Code : <https://code.visualstudio.com/docs/agent-customization/custom-instructions>
- Instructions de dépôt GitHub Copilot : <https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/add-custom-instructions/add-repository-instructions>
- Claude Code : <https://code.claude.com/docs/en/overview> · mémoire et `CLAUDE.md` : <https://code.claude.com/docs/en/memory>
- Format `AGENTS.md` : <https://agents.md>
- Modèles d'instructions par techno : <https://github.com/github/awesome-copilot/tree/main/instructions>
- GitHub Actions : <https://docs.github.com/actions>
- BMAD-METHOD : <https://github.com/bmad-code-org/BMAD-METHOD>
