# LAB-09 – Agent LangGraph avec validation humaine

**Jalon** M2 · **Durée** ≈ 24 h · **Niveau** avancé · **Livrable** `agentgate/agent-runtime/`

## Objectif
Construire un agent qui traite un dossier de sinistre en appelant les outils MCP via la passerelle, et **s'arrête pour validation humaine** avant toute action sensible. C'est le cœur des offres « agentic AI ».

## Prérequis
LAB-04, LAB-06, LAB-08. Notions de graphes d'états.

## Étapes
1. Initialiser `agent-runtime` (Python, FastAPI, **LangGraph**).
2. Définir le graphe : `comprendre la demande` → `rechercher le contrat` → `analyser le sinistre` → `proposer une décision` → `[validation humaine]` → `exécuter`.
3. Brancher les outils MCP **via la passerelle** (jamais en direct) avec le jeton de l'agent.
4. **Validation humaine** : utiliser les points d'interruption de LangGraph ; l'agent publie une demande d'approbation (API + console), puis reprend après décision.
5. **Persistance d'état** (checkpointer PostgreSQL) : un redémarrage du service ne perd pas les dossiers en cours.
6. **Robustesse** : limites d'étapes et de budget de tokens, reprise sur erreur d'outil, détection de boucle, sortie structurée validée.
7. Tests : scénarios déterministes avec un faux LLM, puis scénarios réels notés (voir [LAB-12](../lab-12-evals-ci/README.md)).
8. Comparer en une page à une variante simple « un seul appel + outils » : quand le graphe vaut-il le coût ?

## Critères d'acceptation
- [ ] L'action sensible n'est jamais exécutée sans approbation (test automatisé)
- [ ] Le service redémarré reprend un dossier en attente
- [ ] Une boucle infinie provoquée volontairement est stoppée par les limites
- [ ] Les appels d'outils passent tous par la passerelle (visible dans l'audit)

## Pour aller plus loin
Deuxième agent (contrôle qualité) et coordination multi-agents ; protocole A2A en bonus.

## Ressources
- LangGraph : <https://langchain-ai.github.io/langgraph/> (concepts, persistance, human-in-the-loop)
- MCP : <https://modelcontextprotocol.io>
- Cours courts DeepLearning.AI sur les agents : <https://www.deeplearning.ai/short-courses/>
