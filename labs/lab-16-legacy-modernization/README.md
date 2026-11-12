# LAB-16 – Modernisation de legacy assistée par IA

**Jalon** M4 · **Durée** ≈ 24 h · **Niveau** avancé · **Livrable** `agentgate/case-study-legacy/` + article

## Objectif
Démontrer, chiffres à l'appui, comment un workflow agentique accélère la modernisation d'une application legacy en Java, sans perdre en qualité. Sujet récurrent en banque et assurance (Spring Batch, COBOL, architecture hexagonale).

## Prérequis
LAB-00, LAB-05. Un dépôt legacy **fictif ou open source** : jamais de code d'un client ou employeur.

## Étapes
1. Choisir ou écrire une application legacy représentative : Java ancien, batch de calcul de primes, logique métier dans des classes volumineuses, sans tests.
2. **Mesurer l'état initial** : couverture, complexité, dette (SonarQube local, outil d'analyse jetable lancé en Docker pour ce TP, hors pile AgentGate), temps de build. Noter la méthode : sans base de comparaison, aucun gain ne sera crédible.
3. Faire générer des **tests de caractérisation** par l'agent pour figer le comportement actuel, **relus** et corrigés par vous.
4. Découper en **hexagonal** par étapes courtes ; chaque étape = une spec écrite, un plan, un commit, des tests verts.
5. Migrer le batch vers **Spring Batch** (Java 21, Spring Boot actuel) ; documenter les écarts de comportement trouvés.
6. Simuler l'intégration d'un module externe (appel COBOL) derrière un port d'adaptation, avec un bouchon.
7. **Mesurer le résultat** : temps passé, couverture, défauts trouvés après coup, coût en tokens. Pour le temps, ne pas se contenter d'une estimation : migrer **un module témoin à la main, chronométré**, et comparer au même type de module fait avec l'agent (en notant les limites de la comparaison : un module n'est pas un échantillon).
8. Rédiger l'étude de cas (avant/après, ce que l'agent a bien et mal fait, règles de relecture) et un article.

## Critères d'acceptation
- [ ] Le comportement avant/après est identique sur un jeu de cas de référence
- [ ] Couverture ≥ 80 % sur le code migré
- [ ] Chaque gain annoncé est mesuré et la méthode de mesure est décrite
- [ ] L'article liste au moins 3 pièges de l'agent et les contre-mesures

## Pour aller plus loin
Rejouer la modernisation avec un autre outil pour comparer.

## Ressources
- Spring Batch : <https://docs.spring.io/spring-batch/reference/>
- ArchUnit : <https://www.archunit.org> · SonarQube : <https://docs.sonarsource.com/sonarqube/latest/>
- BMAD-METHOD : <https://github.com/bmad-code-org/BMAD-METHOD>
