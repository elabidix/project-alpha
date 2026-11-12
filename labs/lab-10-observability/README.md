# LAB-10 – Observabilité LLM (Langfuse et OpenTelemetry)

**Jalon** M2 · **Durée** ≈ 12 h · **Niveau** moyen · **Livrable** `agentgate/deploy/observability/`

## Objectif
Voir ce que font les agents : traces de bout en bout, coûts, latences, erreurs. L'observabilité et l'évaluation figurent dans 41 % des annonces Java + IA.

## Prérequis
LAB-06, LAB-08, LAB-09.

## Étapes
1. Démarrer **Langfuse** en local (Docker) via le `docker-compose`.
2. Instrumenter le runtime Python : une trace par dossier, un span par étape de graphe et par appel d'outil, avec tokens et coût.
3. Instrumenter les services Java (passerelle, plan de contrôle, RAG) avec l'agent **OpenTelemetry** ; propager l'identifiant de corrélation (W3C Trace Context) à travers les appels HTTP et Kafka.
4. Envoyer les traces techniques vers un collecteur OTel (Jaeger ou Tempo) et les traces LLM vers Langfuse.
5. Dashboards : coût par tenant et par agent, latence p95, taux d'erreur par outil.
6. Alertes simples : taux d'erreur d'outil > seuil ; coût journalier > budget.
7. Masquage : vérifier qu'aucune donnée personnelle ne part dans les traces.

## Critères d'acceptation
- [ ] Un dossier unique est visible de la console jusqu'à l'outil MCP dans une seule trace
- [ ] Le coût par agent et par tenant est affiché
- [ ] Une panne injectée d'un outil déclenche l'alerte
- [ ] Un test vérifie l'absence de PII dans les traces

## Pour aller plus loin
Annotations humaines dans Langfuse alimentant le jeu d'évaluation ([LAB-12](../lab-12-evals-ci/README.md)).

## Ressources
- Langfuse : <https://langfuse.com/docs> · OpenTelemetry Java : <https://opentelemetry.io/docs/languages/java/>
