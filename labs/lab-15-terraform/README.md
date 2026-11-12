# LAB-15 – Terraform (optionnel)

**Jalon** M4 · **Durée** ≈ 10 h · **Niveau** moyen · **Livrable** `agentgate/deploy/terraform/`

## Objectif
Provisionner l'infrastructure cible en code (cluster managé, base, réseau). À faire seulement si votre cible de missions l'exige : Terraform apparaît dans 12 % des annonces Java + IA.

## Prérequis
LAB-14, un compte cloud avec **budget et alertes de coût activés** avant toute création de ressource.

## Étapes
1. Suivre les tutoriels Terraform de base (providers, variables, état, modules).
2. Écrire un module qui crée un cluster Kubernetes managé minimal (ou un environnement équivalent) et une base PostgreSQL managée.
3. Backend d'état distant verrouillé ; variables sensibles hors du dépôt.
4. `terraform plan` en CI sur chaque pull request, `apply` manuel protégé.
5. Déployer le chart du LAB-14, vérifier, puis **détruire** (`terraform destroy`) et confirmer l'absence de ressources résiduelles.

## Critères d'acceptation
- [ ] Création et destruction reproductibles en une commande
- [ ] Aucun secret dans l'état versionné ni dans le dépôt
- [ ] Coût total du TP documenté et < 10 €

## Ressources
- Terraform : <https://developer.hashicorp.com/terraform/tutorials>
