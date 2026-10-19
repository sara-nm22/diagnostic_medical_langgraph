# Rapport technique : Diagnostic Médical Multi-Agent avec LangGraph

**Réalisé par : Sara Naim**

## 1. Introduction

Le projet « Diagnostic Médical » démontre l'utilisation de LangGraph pour créer un système multi-agent d'orientation diagnostique préliminaire.

Technologies : LangGraph (orchestration d'agents IA), FastAPI (API REST), Streamlit (interface), MCP (Model Context Protocol pour les outils).

> ⚠️ Outil académique. Ne pas utiliser pour diagnostiquer des patients réels.

## 2. Architecture générale

### 2.1 Composants principaux

| Service | Port | Technologie | Rôle |
|---|---|---|---|
| Backend | 8000 | FastAPI | API REST |
| Frontend | 8501 | Streamlit | Interface |
| Debugging | 8123 | LangGraph Studio | Visualisation |

### 2.2 Flux d'exécution

1. L'utilisateur entre un cas patient via Streamlit
2. Le frontend envoie une requête `POST /consultation/start`
3. FastAPI invoque le graphe LangGraph
4. Le Supervisor orchestre et active les agents
5. Le Diagnostic Agent génère une question
6. Le graphe s'interrompt et demande une réponse
7. Streamlit affiche la question et attend la réponse
8. `POST /consultation/resume` reprend le graphe

## 3. Composants techniques

### 3.1 FastAPI (backend)
Framework web moderne pour construire des APIs REST en Python : performance élevée (async native), documentation Swagger automatique, validation de données robuste.

### 3.2 Streamlit (frontend)
Création rapide d'applications web pour l'IA : développement rapide, hot-reload, gestion d'état avec `session_state`, composants pré-construits.

### 3.3 LangGraph
Framework multi-agent avec contrôle explicite du flux : graphe d'état visualisable, interruptions natives pour interactions humaines, persistance par checkpoints, Studio pour le debugging.

## 4. Flux du graphe LangGraph

| Nœud | Rôle | Sortie |
|---|---|---|
| Supervisor | Orchestre le flux, décide quel agent activer | Nom du nœud suivant |
| Diagnostic Agent | Pose des questions cliniques | Questions / interruption |
| Physician Review | Révise les hypothèses | Critique / validation |
| Report Agent | Génère le rapport final | Rapport structuré |

## 5. Choix technologiques

- **LangGraph** : flux explicite et debuggable, interruptions humaines, checkpoints, visualisation en temps réel
- **FastAPI** : asynchrone natif, Swagger automatique, validation Pydantic, écosystème Python riche
- **Streamlit** : rapidité de développement, pas de framework frontend (React, Vue), hot-reload

## 6. Sécurité et limitations

**Limitations actuelles** : pas d'authentification, données stockées localement, pas de chiffrement (HTTP en local), outil académique uniquement.

**Pour la production** : HTTPS/SSL, JWT ou OAuth2, base de données PostgreSQL, logs de sécurité, validation comme dispositif médical si nécessaire.

## 7. Conclusion

Le projet démontre comment intégrer LangGraph, FastAPI et Streamlit pour créer une application d'IA multi-agent complète : architecture modulaire et découplée, orchestration intelligente, interface intuitive, potentiel d'extension (support client, assistants légaux, recommandation, automatisation de processus métier).
