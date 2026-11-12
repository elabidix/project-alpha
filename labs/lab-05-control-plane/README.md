# LAB-05 – Plan de contrôle hexagonal

**Jalon** M1 · **Durée** ≈ 20 h · **Niveau** avancé · **Livrable** `agentgate/control-plane/`

## Objectif
Construire le cœur d'AgentGate : le service qui gère tenants, registre d'outils/agents, politiques d'accès et journal d'audit. C'est ici que votre expérience Java senior fait la différence.

## Prérequis
LAB-03, LAB-04. Connaissances Spring Security et JPA.

## Étapes
1. Structurer en **hexagonal** : `domain` (sans framework), `application` (cas d'usage), `adapters` (REST, JPA). Ajouter des tests **ArchUnit** qui interdisent les dépendances interdites.
2. Modèle : `Tenant`, `ToolServer` (URL, transport, propriétaire), `Agent`, `Policy` (qui peut appeler quel outil), `AuditEvent`.
3. API REST versionnée (`/api/v1`) : CRUD du registre, enregistrement d'un serveur MCP, test de connectivité. Documentation **OpenAPI**.
4. Sécurité : **Spring Authorization Server** (ou Keycloak simple pour démarrer), OAuth2 client credentials pour les agents, rôles `admin`, `operator`, `auditor`.
5. Persistance **PostgreSQL**, migrations **Flyway**, tests avec **Testcontainers**.
6. Journal d'audit **immuable** (insertion seule) : qui, quoi, quand, résultat, identifiant de corrélation.
7. Ajouter des tests de contrat de l'API (Spring REST Docs ou tests OpenAPI) et un `Dockerfile`.

## Critères d'acceptation
- [ ] Tests ArchUnit verts (le domaine ne dépend d'aucun framework)
- [ ] Un client sans le bon rôle reçoit 403 ; sans jeton, 401
- [ ] Aucune modification ni suppression possible sur `AuditEvent` via l'API
- [ ] Couverture ≥ 80 % sur domaine et application
- [ ] OpenAPI publié ; image Docker construite

## Pour aller plus loin
Événements de domaine publiés sur Kafka pour l'audit asynchrone ([LAB-08](../lab-08-rag-spring-ai/README.md)).

## Ressources
- DDIA : transactions et niveaux d'isolation, évolution des schémas (voir [ROADMAP.md](../../ROADMAP.md), section Lecture)
- Hexagonal : <https://alistair.cockburn.us/hexagonal-architecture/> · ArchUnit : <https://www.archunit.org>
- Spring Authorization Server : <https://docs.spring.io/spring-authorization-server/reference/>
- Testcontainers : <https://testcontainers.com/guides/>
