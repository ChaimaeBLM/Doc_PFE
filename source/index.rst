.. Documentation SmartGOV documentation master file, created by
   sphinx-quickstart on Sat Apr 12 13:50:00 2025.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Documentation SmartGOV 
====================================

Bienvenue à la documentation de *SmartGOV*! Un outil intelligent pour l'amélioration de l'aménagement territorial et la gouvernance.
Il est conçu pour aider les gouvernements locaux à prendre des décisions éclairées en matière d'aménagement du territoire!.

Cette documentation présente l'architecture, l'implémentation et l'utilisation de l'application. Le projet est divisé en deux parties principales :

- **Backend** : service API construit avec FastAPI, intégrant un système RAG et une base de données PostgreSQL.
- **Frontend** : interface utilisateur construite avec Gradio (ou Streamlit si changé), permettant d'interagir avec l'assistant.

.. toctree::
   :maxdepth: 4
   :caption: Table de matières:

   Traitement des Donnnées avec Aumentoolkit

  

.. toctree::
   :maxdepth: 2
   :caption: Backend

   backend/overview
   backend/architecture
   backend/endpoints
   backend/database
   backend/usage

.. toctree::
   :maxdepth: 2
   :caption: Frontend

   frontend/overview
   frontend/architecture
   frontend/components
   frontend/interactions
   frontend/usage

