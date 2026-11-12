# LAB-03 – Serveur MCP en Java : screening de conformité

**Jalon** M1 · **Durée** ≈ 10 h · **Niveau** moyen · **Livrable** `agentgate/mcp-screening/`

## Objectif
Exposer un petit moteur **déterministe** de screening de conformité bancaire (données 100 % synthétiques) comme **serveur MCP** consommable par un assistant ou un agent. Le moteur calcule, l'IA ne fait qu'expliquer et assister : aucune décision réglementaire n'est prise par l'IA. MCP est cité dans 18 % des annonces Java + IA et encore peu maîtrisé.

## Prérequis
LAB-00 à LAB-02. Lire l'introduction de MCP (outils, ressources, prompts, transports). Lire la [note de confidentialité](../../agentgate/README.md#cadre-et-confidentialité) avant de modéliser le domaine.

## Étapes
1. Créer le projet Spring Boot `mcp-screening` (Java 21) avec la dépendance Spring AI pour serveur MCP.
2. Modéliser un domaine fictif : `Customer`, `WatchlistEntry` (liste synthétique de 50 à 100 entrées avec alias, dates de naissance, pays), `ScreeningResult`. Jamais de données réelles ni reprises d'un employeur.
3. **Moteur de correspondance** (simple et explicable) : normalisation (casse, accents, inversion nom/prénom), similarité de noms (Jaro-Winkler ou Levenshtein via une bibliothèque), alias, date de naissance et pays comme critères complémentaires. Le résultat contient le score, les critères qui ont pesé, les champs comparés, les règles déclenchées et la source. Un score n'est jamais une preuve d'identité.
4. Exposer 3 **outils** : `searchCustomers(query)`, `screenCustomer(customerId)`, `getWatchlistEntry(id)` avec descriptions précises (le modèle s'en sert pour choisir).
5. Exposer 1 **ressource** (procédure de traitement d'une alerte, en texte) et 1 **prompt** réutilisable (« résumer une investigation »).
6. Tester avec **MCP Inspector**, puis brancher le serveur dans votre assistant (Claude Code ou Copilot) et poser 5 questions métier.
7. Ajouter la validation des entrées, des limites (taille, pagination) et des logs sans données personnelles.
8. Écrire des tests : 20 paires de noms (variantes, inversions, homonymes) avec résultat attendu pour le moteur, et des tests d'intégration (appel d'outil via le client MCP de test) ; image Docker.

## Critères d'acceptation
- [ ] ADR-0003 rédigé (versionnage des contrats et schémas d'outils) : [gabarit](../../docs/adr/README.md)
- [ ] Les 3 outils sont découverts par l'Inspector et par l'assistant
- [ ] Le moteur donne le résultat attendu sur ≥ 18 des 20 paires, et chaque résultat est explicable (critères et sources)
- [ ] 5 scénarios de questions réussissent ; les échecs sont documentés
- [ ] Les entrées invalides renvoient une erreur claire, jamais une exception brute
- [ ] Tests d'intégration verts en CI ; image Docker construite

## Pour aller plus loin
Transport HTTP (streamable) plutôt que stdio, en préparation de la passerelle ([LAB-06](../lab-06-mcp-gateway/README.md)).

## Ressources
- MCP : <https://modelcontextprotocol.io> · Inspector : <https://github.com/modelcontextprotocol/inspector>
- Spring AI (section MCP) : <https://docs.spring.io/spring-ai/reference/>
