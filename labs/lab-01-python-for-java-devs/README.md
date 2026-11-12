# LAB-01 – Python pour développeurs Java

**Jalon** M0 · **Durée** ≈ 8 h · **Niveau** facile à moyen

## Objectif
Écrire du Python de production (typé, testé, asynchrone), car un poste IA sur deux demande Python en plus de Java.

## Prérequis
LAB-00 terminé. Installer `uv` (gestionnaire de projet Python).

## Étapes
1. Créer un projet avec `uv init`, un environnement virtuel, `ruff` (lint/format) et `mypy` ou `pyright` (typage).
2. Écrire une API **FastAPI** `contracts` : `GET/POST /contracts`, modèles **Pydantic** (validation, énumérations), erreurs HTTP propres.
3. Remplacer la persistance en mémoire par **SQLAlchemy 2 + PostgreSQL** (Docker), avec migrations **Alembic**.
4. Ajouter des tests **pytest** : unitaires, API (`TestClient`/`httpx`), base via Testcontainers pour Python.
5. Introduire de l'asynchrone : endpoint qui appelle deux services externes simulés en parallèle avec `asyncio.gather`, timeouts et gestion d'erreurs.
6. Écrire un tableau « Java → Python » (records ↔ dataclasses/Pydantic, Optional ↔ `X | None`, Streams ↔ compréhensions, DI Spring ↔ `Depends`).
7. Dockeriser l'API (image minimale) et ajouter la CI.

## Critères d'acceptation
- [ ] `ruff`, le vérificateur de types et `pytest` passent en CI
- [ ] Couverture ≥ 80 %
- [ ] L'API valide ses entrées et renvoie des erreurs structurées
- [ ] Un test prouve que les appels parallèles sont plus rapides que séquentiels

## Pour aller plus loin
Streaming SSE avec FastAPI (utile pour LAB-02 et LAB-08).

## Ressources
- uv : <https://docs.astral.sh/uv/> · FastAPI : <https://fastapi.tiangolo.com> · Pydantic : <https://docs.pydantic.dev> · pytest : <https://docs.pytest.org>
- Testcontainers : <https://testcontainers.com/guides/>
