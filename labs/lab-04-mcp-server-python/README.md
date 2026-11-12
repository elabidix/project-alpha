# LAB-04 – Serveur MCP en Python : alertes de conformité

**Jalon** M1 · **Durée** ≈ 7 h · **Niveau** moyen · **Livrable** `agentgate/mcp-alerts/`

## Objectif
Construire un second serveur MCP en Python (FastMCP) pour le workflow des alertes issues du screening, et comparer les deux écosystèmes. La décision finale reste humaine : l'outil de décision est protégé.

## Prérequis
LAB-01, LAB-03.

## Étapes
1. Créer `mcp-alerts` avec `uv` et FastMCP.
2. Modéliser une alerte avec des statuts `NEW`, `ASSIGNED`, `UNDER_INVESTIGATION`, `PENDING_APPROVAL`, `CONFIRMED_MATCH`, `FALSE_POSITIVE`, `CLOSED` et des transitions autorisées (une transition invalide est refusée).
3. Outils **lecture** : `getAlert(id)`, `listAlerts(status)`, `getAlertHistory(id)`. Outils **écriture sans décision** : `addComment(alertId, text)`, `proposeDecision(alertId, decision, justification)` qui met l'alerte en `PENDING_APPROVAL` mais ne la clôture jamais.
4. Outil **sensible** `recordDecision(alertId, decision, justification, approvedBy)` : refuse tout appel venant d'un agent ; il exige un paramètre `approvedBy` issu d'une approbation humaine (la vérification complète viendra du plan de contrôle, [LAB-05](../lab-05-control-plane/README.md)). Marquer clairement l'effet de bord dans sa description.
5. Valider les paramètres avec Pydantic ; persister en SQLite ou PostgreSQL ; chaque action écrit une ligne d'historique.
6. Tester avec Inspector et via l'assistant ; écrire des tests pytest sur les outils et les transitions.
7. Exposer en transport HTTP ; ajouter un `/health`.
8. Produire `docs/mcp-java-vs-python.md` : lignes de code, temps de démarrage, expérience de debug, choix recommandé selon le contexte.

## Critères d'acceptation
- [ ] Les deux serveurs (Java et Python) fonctionnent ensemble dans un même assistant
- [ ] Une transition de statut invalide est refusée (test)
- [ ] `proposeDecision` ne peut jamais clôturer une alerte ; `recordDecision` refuse un appel sans approbation humaine (test)
- [ ] Tests pytest verts ; image Docker construite

## Pour aller plus loin
Écrire un scénario de test d'**empoisonnement d'outil** : une description d'outil malveillante qui tente de détourner l'agent (réutilisé dans [LAB-11](../lab-11-guardrails/README.md)).

## Ressources
- FastMCP : <https://gofastmcp.com> · MCP : <https://modelcontextprotocol.io>
- OWASP LLM Top 10 : <https://genai.owasp.org/llm-top-10/>
