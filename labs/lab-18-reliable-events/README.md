# LAB-18 – Fiabilité des événements : outbox, idempotence, relecture

**Jalon** M2 · **Durée** ≈ 10 h · **Niveau** avancé · **Livrable** `agentgate/control-plane/` (outbox) + `agentgate/rag-app/` (consommateur idempotent)

## Objectif
Rendre fiables les échanges d'événements d'AgentGate (audit, ingestion RAG, approbations). Vous appliquez ici les idées de *Designing Data-Intensive Applications* sur les systèmes dérivés, les flux d'événements et les garanties de livraison. C'est ce qui sépare un senior d'un développeur qui « branche Kafka ».

## Prérequis
LAB-05, LAB-08 (Kafka et ingestion asynchrone). Lecture conseillée : les chapitres de DDIA sur les transactions, les flux d'événements et les données dérivées (voir [ROADMAP.md](../../ROADMAP.md), section Lecture).

## Étapes
1. **Reproduire le bug** : le plan de contrôle écrit un `AuditEvent` en base puis publie sur Kafka. Provoquer un arrêt brutal entre les deux et constater l'incohérence (écriture double non atomique).
2. **Outbox transactionnelle** : écrire l'événement dans une table `outbox` dans la *même* transaction que la donnée métier ; un relais (polling, ou Debezium) publie ensuite sur Kafka.
3. **Consommateurs idempotents** : la livraison est *au moins une fois*. Dédupliquer par identifiant d'événement (contrainte d'unicité) ; tester avec des doublons injectés.
4. **Ordre** : choisir la clé de partition (`tenantId` ou `dossierId`) ; démontrer par un test ce qui casse sans clé (événements d'un même dossier traités dans le désordre).
5. **Échecs** : nouvelle tentative avec backoff, file des messages morts (DLQ), message « poison » qui n'arrête pas le consommateur.
6. **Reconstruire un système dérivé** : rejouer le topic pour reconstruire l'index vectoriel du RAG et la vue d'audit ; mesurer la durée et vérifier que le résultat est identique.
7. **Évolution de schéma** : ajouter un champ à l'événement ; les anciens consommateurs doivent continuer à fonctionner (compatibilité ascendante et descendante, schéma versionné).
8. **Test de chaos** : tuer broker, relais et consommateur pendant une charge ; aucun événement perdu, aucun effet en double.

## Critères d'acceptation
- [ ] Après l'arrêt brutal de l'étape 1, aucun événement n'est perdu avec l'outbox (test automatisé)
- [ ] Un événement livré 3 fois produit un seul effet
- [ ] Le message poison finit en DLQ sans bloquer les suivants
- [ ] La reconstruction de l'index depuis le topic donne les mêmes résultats qu'avant
- [ ] Un consommateur ancien lit un événement au nouveau schéma
- [ ] Une note d'une page explique ce que vous garantissez (et ne garantissez pas) : « exactement une fois » en pratique

## Pour aller plus loin
Appliquer la même idée aux outils des agents ([LAB-09](../lab-09-agent-langgraph/README.md)) : clé d'idempotence sur chaque action sensible pour qu'une reprise ou une nouvelle tentative ne l'exécute pas deux fois.

## Ressources
- Designing Data-Intensive Applications (Kleppmann, Riccomini), thèmes transactions, flux d'événements, données dérivées, évolution des schémas
- Pattern outbox : <https://microservices.io/patterns/data/transactional-outbox.html>
- Debezium : <https://debezium.io/documentation/>
- Spring for Apache Kafka : <https://docs.spring.io/spring-kafka/reference/>
- Testcontainers (Kafka) : <https://testcontainers.com/guides/>
