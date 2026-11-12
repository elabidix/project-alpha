# LAB-06 – Passerelle MCP avec audit

**Jalon** M1 · **Durée** ≈ 14 h · **Niveau** avancé · **Livrable** `agentgate/gateway/`

## Objectif
Placer une passerelle entre les agents et les serveurs MCP : authentification, contrôle des politiques du plan de contrôle, journalisation de chaque appel d'outil. C'est le **point d'application** de toute la gouvernance.

## Prérequis
LAB-03 à LAB-05.

## Étapes
1. Créer `gateway` avec **Spring Cloud Gateway** (reactive).
2. Router `/mcp/{tenant}/{server}/**` vers le serveur enregistré dans le plan de contrôle (cache des routes + invalidation).
3. Filtre d'authentification : valider le jeton OAuth2 et extraire tenant et agent.
4. Filtre de politique : appeler le plan de contrôle (ou un cache) pour autoriser/refuser l'outil demandé ; refus journalisé.
5. Filtre d'audit : pour chaque appel, enregistrer outil, durée, statut, taille, identifiant de corrélation ; **ne jamais journaliser le contenu brut** par défaut (option avec masquage).
6. Résilience : timeouts, circuit breaker (Resilience4j), limite de débit par tenant.
7. Tests : Testcontainers avec les deux serveurs MCP ; scénarios autorisé, refusé, timeout, panne du serveur.
8. `docker-compose.yml` qui démarre tout (plan de contrôle, passerelle, 2 serveurs MCP, PostgreSQL).

## Critères d'acceptation
- [ ] Un agent autorisé appelle un outil via la passerelle ; un agent non autorisé est refusé et l'événement est audité
- [ ] Le dépassement de débit renvoie 429
- [ ] La coupure d'un serveur MCP n'entraîne pas de blocage de la passerelle (circuit ouvert)
- [ ] `docker compose up` suffit pour rejouer les scénarios

## Pour aller plus loin
Corrélation de bout en bout avec OpenTelemetry ([LAB-10](../lab-10-observability/README.md)).

## Ressources
- Spring Cloud Gateway : <https://docs.spring.io/spring-cloud-gateway/reference/>
- MCP : <https://modelcontextprotocol.io>
