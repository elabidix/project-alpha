# AgentGate

Plan de contrôle et passerelle open source pour déployer des agents IA et des outils MCP en entreprise régulée : catalogue, droits, garde-fous, évaluation continue, coûts, audit.

Ce dossier reste vide jusqu'au jalon **M1**. Les TP des `labs/` produisent chacun un composant à placer ici. Le suivi d'avancement est dans [../ROADMAP.md](../ROADMAP.md).

## Architecture cible

| Brique | Dossier | Techno | TP |
|---|---|---|---|
| Outil MCP d'exemple (screening) | `mcp-screening/` | Java 21, Spring AI MCP | [lab-03](../labs/lab-03-mcp-server-java/README.md) |
| Outil MCP d'exemple (alertes) | `mcp-alerts/` | Python, FastMCP | [lab-04](../labs/lab-04-mcp-server-python/README.md) |
| Plan de contrôle | `control-plane/` | Spring Boot, hexagonal, PostgreSQL, Spring Authorization Server | [lab-05](../labs/lab-05-control-plane/README.md) |
| Passerelle | `gateway/` | Spring Cloud Gateway | [lab-06](../labs/lab-06-mcp-gateway/README.md) |
| Console | `console/` | React, TypeScript | [lab-07](../labs/lab-07-react-console/README.md) |
| Application RAG | `rag-app/` | Spring AI, pgvector, Kafka | [lab-08](../labs/lab-08-rag-spring-ai/README.md), [lab-18](../labs/lab-18-reliable-events/README.md) |
| Runtime d'agents | `agent-runtime/` | Python, LangGraph | [lab-09](../labs/lab-09-agent-langgraph/README.md) |
| Évaluation | `evals/` | promptfoo / DeepEval | [lab-12](../labs/lab-12-evals-ci/README.md) |
| Déploiement | `deploy/` | Helm, Terraform | [lab-14](../labs/lab-14-kubernetes-helm/README.md) |
| Étude de cas legacy | `case-study-legacy/` | Java, Spring Batch (hors pile AgentGate) | [lab-16](../labs/lab-16-legacy-modernization/README.md) |

Les mini-projets du jalon M0 (LAB-00 à 02) ne sont pas des composants d'AgentGate : ils vivent dans `exercises/` à la racine du dépôt. Détail du parcours : [labs/README.md](../labs/README.md).

## Cas d'usage de démonstration : conformité bancaire (ComplyFlow-lite)

AgentGate est la plateforme **horizontale** (gouvernance des agents et des outils MCP). Pour la démontrer, on l'applique à un cas **vertical** réduit : l'aide à l'analyse des alertes de screening bancaire.

Principe fondateur : **un moteur déterministe calcule, l'IA explique et assiste, un humain décide**. Aucun agent ne prend de décision réglementaire finale ; le plan de contrôle l'impose.

Volume volontairement réduit : un service de screening (Java), un service d'alertes (Python), un agent d'investigation avec contrôle qualité. Ce n'est pas une plateforme de conformité complète.

### Scénarios de démonstration

| | Scénario | Ce qu'il prouve |
|---|---|---|
| A | Client sans correspondance : le screening ne crée pas d'alerte | Moteur déterministe |
| B | Nom proche d'une entrée de liste : alerte créée avec score explicable | Explicabilité du moteur |
| C | L'analyste demande à l'agent d'expliquer l'alerte : rapport avec références | RAG, agent, citations |
| D | L'analyste classe un faux positif avec justification | Décision humaine tracée |
| E | Un superviseur valide une décision à seconde approbation | Approbation humaine imposée par la passerelle |
| F | Injection d'instruction dans un commentaire d'alerte : bloquée et auditée | Garde-fous |

## Cadre et confidentialité

- **Données 100 % synthétiques.** Aucune liste, donnée client ou règle réelle.
- **Aucune reprise d'un employeur ou client** : ni code, ni spécification, ni jeu de données, ni règles métier propres. Vérifiez votre clause de confidentialité et de propriété intellectuelle avant de publier le dépôt.
- L'application de démonstration reste un prétexte : l'angle de valeur est la **gouvernance, l'évaluation et la sécurité** des agents.

## Hors périmètre (volontairement)

Pour tenir en ≈ 500 heures, on n'ajoute pas : RabbitMQ (Kafka couvre le besoin et pèse plus dans les annonces), OpenSearch, Redis, MinIO, Argo CD, SonarQube, ni une architecture multi-agents à 6 rôles. Une brique n'entre que si un ADR en démontre le besoin.

## Licence

Prévue : Apache-2.0 (à ajouter avant la première publication publique).
