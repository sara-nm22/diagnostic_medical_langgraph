# Diagnostic Médical Multi-Agent avec LangGraph

Application d'**orientation diagnostique préliminaire** basée sur un système multi-agent.
Projet réalisé par **Sara Naim**.

> ⚠️ **Avertissement** : outil académique uniquement. Ne pas utiliser pour diagnostiquer de vrais patients.

## Technologies

| Technologie | Rôle |
|---|---|
| LangGraph | Orchestration des agents IA |
| FastAPI | API REST (backend) |
| Streamlit | Interface utilisateur (frontend) |
| MCP | Model Context Protocol pour les outils |

## Architecture

| Service | Port | Technologie | Rôle |
|---|---|---|---|
| Backend | 8000 | FastAPI | API REST |
| Frontend | 8501 | Streamlit | Interface |
| Debugging | 8123 | LangGraph Studio | Visualisation du graphe |

Le graphe LangGraph comporte quatre nœuds :

- **Supervisor** : orchestre le flux et choisit l'agent à activer
- **Diagnostic Agent** : pose les questions cliniques (interruption pour la réponse du patient)
- **Physician Review** : révise les hypothèses
- **Report Agent** : génère le rapport final structuré

Le rapport technique complet se trouve dans [`docs/rapport_technique.md`](docs/rapport_technique.md).

## Structure du projet

```
diagnostic-medical-langgraph/
├── backend/        # API FastAPI + graphe LangGraph (app/, nodes/, tools/)
├── frontend/       # Interface Streamlit
├── mcp_server/     # Serveur MCP (outils)
└── docs/           # Rapport technique
```

## Installation (Windows)

Prérequis : [Python 3.11+](https://www.python.org/downloads/) et [Git](https://git-scm.com).

```bash
git clone https://github.com/VOTRE-NOM/diagnostic-medical-langgraph.git
cd diagnostic-medical-langgraph

# Backend
cd backend
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
cd ..

# Frontend (dans un autre terminal, ou le même environnement)
pip install -r frontend/requirements.txt
```

## Lancement

**1. Backend** (depuis le dossier `backend`, environnement activé) :

```bash
uvicorn app.api:app --port 8000
```

Documentation Swagger : http://127.0.0.1:8000/docs

**2. Frontend** (depuis la racine du projet) :

```bash
streamlit run frontend/streamlit_app.py
```

Interface : http://localhost:8501

**3. (Optionnel) LangGraph Studio**, depuis `backend` :

```bash
pip install "langgraph-cli[inmem]"
langgraph dev --port 8123
```

## Configuration

Copiez `backend/.env.example` en `backend/.env` si vous voulez modifier des paramètres
(par exemple `MCP_SERVER_PATH`). Ne publiez jamais le fichier `.env`.

## Limitations

- Pas d'authentification (démo)
- Données stockées localement, pas de chiffrement (HTTP en local)
- Pour la production : HTTPS, JWT/OAuth2, base PostgreSQL, logs de sécurité, validation comme dispositif médical

## Licence

MIT, voir [LICENSE](LICENSE).
