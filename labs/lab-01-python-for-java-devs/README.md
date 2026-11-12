# LAB-01 – Python pour développeurs Java

**Jalon** M0 · **Durée** ≈ 8 h · **Niveau** facile à moyen · **Livrable** `exercises/lab-01-python-for-java-devs/`

## Objectif
Écrire du Python de production (typé, testé, asynchrone), car un poste IA sur deux demande Python en plus de Java. Vous n'apprenez pas la syntaxe : vous apprenez les **réflexes de production** Python que vous avez déjà en Java (typage strict, injection, tests, migrations, conteneur).

## Prérequis
LAB-00 terminé (fichier d'instructions et workflow spec d'abord). Python 3.12+, `uv` (gestionnaire de projet Python), Docker.

## Étapes
Travailler avec votre agent comme au LAB-00 : spec courte, plan relu, petits commits, incidents consignés. Python est un terrain où l'agent produit vite du code « qui tourne » mais mal typé ou mal testé : c'est votre relecture qui compte.

1. Créer un projet avec `uv init`, un environnement virtuel, `ruff` (lint/format) et `mypy` ou `pyright` (typage strict). Ajouter à vos instructions d'agent une section Python (commandes `uv run ruff check`, `uv run mypy`, `uv run pytest`, règle « pas de `Any` sans justification », fichier ciblé `applyTo: '**/*.py'` côté Copilot ou `.claude/rules/` côté Claude Code).
2. Écrire une API **FastAPI** `contracts` : `GET/POST /contracts`, modèles **Pydantic** (validation, énumérations), erreurs HTTP propres.
3. Remplacer la persistance en mémoire par **SQLAlchemy 2 + PostgreSQL** (Docker), avec migrations **Alembic**.
4. Ajouter des tests **pytest** : unitaires, API (`TestClient`/`httpx`), base via Testcontainers pour Python.
5. Introduire de l'asynchrone : endpoint qui appelle deux services externes simulés en parallèle avec `asyncio.gather`, timeouts et gestion d'erreurs.
6. Écrire un tableau « Java → Python » (records ↔ dataclasses/Pydantic, Optional ↔ `X | None`, Streams ↔ compréhensions, DI Spring ↔ `Depends`).
7. Dockeriser l'API (image minimale, utilisateur non-root, dépendances figées par `uv.lock`) et ajouter la CI GitHub Actions (lint, types, tests, build de l'image).

## Critères d'acceptation
- [ ] `ruff`, le vérificateur de types (mode strict) et `pytest` passent en CI
- [ ] Couverture ≥ 80 %
- [ ] L'API valide ses entrées et renvoie des erreurs structurées (code, message, détail) ; aucune stack trace côté client
- [ ] Les migrations Alembic montent **et** redescendent proprement sur une base vide (test)
- [ ] Un test prouve que les appels parallèles sont plus rapides que séquentiels, et qu'un timeout est correctement géré
- [ ] Le tableau « Java → Python » est écrit avec au moins 8 lignes, chacune illustrée par un extrait de code de votre projet
- [ ] Image Docker construite, exécutée sans privilèges ; taille notée

## Pour aller plus loin
Streaming SSE avec FastAPI (utile pour LAB-02 et LAB-08). Comparer `mypy` et `pyright` sur votre code et noter ce que chacun détecte en plus.

## Ressources
- uv : <https://docs.astral.sh/uv/> · FastAPI : <https://fastapi.tiangolo.com> · Pydantic : <https://docs.pydantic.dev> · pytest : <https://docs.pytest.org>
- SQLAlchemy 2 : <https://docs.sqlalchemy.org> · Alembic : <https://alembic.sqlalchemy.org> · asyncio : <https://docs.python.org/3/library/asyncio.html>
- Ruff : <https://docs.astral.sh/ruff/> · mypy : <https://mypy.readthedocs.io>
- Testcontainers : <https://testcontainers.com/guides/>
