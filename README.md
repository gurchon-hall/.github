# Gurchon Hall

**Open-source tools for the [Vampire: The Eternal Struggle](https://www.vekn.net/) (VTES) community.**

*Outils open-source pour la communauté [Vampire: The Eternal Struggle](https://www.vekn.net/) (VTES).*

---

## What is this? / C'est quoi ?

Gurchon Hall is a personal project dedicated to building automated tooling around VTES Tournament
Winning Decks (TWD). The goal: scrape, validate, structure, and publish every tournament-winning
deck from the VEKN forum — making this data freely available to players, deck builders, and analysts.

*Gurchon Hall est un projet personnel dédié à la création d'outils automatisés autour des decks
gagnants de tournois VTES (TWD). L'objectif : scraper, valider, structurer et publier chaque deck
gagnant depuis le forum VEKN — rendant ces données librement accessibles aux joueurs, deckbuilders
et analystes.*

---

## Repositories / Dépôts

### [channel-ten](https://github.com/gurchon-hall/channel-ten)

**The engine.** Python CLI that scrapes tournament winning decks from the
[VEKN forum](https://www.vekn.net/forum/event-reports-and-twd), parses them into structured YAML,
validates card data against [KRCG](https://pypi.org/project/krcg/), and publishes new decks to the
community archive [GiottoVerducci/TWD](https://github.com/GiottoVerducci/TWD).

*Le moteur. CLI Python qui scrape les decks gagnants depuis le forum VEKN, les parse en YAML
structuré, valide les cartes via KRCG, et publie les nouveaux decks vers l'archive communautaire
GiottoVerducci/TWD.*

| | |
| --- | --- |
| **Stack** | Python 3.14, httpx, BeautifulSoup, Pydantic, ruamel.yaml |
| **Automation** | Daily scrape, weekly validation, weekly publish via GitHub Actions |
| **License** | MIT |

### [eternal-vigilance](https://github.com/gurchon-hall/eternal-vigilance)

**The archive.** Data repository holding every scraped TWD as a YAML file, organized by date
(`YYYY/MM/<event_id>.yaml`). Includes error triage directories for decks with invalid cards, date
mismatches, or unconfirmed winners. Also stores weekly publish reports.

*L'archive. Dépôt de données contenant chaque TWD scrapé au format YAML, organisé par date. Inclut
des répertoires de triage pour les decks comportant des erreurs, ainsi que les rapports de
publication hebdomadaires.*

| | |
| --- | --- |
| **Coverage** | 2014 — present |
| **Updated** | Daily (automated) |

### [tabriz-assembly](https://github.com/gurchon-hall/tabriz-assembly)

**The lab.** Machine learning and statistical exploration over VTES data. FastAPI backend with
PostgreSQL (SQLAlchemy + Alembic), currently in early development.

*Le labo. Exploration ML et statistique des données VTES. Backend FastAPI avec PostgreSQL,
actuellement en développement.*

| | |
| --- | --- |
| **Stack** | Python 3.14, FastAPI, SQLAlchemy, Alembic, PostgreSQL |
| **Status** | Early development / En développement |

---

## How it works / Comment ça marche

```text
VEKN Forum ──scrape──▸ channel-ten ──write──▸ eternal-vigilance (YAML archive)
                            │                         │
                        validate                  publish
                        (weekly)               (weekly PR)
                            │                         │
                            ▼                         ▼
                     errors / fixes         GiottoVerducci/TWD
                                            (community archive)

eternal-vigilance ──feed──▸ tabriz-assembly (ML / stats)
```

---

## For players / Pour les joueurs

- Browse tournament winning decks in structured YAML format in
  [eternal-vigilance](https://github.com/gurchon-hall/eternal-vigilance)
- Every deck includes: winner name, VEKN ID, event location, date, round format, player count, and
  full decklist with card counts
- Data is validated against the official VTES card database (KRCG)
- New decks from the VEKN forum are added automatically every day

*Parcourez les decks gagnants au format YAML structuré. Chaque deck inclut le nom du gagnant, l'ID
VEKN, le lieu, la date, le format et la liste complète. Les données sont validées contre la base
officielle KRCG. Les nouveaux decks sont ajoutés automatiquement chaque jour.*

## For developers / Pour les développeurs

- **channel-ten** is installable as a Python package (`pip install -e ".[dev]"`)
- Full CLI with subcommands: `scrape`, `parse`, `validate`, `publish`
- Usable as a Python library (`from channel_ten.scraper import scrape_forum`)
- Pre-commit hooks (ruff, pytest, CLI smoke tests), CI via GitHub Actions
- MIT licensed — contributions welcome

---

## Tech overview / Vue technique

| Tool | Purpose |
| --- | --- |
| Python 3.14 | Runtime |
| httpx | HTTP client |
| BeautifulSoup + lxml | HTML parsing |
| Pydantic | Data validation & models |
| ruamel.yaml | YAML I/O |
| KRCG | Official VTES card database |
| FastAPI | API backend (tabriz-assembly) |
| SQLAlchemy + Alembic | ORM & migrations |
| GitHub Actions | CI/CD & automation |
| ruff | Linting & formatting |
| pytest | Testing |

---

*Built with passion for the VTES community.* 🧛

*Construit avec passion pour la communauté VTES.* 🧛
