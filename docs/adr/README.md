# Décisions d'architecture (ADR)

Chaque ADR consigne **un choix, ses alternatives et ses compromis**. C'est la preuve visible de la vision d'architecte : on ne dit pas « j'ai utilisé X », on dit « j'ai choisi X plutôt que Y, pour cette raison, avec ce coût ».

Règle : un ADR par TP concerné (≈ 1 h), rédigé **avant ou pendant** l'implémentation, jamais après coup. Les ADR sont comptés dans la *Definition of Done* des jalons et ne sont pas sacrifiés en cas de retard. L'avancement se coche dans [ROADMAP.md](../../ROADMAP.md) ; ce dossier ne contient pas de statut.

## Gabarit

Copier dans `NNNN-titre-court.md` (ex. `0004-timeouts-et-reessais.md`).

```markdown
# ADR-NNNN : titre

Date : AAAA-MM-JJ · Statut : proposé | accepté | remplacé par ADR-XXXX · TP : LAB-NN

## Contexte
Le problème, les contraintes (volume, pannes, sécurité, coût, délai).

## Options étudiées
1. Option A : avantages, inconvénients
2. Option B : avantages, inconvénients
3. (au moins deux options réelles)

## Décision
L'option retenue et pourquoi, en citant le compromis (ex. cohérence contre disponibilité).

## Conséquences
Ce que l'on gagne, ce que l'on accepte de perdre, ce qu'il faudra surveiller.

## Ce que la décision ne garantit pas
Les pannes ou cas limites non couverts, et comment on les détecte.

## Preuve
Test, mesure ou expérience de panne qui valide la décision (lien vers le code ou le rapport).

## Références
DDIA chapitre N (section), autres sources.
```

## ADR prévus

| ADR | Sujet | TP | DDIA |
|---|---|---|---|
| 0001 | Système de référence PostgreSQL et architecture hexagonale | LAB-05 | ch. 1, 2 |
| 0002 | Niveau d'isolation et journal d'audit en insertion seule | LAB-05 | ch. 8 |
| 0003 | Versionnage des contrats d'API et des schémas d'outils MCP | LAB-03, LAB-05 | ch. 5 |
| 0004 | Timeouts, nouvelles tentatives et disjoncteur de la passerelle | LAB-06 | ch. 9 |
| 0005 | L'index vectoriel comme vue dérivée ; recherche hybride | LAB-08 | ch. 1, 4 |
| 0006 | Exécution durable et reprise des agents | LAB-09 | ch. 5, 8 |
| 0007 | Outbox contre CDC ; garanties de livraison | LAB-18 | ch. 8, 12 |
| 0008 | Évaluation continue comme vérification | LAB-12 | ch. 13 |
| 0009 | Repli, cache et cohérence du routage de modèles | LAB-13 | ch. 9 |
| 0010 | Stratégie d'isolation multi-tenant | LAB-17 | ch. 7, 8 |
