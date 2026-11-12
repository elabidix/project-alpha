# LAB-09 – Agent LangGraph avec validation humaine

**Jalon** M2 · **Durée** ≈ 24 h · **Niveau** avancé · **Livrable** `agentgate/agent-runtime/`

## Objectif
Construire un agent qui assiste un analyste sur une alerte de conformité : il explique la correspondance, prépare l'investigation et **propose** une décision en appelant les outils MCP via la passerelle. Il **s'arrête pour validation humaine** avant toute action sensible et **ne prend jamais la décision réglementaire finale**. C'est le cœur des offres « agentic AI ».

## Prérequis
LAB-04, LAB-06, LAB-08. Notions de graphes d'états.

## Étapes
1. Initialiser `agent-runtime` (Python, FastAPI, **LangGraph**).
2. Définir le graphe : `comprendre l'alerte` → `screening et explication` (outils `mcp-screening`) → `analyser l'historique` (outils `mcp-alerts`) → `proposer une décision` (`proposeDecision`) → `contrôle qualité` (chaque affirmation cite une source ; faits, hypothèses et recommandations sont distingués ; informations manquantes signalées) → `[validation humaine]`. La décision finale est enregistrée par un humain, pas par l'agent.
3. Brancher les outils MCP **via la passerelle** (jamais en direct) avec le jeton de l'agent.
4. **Validation humaine** : utiliser les points d'interruption de LangGraph ; l'agent publie une demande d'approbation (API + console), puis reprend après décision.
5. **Persistance d'état** (checkpointer PostgreSQL) : un redémarrage du service ne perd pas les dossiers en cours.
6. **Robustesse** : limites d'étapes et de budget de tokens, reprise sur erreur d'outil, détection de boucle, sortie structurée validée.
7. Tests : scénarios déterministes avec un faux LLM, puis scénarios réels notés (voir [LAB-12](../lab-12-evals-ci/README.md)).
8. Comparer en une page à une variante simple « un seul appel + outils » : quand le graphe vaut-il le coût ?

## Critères d'acceptation
- [ ] ADR-0006 rédigé (exécution durable et reprise : pourquoi un graphe avec persistance plutôt qu'un simple appel) : [gabarit](../../docs/adr/README.md)
- [ ] ADR-0011 rédigé (séparation moteur déterministe / assistant IA : aucune décision réglementaire automatisée)
- [ ] Aucun test ne permet à l'agent d'appeler `recordDecision` (le plan de contrôle le refuse)
- [ ] L'action sensible n'est jamais exécutée sans approbation (test automatisé)
- [ ] Le service redémarré reprend un dossier en attente
- [ ] Une boucle infinie provoquée volontairement est stoppée par les limites
- [ ] Les appels d'outils passent tous par la passerelle (visible dans l'audit)

## Pour aller plus loin
Deuxième agent (contrôle qualité) et coordination multi-agents ; protocole A2A en bonus.

## Ressources
- DDIA : ch. 5 *Durable Execution and Workflows* (c'est le modèle derrière la persistance d'état et la reprise de LangGraph) ; ch. 8 *Exactly-Once Message Processing Revisited*. Une reprise ne doit pas exécuter deux fois une action sensible : clé d'idempotence par action
- LangGraph : <https://langchain-ai.github.io/langgraph/> (concepts, persistance, human-in-the-loop)
- MCP : <https://modelcontextprotocol.io>
- Cours courts DeepLearning.AI sur les agents : <https://www.deeplearning.ai/short-courses/>
