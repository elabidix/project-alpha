# LAB-03 – Serveur MCP en Java

**Jalon** M1 · **Durée** ≈ 8 h · **Niveau** moyen · **Livrable** `agentgate/mcp-contracts/`

## Objectif
Exposer une API métier d'assurance (contrats) comme **serveur MCP** consommable par un assistant ou un agent. MCP est cité dans 18 % des annonces Java + IA et encore peu maîtrisé.

## Prérequis
LAB-00 à LAB-02. Lire l'introduction de MCP (outils, ressources, prompts, transports).

## Étapes
1. Créer le projet Spring Boot `mcp-contracts` (Java 21) avec la dépendance Spring AI pour serveur MCP.
2. Modéliser un domaine fictif : `Contract`, `Claim` (données synthétiques, jamais réelles).
3. Exposer 3 **outils** : `searchContracts(query)`, `getContract(id)`, `listClaims(contractId)` avec descriptions précises (le modèle s'en sert pour choisir).
4. Exposer 1 **ressource** (conditions générales en texte) et 1 **prompt** réutilisable.
5. Tester avec **MCP Inspector**, puis brancher le serveur dans votre assistant (Claude Code ou Copilot) et poser 5 questions métier.
6. Ajouter la validation des entrées, des limites (taille, pagination) et des logs sans données sensibles.
7. Écrire des tests d'intégration (appel d'outil via le client MCP de test) et une image Docker.

## Critères d'acceptation
- [ ] Les 3 outils sont découverts par l'Inspector et par l'assistant
- [ ] 5 scénarios de questions réussissent ; les échecs sont documentés
- [ ] Les entrées invalides renvoient une erreur claire, jamais une exception brute
- [ ] Tests d'intégration verts en CI ; image Docker construite

## Pour aller plus loin
Transport HTTP (streamable) plutôt que stdio, en préparation de la passerelle ([LAB-06](../lab-06-mcp-gateway/README.md)).

## Ressources
- MCP : <https://modelcontextprotocol.io> · Inspector : <https://github.com/modelcontextprotocol/inspector>
- Spring AI (section MCP) : <https://docs.spring.io/spring-ai/reference/>
