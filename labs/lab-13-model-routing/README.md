# LAB-13 – Routage de modèles, quotas et fallback

**Jalon** M3 · **Durée** ≈ 12 h · **Niveau** moyen à avancé · **Livrable** `agentgate/gateway/` (module modèles) + `agentgate/deploy/litellm/`

## Objectif
Contrôler l'accès aux modèles : routage entre fournisseurs et modèle local, quotas, timeouts, repli en cas de panne, coûts. Correspond aux missions « LLMOps / model serving ».

## Prérequis
LAB-02, LAB-06, LAB-10.

## Étapes
1. Déployer **LiteLLM** (proxy) avec au moins deux fournisseurs et un modèle local **Ollama**.
2. Définir des règles : modèle économique par défaut, modèle puissant pour les cas complexes, modèle local pour les données sensibles.
3. **Fallback** : si le fournisseur A échoue ou dépasse le délai, bascule sur B ; tester par injection de pannes.
4. **Quotas** par tenant (tokens/jour, requêtes/minute) appliqués côté passerelle, avec erreurs 429 explicites.
5. **Cache** de réponses pour les requêtes identiques ; mesurer le gain et définir quand il est dangereux.
6. **Versionnage de prompts** : prompts stockés et versionnés, chaque trace indique la version utilisée.
7. Rapport coût/qualité : 20 cas évalués avec 3 modèles (score LAB-12, coût, latence) et recommandation.

## Critères d'acceptation
- [ ] Une panne simulée du fournisseur principal est invisible pour l'utilisateur (repli)
- [ ] Un tenant dépassant son quota reçoit 429 sans impacter les autres
- [ ] Le rapport coût/qualité justifie le modèle choisi par cas d'usage
- [ ] Chaque trace mentionne modèle et version du prompt

## Pour aller plus loin
Servir un modèle ouvert avec **vLLM** sur GPU (cloud ponctuel) et le brancher derrière LiteLLM.

## Ressources
- LiteLLM : <https://docs.litellm.ai> · Ollama : <https://ollama.com> · vLLM : <https://docs.vllm.ai>
