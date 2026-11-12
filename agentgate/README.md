# AgentGate

Plan de contrôle et passerelle open source pour déployer des agents IA et des outils MCP en entreprise régulée : catalogue, droits, garde-fous, évaluation continue, coûts, audit.

Ce dossier reste vide jusqu'au jalon **M1**. Les TP des `labs/` produisent chacun un composant à placer ici. Le suivi d'avancement est dans [../ROADMAP.md](../ROADMAP.md).

## Architecture cible

| Brique | Dossier | Techno | TP |
|---|---|---|---|
| Outil MCP d'exemple (contrats) | `mcp-contracts/` | Java 21, Spring AI MCP | [lab-03](../labs/lab-03-mcp-server-java/README.md) |
| Outil MCP d'exemple (sinistres) | `mcp-claims/` | Python, FastMCP | [lab-04](../labs/lab-04-mcp-server-python/README.md) |
| Plan de contrôle | `control-plane/` | Spring Boot, hexagonal, PostgreSQL, Spring Authorization Server | [lab-05](../labs/lab-05-control-plane/README.md) |
| Passerelle | `gateway/` | Spring Cloud Gateway | [lab-06](../labs/lab-06-mcp-gateway/README.md) |
| Console | `console/` | React, TypeScript | [lab-07](../labs/lab-07-react-console/README.md) |
| Application RAG | `rag-app/` | Spring AI, pgvector, Kafka | [lab-08](../labs/lab-08-rag-spring-ai/README.md) |
| Runtime d'agents | `agent-runtime/` | Python, LangGraph | [lab-09](../labs/lab-09-agent-langgraph/README.md) |
| Évaluation | `evals/` | promptfoo / DeepEval | [lab-12](../labs/lab-12-evals-ci/README.md) |
| Déploiement | `deploy/` | Helm, Terraform | [lab-14](../labs/lab-14-kubernetes-helm/README.md) |

## Licence

Prévue : Apache-2.0 (à ajouter avant la première publication publique).
