# LAB-11 – Garde-fous et sécurité IA

**Jalon** M3 · **Durée** ≈ 20 h · **Niveau** avancé · **Livrable** `agentgate/gateway/` (filtres) + `agentgate/evals/security/`

## Objectif
Protéger les agents contre l'injection de prompt, les fuites de données et les outils détournés. Rare chez les candidats, et demandé par les banques (« guardrails », « sécurité des agents »).

## Prérequis
LAB-04, LAB-06, LAB-09.

## Étapes
1. Lire l'OWASP Top 10 LLM et cartographier chaque risque sur AgentGate (tableau dans `docs/threat-model.md`).
2. **Filtrage PII** : détecter et masquer noms, IBAN, e-mails, numéros de téléphone en entrée et sortie, avec **Presidio** ; mesurer faux positifs/négatifs sur un jeu de 100 textes synthétiques.
3. **Injection de prompt** : constituer 30 attaques (directes, indirectes via un document RAG, via une description d'outil MCP piégée) et un classifieur ou règles de détection dans la passerelle.
4. **Principe du moindre privilège** : chaque agent n'a accès qu'aux outils de sa politique ; paramètres sensibles interdits par schéma.
5. **Sorties** : vérifier format et contenu (pas de secret, pas d'URL arbitraire) avant exécution d'une action.
6. **Journal de sécurité** : chaque blocage est audité avec la raison.
7. Automatiser un **rapport de red teaming** (promptfoo) exécuté en CI : taux d'attaques bloquées par catégorie.
8. Rédiger une note de conformité (AI Act) : transparence, supervision humaine, traçabilité couvertes par AgentGate.

## Critères d'acceptation
- [ ] ≥ 90 % des 30 attaques sont bloquées, les échecs sont analysés
- [ ] Faux positifs PII < 5 % sur le jeu témoin
- [ ] Un outil piégé n'obtient pas d'action sensible sans approbation
- [ ] Le rapport de sécurité est généré automatiquement en CI

## Pour aller plus loin
Test de « RAG poisoning » : un document piégé dans le corpus du [LAB-08](../lab-08-rag-spring-ai/README.md).

## Ressources
- DDIA : ch. 14 *Doing the Right Thing* (biais, responsabilité, vie privée) et ch. 1 *Data Systems, Law, and Society*, pour le modèle de menaces et la note de conformité
- OWASP LLM Top 10 : <https://genai.owasp.org/llm-top-10/>
- Presidio : <https://microsoft.github.io/presidio/> · promptfoo (red teaming) : <https://www.promptfoo.dev/docs/intro>
- AI Act : <https://artificialintelligenceact.eu>
