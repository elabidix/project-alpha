# LAB-12 – Évaluation continue en CI

**Jalon** M3 · **Durée** ≈ 16 h · **Niveau** avancé · **Livrable** `agentgate/evals/`

## Objectif
Faire de la qualité des agents et du RAG un critère **bloquant** en CI, comme les tests unitaires. C'est la différence entre une démo et un système de production.

## Prérequis
LAB-08, LAB-09, LAB-10.

## Étapes
1. Constituer des **jeux dorés** : 30 cas RAG et 20 scénarios d'agent (entrée, comportement attendu, outils attendus), versionnés dans Git.
2. Choisir les métriques : exactitude, fidélité au contexte, bon choix d'outil, respect de la validation humaine, coût et latence par cas.
3. Implémenter avec **promptfoo** ou **DeepEval** ; ajouter un **LLM-as-judge** et mesurer son accord avec vos propres notes sur 20 cas (si < 80 %, corriger le juge).
4. Définir des **seuils** et une règle de non-régression : la pull request échoue si une métrique baisse de plus de X points.
5. Intégrer dans **GitHub Actions** (exécution sur un sous-ensemble rapide en PR, complète chaque nuit) ; commentaire automatique de la PR avec les scores.
6. Contrôler le coût de l'évaluation (cache des appels, modèle plus économique pour le juge).
7. Boucle de feedback : transformer 5 erreurs réelles tracées dans Langfuse en nouveaux cas de test.

## Critères d'acceptation
- [ ] Une dégradation volontaire du prompt fait échouer la CI
- [ ] Le juge a ≥ 80 % d'accord avec vos annotations
- [ ] Les scores sont affichés dans la PR et historisés
- [ ] Coût d'une exécution PR documenté et < budget fixé

## Pour aller plus loin
Tableau de bord de l'évolution des scores par version d'AgentGate.

## Ressources
- promptfoo : <https://www.promptfoo.dev/docs/intro> · DeepEval : <https://deepeval.com> · Ragas : <https://docs.ragas.io>
- <https://hamel.dev/blog/posts/evals/>
- GitHub Actions : <https://docs.github.com/actions>
