# Travaux pratiques (labs)

Chaque TP produit un composant testé, documenté et reproductible. Le suivi d'avancement se fait **uniquement** dans [../ROADMAP.md](../ROADMAP.md) : les cases des critères d'acceptation ci-dessous servent à vérifier le TP, pas à suivre la progression.

## Parcours

| TP | Sujet | Jalon | Durée | Prérequis | Livrable |
|---|---|---|---|---|---|
| [00](./lab-00-agentic-workflow/README.md) | Environnement agentique | M0 | 6 h | n/a | `exercises/` + instructions d'agent |
| [01](./lab-01-python-for-java-devs/README.md) | Python pour développeurs Java | M0 | 8 h | 00 | `exercises/` |
| [02](./lab-02-llm-api-basics/README.md) | Bases des API LLM | M0 | 6 h | 01 | `exercises/` |
| [03](./lab-03-mcp-server-java/README.md) | Serveur MCP Java (screening) | M1 | 10 h | 00-02 | `agentgate/mcp-screening/` |
| [04](./lab-04-mcp-server-python/README.md) | Serveur MCP Python (alertes) | M1 | 7 h | 01, 03 | `agentgate/mcp-alerts/` |
| [05](./lab-05-control-plane/README.md) | Plan de contrôle hexagonal | M1 | 20 h | 03, 04 | `agentgate/control-plane/` |
| [06](./lab-06-mcp-gateway/README.md) | Passerelle MCP avec audit | M1 | 14 h | 03-05 | `agentgate/gateway/` |
| [07](./lab-07-react-console/README.md) | Console React | M1 | 12 h | 05, 06 | `agentgate/console/` |
| [08](./lab-08-rag-spring-ai/README.md) | RAG Spring AI et pgvector | M2 | 20 h | 02, 05 | `agentgate/rag-app/` |
| [09](./lab-09-agent-langgraph/README.md) | Agent LangGraph, validation humaine | M2 | 24 h | 04, 06, 08 | `agentgate/agent-runtime/` |
| [10](./lab-10-observability/README.md) | Observabilité LLM | M2 | 12 h | 06, 08, 09 | `agentgate/deploy/observability/` |
| [18](./lab-18-reliable-events/README.md) | Fiabilité des événements | M2 | 10 h | 05, 08 | `control-plane/` + `rag-app/` |
| [11](./lab-11-guardrails/README.md) | Garde-fous et sécurité IA | M3 | 20 h | 04, 06, 09 | `gateway/` + `evals/security/` |
| [12](./lab-12-evals-ci/README.md) | Évaluation continue en CI | M3 | 16 h | 08-10 | `agentgate/evals/` |
| [13](./lab-13-model-routing/README.md) | Routage de modèles, quotas | M3 | 12 h | 02, 06, 10 | `gateway/` + `deploy/litellm/` |
| [14](./lab-14-kubernetes-helm/README.md) | Kubernetes et Helm | M4 | 24 h | 06-13 | `agentgate/deploy/helm/` |
| [15](./lab-15-terraform/README.md) | Terraform (optionnel) | M4 | 10 h | 14 | `agentgate/deploy/terraform/` |
| [16](./lab-16-legacy-modernization/README.md) | Modernisation legacy assistée par IA | M4 | 24 h | 00, 05 | `agentgate/case-study-legacy/` |
| [17](./lab-17-multitenancy-sso/README.md) | Multi-tenant et SSO | M4 | 14 h | 05-07, 14 | `control-plane/` + `deploy/keycloak/` |

L'ordre de la feuille de route fait foi ; la numérotation 18 reste à la fin pour ne pas renuméroter les liens existants.

## Où va le code

- **M0 (LAB-00 à 02)** : mini-projets dans `exercises/lab-NN-nom/` à la racine de ce dépôt, un dossier par TP, chacun avec son README et sa CI.
- **M1 et au-delà** : directement dans [../agentgate/](../agentgate/README.md), dans le dossier indiqué par le livrable.

## Structure d'un TP

Chaque README suit le même plan : *Objectif* → *Prérequis* → *Étapes* → *Critères d'acceptation* → *Pour aller plus loin* → *Ressources*. Les critères d'acceptation sont **vérifiables** (test, mesure, démonstration) ; si un critère ne l'est pas, le reformuler plutôt que le valider « à l'œil ».

## Règles communes

1. **Spec d'abord** : une spec courte et un plan relu avant de laisser l'agent écrire du code ([LAB-00](./lab-00-agentic-workflow/README.md)).
2. **Relecture humaine** de tout ce que produit l'agent ; vous devez pouvoir l'expliquer.
3. **Données 100 % synthétiques**, jamais de code, données ou règles d'un employeur ou d'un client.
4. **Aucun secret** dans Git ; `.env` est ignoré.
5. **Un ADR par TP concerné**, écrit avant ou pendant l'implémentation ([gabarit](../docs/adr/README.md)).
6. **Mesurer** : un gain, un score ou un coût annoncé doit être accompagné de sa méthode de mesure et d'un résultat reproductible.
7. **Journaliser vos échecs** (erreurs de l'agent, pannes, mauvais choix) : ils nourrissent les articles et les ADR.

## Évaluer un TP terminé

- Tous les critères d'acceptation sont satisfaits, preuves à l'appui (lien vers test, rapport ou capture).
- La CI du composant est verte et reproductible depuis un clone neuf (`docker compose up` ou la commande documentée).
- Le README du composant dit comment le lancer, le tester et ce qu'il ne fait pas.
- Seulement alors, cocher la case du TP dans [../ROADMAP.md](../ROADMAP.md).
