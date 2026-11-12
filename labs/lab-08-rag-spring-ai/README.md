# LAB-08 – RAG avec Spring AI et pgvector

**Jalon** M2 · **Durée** ≈ 20 h · **Niveau** avancé · **Livrable** `agentgate/rag-app/`

## Objectif
Construire un assistant de questions-réponses sur des documents d'assurance, avec **citations des sources** et une évaluation chiffrée, en Java. Le RAG est dans 31 % des annonces Java + IA.

## Prérequis
LAB-02, LAB-05. PostgreSQL avec l'extension pgvector (Docker).

## Étapes
1. Constituer un corpus **synthétique** de 30 à 50 documents (conditions générales, FAQ, procédures) ; ne jamais utiliser de documents clients.
2. **Ingestion** : découpage (chunking) paramétrable, métadonnées (source, page, version), embeddings, stockage pgvector ; ingestion **asynchrone via Kafka** (événement « document ajouté »).
3. **Récupération** : recherche vectorielle, puis combinaison avec recherche plein texte (hybride) et re-classement ; comparer au moins 2 stratégies de chunking.
4. **Génération** : prompt avec contexte, réponse avec citations (document + passage), refus de répondre si le contexte est insuffisant.
5. **Streaming** vers un front React minimal (SSE) avec affichage des sources et un bouton « utile / pas utile ».
6. **Évaluation de base** : jeu de 30 questions avec réponses attendues et documents sources ; mesurer *fidélité* (la réponse est-elle appuyée par le contexte ?), *pertinence du contexte* et *taux de refus justifié* avec Ragas ou DeepEval.
7. Documenter dans le README les résultats avant/après chaque amélioration.

## Critères d'acceptation
- [ ] Chaque réponse cite ses sources ; une question hors corpus donne un refus explicite
- [ ] Les scores d'évaluation sont publiés et reproductibles (`make eval` ou équivalent)
- [ ] L'ingestion tolère un document corrompu sans bloquer les autres
- [ ] Une amélioration mesurée entre la première et la dernière version (≥ 10 points sur la fidélité, ou explication honnête sinon)

## Pour aller plus loin
Variante en Python/LangChain sur le même corpus, pour comparer.

## Ressources
- DDIA : données dérivées et index (l'index vectoriel est une vue dérivée à garder synchronisée), voir [LAB-18](../lab-18-reliable-events/README.md)
- Spring AI : <https://docs.spring.io/spring-ai/reference/>
- Ragas : <https://docs.ragas.io> · DeepEval : <https://deepeval.com>
- Évaluer les systèmes LLM : <https://hamel.dev/blog/posts/evals/>
- *AI Engineering*, Chip Huyen : chapitres sur le RAG et l'évaluation
