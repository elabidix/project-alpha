# LAB-15 – Terraform (optionnel)

**Jalon** M4 · **Durée** ≈ 10 h · **Niveau** moyen · **Livrable** `agentgate/deploy/terraform/`

## Objectif
Provisionner l'infrastructure cible en code (cluster managé, base, réseau). À faire seulement si votre cible de missions l'exige : Terraform apparaît dans 12 % des annonces Java + IA.

## Prérequis
LAB-14, un compte cloud avec **budget et alertes de coût activés** avant toute création de ressource.

## Étapes
1. Suivre les tutoriels Terraform de base (providers, variables, état, modules).
2. Écrire un module qui crée un cluster Kubernetes managé minimal (ou un environnement équivalent) et une base PostgreSQL managée. Étiqueter (`tags`) toutes les ressources (projet, propriétaire, TP) pour retrouver d'éventuels résidus.
3. Backend d'état distant verrouillé ; variables sensibles hors du dépôt (jamais de valeur par défaut pour un secret, `sensitive = true`).
4. Analyse statique du code : `terraform fmt`, `terraform validate`, plus un scanner de sécurité (`tflint`, `trivy config` ou `checkov`) ; corriger ou justifier chaque alerte.
5. `terraform plan` en CI sur chaque pull request, `apply` manuel protégé par approbation humaine ; le plan est relu comme un diff de code.
6. Déployer le chart du LAB-14, vérifier, puis **détruire** (`terraform destroy`) et confirmer l'absence de ressources résiduelles (inventaire par tags dans la console du fournisseur).

## Critères d'acceptation
- [ ] Création et destruction reproductibles en une commande
- [ ] Aucun secret dans l'état versionné ni dans le dépôt
- [ ] `validate` et le scanner de sécurité passent en CI ; les exceptions sont justifiées par écrit
- [ ] Aucune ressource résiduelle après `destroy` (preuve : inventaire par tags)
- [ ] Coût total du TP documenté et < 10 €

## Pour aller plus loin
Comparer avec OpenTofu, ou ajouter un environnement `dev` / `prod` avec le même module et des variables différentes.

## Ressources
- Terraform : <https://developer.hashicorp.com/terraform/tutorials>
- Trivy : <https://trivy.dev> · TFLint : <https://github.com/terraform-linters/tflint> · Checkov : <https://www.checkov.io>
