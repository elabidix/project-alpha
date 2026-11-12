# LAB-07 – Console React

**Jalon** M1 · **Durée** ≈ 12 h · **Niveau** moyen · **Livrable** `agentgate/console/`

## Objectif
Offrir une interface d'administration claire : catalogue des outils MCP et agents, journal d'audit, file d'approbation. C'est la partie visible de la démo.

## Prérequis
LAB-05, LAB-06. Notions React/TypeScript.

## Étapes
1. Créer le projet **Vite + React + TypeScript** ; client d'API généré depuis l'OpenAPI du plan de contrôle.
2. Authentification OIDC (code + PKCE) ; routage protégé selon les rôles.
3. Pages : **Catalogue** (liste, détail, statut de connectivité), **Politiques** (matrice agent × outil), **Audit** (filtres, pagination, export CSV).
4. Gestion des données avec **TanStack Query** (cache, états de chargement et d'erreur propres).
5. Tests composants (Testing Library) et un test de bout en bout **Playwright** sur le parcours « enregistrer un serveur MCP ».
6. Accessibilité de base (clavier, contrastes) et responsive.
7. Containeriser (nginx) et l'ajouter au `docker-compose`.

## Critères d'acceptation
- [ ] Parcours complet : connexion → enregistrer un serveur → créer une politique → voir l'audit de l'appel
- [ ] Un auditeur ne voit pas les boutons de modification
- [ ] Test Playwright vert en CI ; score Lighthouse accessibilité ≥ 90
- [ ] Aucune clé ni jeton stocké dans le code

## Pour aller plus loin
Page « Approbations » alimentée par l'agent du [LAB-09](../lab-09-agent-langgraph/README.md).

## Ressources
- React : <https://react.dev> · Vite : <https://vite.dev> · TanStack Query : <https://tanstack.com/query>
- Playwright : <https://playwright.dev>
