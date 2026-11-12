# LAB-02 – Bases des API LLM (Python et Java)

**Jalon** M0 · **Durée** ≈ 6 h · **Niveau** facile · **Livrable** `exercises/lab-02-llm-api-basics/` (Python et Java)

## Objectif
Maîtriser les briques de base d'un appel LLM : messages, sortie structurée, appel d'outils (function calling), streaming, gestion des coûts et des erreurs. Tout agent et tout MCP repose dessus.

## Prérequis
LAB-01. Une clé d'API d'un fournisseur (OpenAI, Anthropic, Mistral…) ou **Ollama** en local (gratuit). Ne jamais commiter la clé (`.env`, ignoré par Git). Si vous utilisez un fournisseur payant, **fixer un plafond de dépense** dans son tableau de bord avant le premier appel.

## Étapes
1. **Python** : appeler un modèle avec le SDK du fournisseur ; comparer température 0 et 1 sur 5 prompts.
2. **Sortie structurée** : obtenir un JSON validé par un modèle Pydantic (extraction d'informations d'une alerte de conformité fictive) ; mesurer le taux d'échec sur 20 textes.
3. **Appel d'outils** : définir 2 fonctions (`get_contract`, `get_weather` fictive) ; faire choisir l'outil au modèle, exécuter, renvoyer le résultat.
4. **Streaming** : afficher la réponse token par token (SSE via FastAPI).
5. **Java** : refaire les points 1 à 4 avec **Spring AI** (`ChatClient`, sorties structurées, `@Tool`, streaming `Flux`).
6. **Robustesse** : configurer timeout, nouvelles tentatives avec backoff sur erreurs transitoires (429, 5xx) et aucune tentative sur erreurs définitives (400, 401) ; provoquer chaque cas (clé invalide, limite de débit simulée) et vérifier le comportement.
7. **Tests sans réseau** : isoler le client derrière une interface et tester avec un faux client (réponses enregistrées) pour que la CI soit déterministe et gratuite ; un seul test d'intégration réel, optionnel, hors CI.
8. Mesurer tokens et coût d'un lot de 20 appels ; écrire dans un tableau la différence de prix entre deux modèles.
9. Comparer en une page les deux implémentations (verbosité, typage, debug).

## Critères d'acceptation
- [ ] Les mêmes 4 scénarios fonctionnent en Python et en Java
- [ ] Un test vérifie la validité du JSON structuré (au moins 18/20 corrects) ; les échecs sont classés (JSON invalide, champ manquant, valeur hors énumération)
- [ ] Les erreurs transitoires sont retentées, les erreurs définitives non (tests)
- [ ] La CI passe sans clé d'API ni accès réseau
- [ ] Aucun secret dans l'historique Git (vérifié, par exemple avec `gitleaks`)
- [ ] Un tableau tokens/coûts est dans le README du mini-projet

## Pour aller plus loin
Essayer un second fournisseur derrière la même interface (préparation de [LAB-13](../lab-13-model-routing/README.md)).

## Ressources
- Spring AI : <https://docs.spring.io/spring-ai/reference/>
- Ollama : <https://ollama.com>
- Documentation du fournisseur choisi : sorties structurées, appel d'outils, limites de débit, tarifs
- Gitleaks : <https://github.com/gitleaks/gitleaks>
- Cours courts DeepLearning.AI : <https://www.deeplearning.ai/short-courses/>
