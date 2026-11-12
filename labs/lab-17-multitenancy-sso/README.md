# LAB-17 – Multi-tenant et SSO

**Jalon** M4 · **Durée** ≈ 14 h · **Niveau** avancé · **Livrable** `agentgate/control-plane/` + `agentgate/deploy/keycloak/`

## Objectif
Isoler les clients entre eux et brancher l'authentification d'entreprise (SSO). Exigence de toute vente en grand compte.

## Prérequis
LAB-05, LAB-06, LAB-07, LAB-14.

## Étapes
1. Déployer **Keycloak** ; créer deux royaumes ou organisations (tenants A et B) avec utilisateurs et rôles.
2. Brancher la console et le plan de contrôle en OIDC ; mapper les groupes Keycloak vers les rôles `admin`, `operator`, `auditor`.
3. **Isolation des données** : choisir et justifier une stratégie (colonne `tenant_id` + filtrage systématique, ou schémas séparés). Implémenter avec contrainte au niveau base (Row Level Security PostgreSQL recommandé).
4. Propager l'identifiant de tenant dans tous les appels (passerelle, runtime, RAG) ; refuser tout accès sans tenant.
5. Tests d'**isolation** : le tenant A ne peut ni lire, ni modifier, ni deviner l'existence des ressources du tenant B (y compris via l'audit, le cache et les traces).
6. Quotas et coûts par tenant (réutilisation LAB-13).
7. Documenter le modèle de menaces multi-tenant.

## Critères d'acceptation
- [ ] Suite de tests d'isolation verte, y compris tentatives par identifiants devinés
- [ ] Un auditeur du tenant A ne voit aucun événement du tenant B
- [ ] La suppression d'un tenant supprime ses données (démontré par test)
- [ ] SSO fonctionnel avec rôles mappés

## Ressources
- DDIA : ch. 7 *Sharding for Multitenancy* ; ch. 8 Transactions et isolation (stratégie d'isolation par `tenant_id`)
- Keycloak : <https://www.keycloak.org/documentation>
- PostgreSQL Row Level Security : <https://www.postgresql.org/docs/current/ddl-rowsecurity.html>
- Spring Security : <https://docs.spring.io/spring-security/reference/>
