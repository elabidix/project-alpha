# ROADMAP – source de vérité et suivi

Hypothèses : **≈ 10 h/semaine**, démarrage **lundi 16/11/2026 (S1)**, fin **14/11/2027 (S52)**. Les dates sont indicatives : décalez tout si le démarrage change. Contexte et chiffres : [docs/market.md](./docs/market.md).

## Comment utiliser ce fichier

- **Seul endroit où l'on suit l'avancement** : cocher `[x]` ici, rien ailleurs.
- **Rituel du dimanche (20 min)** : cocher ce qui est fini, ajouter une ligne au [journal](#journal), choisir 2 à 3 tâches pour la semaine.
- **Rythme type** : 6 h build, 2 h apprentissage/certification, 2 h visibilité (README, post, échanges).
- **Règle de coupe** si retard : sacrifier d'abord SSO, multi-tenant, routage multi-modèles, Terraform. **Jamais** l'évaluation, la sécurité, la démo ni les [ADR](./docs/adr/README.md).
- **Règle de sortie** : un jalon n'est terminé que si sa *Definition of Done* est cochée en entier.

## Vue d'ensemble

| Jalon | Semaines (dates) | Charge | Résultat |
|---|---|---|---|
| [M0 Fondations](#m0--fondations) | S1-2 (16/11 → 29/11/2026) | 20 h | Outillage agentique, Python, API LLM |
| [M1 Walking skeleton](#m1--walking-skeleton) | S3-8 (30/11/2026 → 10/01/2027) | 63 h | AgentGate v0.1 + démo vidéo |
| [M2 RAG et agents](#m2--rag-et-agents) | S9-16 (11/01 → 07/03/2027) | 80 h | v0.2 publique, premières candidatures |
| [M3 Garde-fous et évaluation](#m3--garde-fous-et-évaluation) | S17-24 (08/03 → 02/05/2027) | 80 h | v0.5 + certification cloud IA |
| [M4 Industrialisation](#m4--industrialisation) | S25-34 (03/05 → 11/07/2027) | 90 h | v1.0 bêta + CKAD |
| [M5 Commercialisation](#m5--commercialisation) | S35-44 (12/07 → 19/09/2027) | 70 h | Offres, pilote, décision produit |
| [M6 Bilan](#m6--bilan) | S45-52 (20/09 → 14/11/2027) | 40 h | Nouveau scan marché, cap choisi |

## Progression globale

- [ ] M0 terminé
- [ ] M1 terminé
- [ ] M2 terminé
- [ ] M3 terminé
- [ ] M4 terminé
- [ ] M5 terminé
- [ ] M6 terminé

---

## M0 – Fondations

**Objectif.** Travailler quotidiennement avec un assistant de code agentique, écrire du Python de production, et appeler un LLM proprement depuis Python et Java.

**TP**
- [ ] [LAB-00 Environnement agentique](./labs/lab-00-agentic-workflow/README.md) (6 h)
- [ ] [LAB-01 Python pour développeurs Java](./labs/lab-01-python-for-java-devs/README.md) (8 h)
- [ ] [LAB-02 Bases des API LLM](./labs/lab-02-llm-api-basics/README.md) (6 h)

**Ressources**
- Claude Code : <https://code.claude.com/docs/en/overview> · GitHub Copilot : <https://docs.github.com/copilot>
- Modèles d'instructions d'agent par techno : <https://github.com/github/awesome-copilot/tree/main/instructions> · format `AGENTS.md` : <https://agents.md>
- *AI Engineering*, Chip Huyen (O'Reilly, 2025) : chapitres 1 à 3
- DeepLearning.AI, cours courts : <https://www.deeplearning.ai/short-courses/>

**Definition of Done**
- [ ] CI GitHub Actions verte sur le dépôt
- [ ] Un schéma d'architecture AgentGate (image ou Mermaid) dans `agentgate/`
- [ ] Un fichier d'instructions d'agent (`AGENTS.md`, `CLAUDE.md` ou `.github/copilot-instructions.md`) commité, testé avec/sans et réduit à l'essentiel (voir LAB-00)
- [ ] Trois mini-projets des LAB-00 à 02 dans `exercises/`, chacun avec sa CI

---

## M1 – Walking skeleton

**Objectif.** Un premier AgentGate bout en bout, minimal mais qui tourne avec `docker compose up` : deux outils MCP, un plan de contrôle sécurisé, une passerelle qui audite les appels, une console React.

**TP**
- [ ] [LAB-03 Serveur MCP en Java : screening de conformité](./labs/lab-03-mcp-server-java/README.md) (10 h)
- [ ] [LAB-04 Serveur MCP en Python : alertes de conformité](./labs/lab-04-mcp-server-python/README.md) (7 h)
- [ ] [LAB-05 Plan de contrôle hexagonal](./labs/lab-05-control-plane/README.md) (20 h)
- [ ] [LAB-06 Passerelle MCP avec audit](./labs/lab-06-mcp-gateway/README.md) (14 h)
- [ ] [LAB-07 Console React](./labs/lab-07-react-console/README.md) (12 h)

**Ressources**
- Spécification et SDK MCP : <https://modelcontextprotocol.io>
- Spring AI : <https://docs.spring.io/spring-ai/reference/> (section MCP)
- Spring Authorization Server : <https://docs.spring.io/spring-authorization-server/reference/>
- Spring Cloud Gateway : <https://docs.spring.io/spring-cloud-gateway/reference/>
- Architecture hexagonale : <https://alistair.cockburn.us/hexagonal-architecture/>

**Definition of Done**
- [ ] `docker compose up` démarre toute la pile
- [ ] Vidéo de démo de 3 minutes
- [ ] Article #1 publié (ex. « Mon premier serveur MCP en Java »)
- [ ] ADR-0001 à 0004 rédigés (voir [docs/adr](./docs/adr/README.md))
- [ ] Tag Git `v0.1.0`

*Prévoir 1 à 2 semaines de marge autour des fêtes de fin d'année.*

---

## M2 – RAG et agents

**Objectif.** Montrer l'intégration IA dans un SI Java (RAG) et un agent avec validation humaine, observé de bout en bout.

**TP**
- [ ] [LAB-08 RAG avec Spring AI et pgvector](./labs/lab-08-rag-spring-ai/README.md) (20 h)
- [ ] [LAB-09 Agent LangGraph avec validation humaine](./labs/lab-09-agent-langgraph/README.md) (24 h)
- [ ] [LAB-10 Observabilité LLM (Langfuse, OpenTelemetry)](./labs/lab-10-observability/README.md) (12 h)
- [ ] [LAB-18 Fiabilité des événements : outbox, idempotence, relecture](./labs/lab-18-reliable-events/README.md) (10 h)

**Ressources**
- LangGraph : <https://langchain-ai.github.io/langgraph/>
- Langfuse : <https://langfuse.com/docs> · OpenTelemetry Java : <https://opentelemetry.io/docs/languages/java/>
- Évaluer les systèmes LLM : <https://hamel.dev/blog/posts/evals/>
- Cours courts DeepLearning.AI sur les agents et le RAG

**Definition of Done**
- [ ] L'application RAG répond avec citations et son jeu de test passe
- [ ] L'agent s'interrompt pour validation humaine et reprend après approbation
- [ ] Les traces apparaissent dans Langfuse avec coûts par appel
- [ ] Aucun événement perdu ni effet en double après arrêt brutal et doublons injectés (LAB-18)
- [ ] ADR-0005, 0006, 0007 et 0011 rédigés
- [ ] Article #2 publié ; tag `v0.2.0`, dépôt rendu présentable (README, schéma)
- [ ] **5 candidatures ciblées** envoyées en citant le dépôt (offres « Java + IA », « agentic coding »)

---

## M3 – Garde-fous et évaluation

**Objectif.** Rendre les agents *fiables et contrôlés* : le différenciant n° 1 face aux profils qui ne font que des démos. Passer une certification cloud IA.

**TP**
- [ ] [LAB-11 Garde-fous et sécurité IA](./labs/lab-11-guardrails/README.md) (20 h)
- [ ] [LAB-12 Évaluation continue en CI](./labs/lab-12-evals-ci/README.md) (16 h)
- [ ] [LAB-13 Routage de modèles, quotas, fallback](./labs/lab-13-model-routing/README.md) (12 h)

**Certification (32 h d'étude)** : choisir un seul cloud.
- [ ] Cloud choisi (cocher un) : Azure AI-103 · AWS · GCP
- [ ] Plan d'étude daté et examen réservé (cible S24)
- [ ] Examen réussi

**Ressources**
- OWASP Top 10 pour LLM : <https://genai.owasp.org/llm-top-10/>
- Presidio (PII) : <https://microsoft.github.io/presidio/> · promptfoo : <https://www.promptfoo.dev/docs/intro> · DeepEval : <https://deepeval.com>
- LiteLLM : <https://docs.litellm.ai> · Ollama : <https://ollama.com>
- AI-103 : <https://learn.microsoft.com/en-us/credentials/certifications/azure-ai-apps-and-agents-developer-associate/> · AWS : <https://aws.amazon.com/certification/>
- AI Act (repères de conformité) : <https://artificialintelligenceact.eu>

**Definition of Done**
- [ ] Jeu d'attaques d'injection et de fuite de données automatisé, avec rapport
- [ ] Évaluation bloquante en CI (seuils) sur au moins un agent et le RAG
- [ ] Quotas et coûts visibles par tenant
- [ ] Certification obtenue et ajoutée au profil
- [ ] ADR-0008 et 0009 rédigés
- [ ] Tag `v0.5.0` ; **nouveau scan marché** (mise à jour de [docs/market.md](./docs/market.md))

---

## M4 – Industrialisation

**Objectif.** Passer du « ça marche chez moi » à « déployable en entreprise » : Kubernetes, SSO, multi-tenant, et une étude de cas legacy.

**TP**
- [ ] [LAB-14 Kubernetes et Helm](./labs/lab-14-kubernetes-helm/README.md) (24 h)
- [ ] [LAB-15 Terraform](./labs/lab-15-terraform/README.md) (10 h, **optionnel**)
- [ ] [LAB-16 Modernisation legacy assistée par IA](./labs/lab-16-legacy-modernization/README.md) (24 h)
- [ ] [LAB-17 Multi-tenant et SSO](./labs/lab-17-multitenancy-sso/README.md) (14 h)

**Certification Kubernetes (≈ 30 h d'étude)**
- [ ] Plan d'étude daté et examen CKAD réservé (cible S32-34)
- [ ] CKAD réussi

**Ressources**
- Kubernetes : <https://kubernetes.io/docs/> · kind : <https://kind.sigs.k8s.io/> · Helm : <https://helm.sh/docs/> · simulateur d'examen : <https://killer.sh>
- Terraform : <https://developer.hashicorp.com/terraform/tutorials>
- Keycloak : <https://www.keycloak.org/documentation>
- Méthode agentique spec-driven : BMAD-METHOD <https://github.com/bmad-code-org/BMAD-METHOD>

**Definition of Done**
- [ ] Installation complète via un seul chart Helm sur kind
- [ ] SSO (Keycloak) et isolation entre au moins deux tenants testées
- [ ] Étude de cas legacy publiée (avant/après, mesures de gain)
- [ ] CKAD obtenue
- [ ] ADR-0010 rédigé ; **revue d'architecture** : relire les 11 ADR, corriger ceux que les tests ou les mesures ont contredits (noter l'écart, ne pas le cacher)
- [ ] Documentation (site ou dossier `docs/`) ; tag `v1.0.0-beta`

---

## M5 – Commercialisation

**Objectif.** Transformer la vitrine en chiffre d'affaires et décider du sort du produit à partir de vraies conversations.

**Tâches** (pas de TP)
- [ ] Rédiger les 3 offres : audit « Agent Readiness » (5-10 j), sprint « Agent en production » (4-8 sem.), option AgentGate Enterprise
- [ ] Trame d'audit réutilisable (checklist risques : injection, fuite de données, coûts, journalisation)
- [ ] Page d'atterrissage + profil LinkedIn et Malt réécrits (titre : *Senior Java/React Engineer – Agentic AI, MCP, RAG en production*)
- [ ] 1 talk (meetup ou conférence) ou webinaire
- [ ] 10 conversations ciblées (anciens clients, ESN, cabinets, startups)
- [ ] 1 client pilote ou partenaire de test

**Ressources**
- Positionnement TJM : 600–650 € après M3, 650–700 €+ avec cas d'étude publié (fourchettes de [docs/market.md](./docs/market.md)) : à valider avec vos recruteurs
- Vérifier la clause de propriété intellectuelle de vos contrats avant toute commercialisation

**Definition of Done**
- [ ] Les 6 scénarios de démonstration (A à F, voir [agentgate/README.md](./agentgate/README.md)) sont rejouables et filmés
- [ ] 1 mission payée **ou** 3 conversations qualifiées
- [ ] **Décision go/no-go produit** notée dans le journal : continuer comme vitrine seule, produit open-core, ou arrêt

---

## M6 – Bilan

**Objectif.** Mesurer, ajuster et choisir le cap pour l'année suivante.

- [ ] Nouveau scan du marché (LinkedIn, Malt, Free-Work, retours recruteurs)
- [ ] Mise à jour de [docs/market.md](./docs/market.md) et de ce fichier (nouveau cycle)
- [ ] Bilan chiffré : TJM atteint, candidatures, entretiens, missions
- [ ] Cap choisi : freelance premium, produit, ou hybride

---

## Lecture : *Designing Data-Intensive Applications* (Kleppmann, Riccomini)

**Verdict : oui, utile**, surtout pour les rôles architecte/tech lead et les entretiens de conception. Le livre ne parle pas d'IA : il donne les fondations (transactions, flux d'événements, données dérivées, évolution de schéma, pannes) sur lesquelles reposent des agents et du RAG fiables. C'est ce qui vous distingue d'un profil « démo ».

Les numéros de chapitres ci-dessous viennent de la table des matières de la 2ᵉ édition.

**Rythme** : ≈ 1 h par semaine, prise sur les 2 h d'apprentissage (≈ 45 h sur l'année pour les chapitres essentiels, ≈ 8 pages/h). Lire avant le TP, puis noter dans le journal une idée appliquée. Les chapitres « optionnels » ne se lisent que s'il reste du temps ou si une offre ou un entretien l'exige.

| Quand | Chapitres (essentiels en gras) | Pourquoi dans ce projet |
|---|---|---|
| M0-M1 (S1-8) | **1** Compromis d'architecture (systèmes de référence vs dérivés, cloud natif, microservices) · **2** Exigences non fonctionnelles (percentiles, tolérance aux pannes) · **5** Encodage et évolution (Protobuf/Avro, REST/RPC, *Durable Execution and Workflows*, architectures événementielles) | Contrats d'API et schémas d'outils MCP versionnés ([LAB-03](./labs/lab-03-mcp-server-java/README.md), [LAB-05](./labs/lab-05-control-plane/README.md)) ; p95 des futurs tableaux de bord ([LAB-10](./labs/lab-10-observability/README.md)) |
| M1-M2 (S6-12) | **8** Transactions (ACID, isolation, write skew, 2PC, *Exactly-Once Message Processing Revisited*) · **4** sections *B-Trees vs LSM*, *Full-Text Search*, *Vector Embeddings* · **3** section *Event Sourcing and CQRS* | Audit insertion seule, contraintes ([LAB-05](./labs/lab-05-control-plane/README.md)) ; comprendre l'index pgvector et la recherche hybride ([LAB-08](./labs/lab-08-rag-spring-ai/README.md)) ; journal d'audit comme journal d'événements |
| M2 (S9-16) | **12** Traitement de flux (journaux, CDC, état et immuabilité, tolérance aux pannes) · **13** Philosophie des systèmes de flux (données dérivées, *Aiming for Correctness*) | Un index vectoriel est une *vue dérivée* à garder synchronisée ; outbox et CDC ([LAB-18](./labs/lab-18-reliable-events/README.md)) ; reprise d'un agent = exécution durable ([LAB-09](./labs/lab-09-agent-langgraph/README.md)) |
| M3 (S17-24) | **9** Les problèmes des systèmes distribués (pannes partielles, timeouts, verrous et baux) · **13** sections *Trust, but Verify* et *Enforcing Constraints* · **14** Faire ce qui est juste | Timeouts, repli, nouvelles tentatives ([LAB-06](./labs/lab-06-mcp-gateway/README.md), [LAB-13](./labs/lab-13-model-routing/README.md)) ; « faire confiance mais vérifier » = évaluation continue ([LAB-12](./labs/lab-12-evals-ci/README.md)) ; biais, vie privée, responsabilité = garde-fous et note AI Act ([LAB-11](./labs/lab-11-guardrails/README.md)) |
| M4 (S25-34) | **7** section *Sharding for Multitenancy* · *6* Réplication (survol : réplication asynchrone, retard de réplication) · *10* Cohérence et consensus (survol : *Coordination Services*) | Isolation par tenant ([LAB-17](./labs/lab-17-multitenancy-sso/README.md)) ; PostgreSQL et état des agents en haute disponibilité ([LAB-14](./labs/lab-14-kubernetes-helm/README.md)) |
| M5+ (optionnel) | *3* Modèles de données (GraphQL, graphes) · *11* Traitement par lots (stockage objet, orchestration, usages ML) · *1* section *Data Systems, Law, and Society* | Entretiens d'architecte, offres d'audit, conformité (AI Act, RGPD) |

**Priorités si le temps manque** : 1, 2, 5, 8, 9, 12, 13, 14 (≈ 340 pages sur ≈ 600). Les chapitres en italique ne se lisent que par sections.

**Livrable de lecture** (dans le journal ou un article) : un schéma « garanties d'AgentGate » : ce que le système assure en cas de panne, de doublon, de désordre, et ce qu'il n'assure pas. À produire avec LAB-18.

**Du livre à la vision d'architecte** : lire ne se voit pas, décider et justifier se voit. Chaque TP clé produit donc un [ADR](./docs/adr/README.md) (choix, alternatives, compromis, preuve). À M5, les 11 ADR et le schéma des garanties deviennent un article ou un talk « Compromis d'architecture d'une plateforme d'agents IA », et la matière des entretiens de conception pour les rôles d'architecte (TJM 610 € relevé dans [docs/market.md](./docs/market.md)).

## Cette semaine

À réécrire chaque dimanche (2 à 3 tâches maximum).

- [ ] Créer le dépôt local et pousser le premier commit
- [ ] Parcourir Malt, Free-Work et LinkedIn et noter 30 offres à comparer avec [docs/market.md](./docs/market.md)
- [ ] Démarrer [LAB-00](./labs/lab-00-agentic-workflow/README.md)

## Risques

| Risque | Parade |
|---|---|
| Surdimensionner le projet | Walking skeleton d'abord, règle de coupe |
| Concurrence (LiteLLM, Langfuse, Kong, passerelles cloud) | Assumer vitrine + accélérateur de missions ; produit en option |
| Technologies qui bougent vite (MCP, A2A, frameworks) | Isoler derrière des interfaces ; rescan marché à M3 et M6 |
| Propriété intellectuelle | Aucun code ni donnée client ; données synthétiques ; ne rien reprendre de vos employeurs (le domaine de la conformité bancaire est proche de votre expérience : relire votre clause de confidentialité avant de publier) |
| Échantillon d'offres biaisé | Recouper avec Malt/Free-Work et recruteurs |
| Manque de temps | Allonger les jalons plutôt que bâcler l'évaluation et la sécurité |

## Journal

| Date | Jalon | Note (fait, bloqué, décision) |
|---|---|---|
| 2026-11-12 | M0 | Création du dépôt et de la roadmap |
