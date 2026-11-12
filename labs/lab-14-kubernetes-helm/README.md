# LAB-14 – Kubernetes et Helm

**Jalon** M4 · **Durée** ≈ 24 h · **Niveau** avancé · **Livrable** `agentgate/deploy/helm/`

## Objectif
Déployer toute la pile AgentGate sur Kubernetes avec un seul chart Helm, et acquérir les réflexes du CKAD. Kubernetes est cité dans près d'une annonce sur deux.

## Prérequis
LAB-06 à LAB-13 (images Docker disponibles). Docker, `kubectl`, `kind`, `helm`.

## Étapes
1. Créer un cluster **kind** local ; écrire les manifestes à la main pour le plan de contrôle seul (Deployment, Service, ConfigMap, Secret) afin de comprendre avant d'abstraire.
2. Ajouter **sondes** liveness/readiness/startup, **requests/limits**, `securityContext` (non-root, système de fichiers en lecture seule) et **NetworkPolicy** (la console ne parle qu'à la passerelle).
3. Packager en **chart Helm** avec `values.yaml` par environnement ; sous-charts ou dépendances pour PostgreSQL et Kafka (dev seulement).
4. **Ingress** avec TLS local, gestion des secrets (Sealed Secrets ou External Secrets ; documenter le choix).
5. Autoscaling **HPA** de la passerelle et test de charge (k6) montrant la montée en charge.
6. Mises à jour **progressives** et retour arrière : provoquer un déploiement défectueux et revenir en arrière.
7. Exercices CKAD : chronométrer 20 tâches (Jobs, CronJobs, probes, volumes, RBAC, Ingress) ; refaire celles dépassant 6 minutes.
8. Ajouter l'installation à la CI (chart linté, déployé sur kind, tests de fumée).

## Critères d'acceptation
- [ ] `helm install` seul fait fonctionner la pile ; `helm uninstall` nettoie tout
- [ ] Les pods tournent sans privilèges et passent un scan (`kubescape` ou `trivy`)
- [ ] Le HPA augmente les réplicas sous charge, test k6 joint
- [ ] Rollback réussi en moins de 2 minutes
- [ ] Au moins 80 % des exercices CKAD faits dans le temps

## Pour aller plus loin
Déploiement GitOps (Argo CD ou Flux) sur kind.

## Ressources
- Kubernetes : <https://kubernetes.io/docs/> · kind : <https://kind.sigs.k8s.io/> · Helm : <https://helm.sh/docs/>
- CKAD : <https://training.linuxfoundation.org/certification/certified-kubernetes-application-developer-ckad/> · simulateur <https://killer.sh>
