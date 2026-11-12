# LAB-00 – Environnement agentique

**Jalon** M0 · **Durée** ≈ 6 h · **Niveau** facile

## Objectif
Travailler avec un assistant de code agentique de façon reproductible et sûre. C'est une compétence explicitement demandée dans les offres (« AI-augmented developer », Claude Code, Copilot, Cursor).

## Prérequis
JDK 21, Node 20+, Docker, Git, compte GitHub, accès à Claude Code et/ou GitHub Copilot.

## Étapes
1. Installer et configurer l'assistant (Claude Code et/ou Copilot agent mode) dans l'éditeur et le terminal.
2. Créer dans le dépôt un fichier d'instructions (`CLAUDE.md` ou `.github/copilot-instructions.md`) : stack, conventions de code, commandes de build/test, règles « ne jamais » (secrets, données clients, modifications hors périmètre).
3. Mettre en place un workflow **spec d'abord** : écrire une spec courte (objectif, critères d'acceptation) dans un fichier, demander un plan à l'agent, relire, puis implémenter par petits commits.
4. Réaliser un mini-projet : API Spring Boot « todo » avec tests, entièrement pilotée par l'agent, avec **vous comme relecteur**.
5. Créer un workflow GitHub Actions qui compile et lance les tests.
6. Rédiger `docs/agentic-workflow.md` (dans votre dépôt de travail) : ce qui a marché, ce qui a échoué, les garde-fous que vous gardez.
7. Essayer une fois une méthode structurée (BMAD-METHOD) et noter votre avis.

## Critères d'acceptation
- [ ] Le fichier d'instructions est commité et l'agent le respecte
- [ ] Le mini-projet a ≥ 80 % de couverture sur la logique métier
- [ ] La CI est verte
- [ ] Chaque commit produit par l'agent a été relu (vous pouvez expliquer le code)
- [ ] Vous avez au moins 3 exemples où l'agent s'est trompé et comment vous l'avez détecté

## Pour aller plus loin
Brancher un serveur MCP existant dans votre assistant (préparation de [LAB-03](../lab-03-mcp-server-java/README.md)).

## Ressources
- Claude Code : <https://docs.claude.com/en/docs/claude-code/overview>
- GitHub Copilot : <https://docs.github.com/copilot>
- GitHub Actions : <https://docs.github.com/actions>
- BMAD-METHOD : rechercher « BMAD-METHOD » sur GitHub
