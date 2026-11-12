# LAB-04 – Serveur MCP en Python

**Jalon** M1 · **Durée** ≈ 6 h · **Niveau** moyen · **Livrable** `agentgate/mcp-claims/`

## Objectif
Construire un second serveur MCP en Python (FastMCP) pour la gestion des sinistres, et comparer les deux écosystèmes.

## Prérequis
LAB-01, LAB-03.

## Étapes
1. Créer `mcp-claims` avec `uv` et FastMCP.
2. Outils : `createClaim(contractId, description)`, `getClaimStatus(id)`, `escalateClaim(id, reason)` ; ce dernier est **sensible** (marquer clairement l'effet de bord dans sa description).
3. Valider les paramètres avec Pydantic et limiter les droits : `escalateClaim` doit exiger un paramètre `confirmed=true` fourni par l'appelant humain.
4. Persister en SQLite ou PostgreSQL, données synthétiques.
5. Tester avec Inspector et via l'assistant ; écrire des tests pytest sur les outils.
6. Exposer en transport HTTP ; ajouter un `/health`.
7. Produire `docs/mcp-java-vs-python.md` : lignes de code, temps de démarrage, expérience de debug, choix recommandé selon le contexte.

## Critères d'acceptation
- [ ] Les deux serveurs (Java et Python) fonctionnent ensemble dans un même assistant
- [ ] L'outil sensible refuse de s'exécuter sans confirmation
- [ ] Tests pytest verts ; image Docker construite

## Pour aller plus loin
Écrire un scénario de test d'**empoisonnement d'outil** : une description d'outil malveillante qui tente de détourner l'agent (réutilisé dans [LAB-11](../lab-11-guardrails/README.md)).

## Ressources
- FastMCP : <https://gofastmcp.com> · MCP : <https://modelcontextprotocol.io>
- OWASP LLM Top 10 : <https://genai.owasp.org/llm-top-10/>
