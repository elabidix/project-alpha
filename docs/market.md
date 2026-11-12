# Analyse du marché (référence, sans suivi)

Dernière mise à jour : 12/11/2026. À refaire aux jalons M3 et M6 (voir [ROADMAP.md](../ROADMAP.md)).

## Sources

1. **Groupe WhatsApp de freelances** : 733 messages d'offres, 17/06/2026 → 12/11/2026 (marché freelance français, ESN et cabinets).
2. **LinkedIn** : 1 292 annonces publiques des 30 derniers jours (France, Royaume-Uni, Allemagne, Pays-Bas, États-Unis, Canada, remote) ; 642 descriptions analysées.
3. **Malt** : non analysé (accès automatisé refusé). À parcourir à la main.

Biais : les requêtes LinkedIn contenaient « java / spring / ai / agentic / mcp », donc l'échantillon est orienté vers ce profil. Il dit *quoi ajouter à Java*, pas la part de marché de Java + IA.

## 1. Marché freelance français (WhatsApp)

| Signal | Messages (sur 733) |
|---|---|
| IA / AI | 108 |
| Python | 72 |
| DevOps | 69 |
| Java | 69 |
| Kubernetes / Docker / Terraform | 52 / 43 / 33 |
| Spring | 34 |
| Agentique / LLM / RAG / MCP | 22 / 23 / 17 / 12 |

TJM relevés : **600–650 €** pour AI Engineer, LLMOps, développeur « agentic coding » (Java/React, Claude Code) et architecte IA (610 €) ; **470–550 €** pour un développeur Java classique.

Offres proches de votre profil : développeur agentic coding Java/React (Claude Code, BMAD/GSD), full stack Java/Angular « AI-augmented » (Copilot, Cursor, Claude Code), développeur Java expert IA, AI/LLM/RAG senior banque (Java/Spring, Azure, Kubernetes), architecte IA générative et agentique (Python, Java/Quarkus/LangChain4j, MCP/A2A, vLLM).

## 2. LinkedIn, sous-ensemble « Java ET IA » (409 annonces)

| Compétence | % des annonces |
|---|---|
| Java / Spring | 100 / 68 |
| Spring AI / LangChain4j | 5 / 2 |
| Python | 48 |
| LLM / Agents / RAG | 53 / 45 / 31 |
| Évaluation / observabilité | 41 |
| Guardrails / sécurité IA | 18 |
| MCP | 18 |
| Kubernetes / Docker / CI-CD | 49 / 45 / 58 |
| AWS / Azure / GCP | 50 / 34 / 26 |
| React / Angular | 47 / 23 |
| Microservices / Kafka | 47 / 23 |
| Outils IA de dev (Copilot, Cursor, Claude Code) | 46 |
| Kafka / RabbitMQ | 23 / 3 |
| Argo CD (GitOps) / Keycloak / SonarQube | 4 / 1 / 4 |
| Secteur banque, finance ou assurance mentionné (indicatif : le mot peut apparaître hors contexte) | 51 |

France (113 annonces) contre hors France (529) :

| | France | Hors France |
|---|---|---|
| Agents / agentique | 27 % | 57 % |
| Évaluation / observabilité | 23 % | 53 % |
| Guardrails / sécurité IA | 14 % | 27 % |
| Angular | 25 % | 15 % |
| GCP | 35 % | 25 % |

Salaires affichés (75 annonces, à ne pas confondre avec un TJM) : Royaume-Uni 60–100 k£, États-Unis 120–280 k$, Canada 100–200 k$ CAD.

## 3. Conclusions qui guident le plan

1. Java seul se tasse ; **Java + IA en production** est valorisé (écart d'environ 100 € de TJM).
2. **Python est indispensable** à côté de Java : un poste sur deux le demande. Spring AI reste secondaire côté recruteurs, mais utile pour la crédibilité Java.
3. Ce qui se paie : **agents, MCP, évaluation, garde-fous, industrialisation (Kubernetes, CI/CD, observabilité)**.
4. La France a un temps de retard sur l'agentique et l'évaluation : avantage à se positionner tôt, et le remote international est ouvert.
5. Les **outils de développement IA** (Claude Code, Copilot, Cursor) sont exigés, pas optionnels.
6. Une seule certification cloud IA + CKAD suffit ; les projets publiés pèsent plus que les badges.

## 4. Certifications (vérifiées le 12/11/2026)

- Microsoft : *Azure AI Engineer Associate* (AI-102) **retirée** ; successeur **Azure AI Apps and Agents Developer Associate (AI-103)**, Python + Microsoft Foundry. <https://learn.microsoft.com/en-us/credentials/certifications/azure-ai-apps-and-agents-developer-associate/>
- AWS : *AI Practitioner*, *Machine Learning Engineer – Associate* (examen en cours de mise à jour), *Developer – Associate* (en cours de mise à jour). <https://aws.amazon.com/certification/>
- Google Cloud : non vérifié.
- Kubernetes : CKAD, puis CKA. <https://training.linuxfoundation.org/certification/certified-kubernetes-application-developer-ckad/>
