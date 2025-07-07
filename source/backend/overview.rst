Présentation du Backend
=======================

Le backend est construit en Python avec **FastAPI**. Il fournit des endpoints RESTful pour interagir avec le modèle LLM et la base de connaissances. Il comprend également une base de données PostgreSQL pour stocker les historiques de conversation et les métadonnées.

Principales fonctionnalités :

- Traitement des requêtes utilisateur via un pipeline RAG.
- Connexion avec un modèle de génération (ex. : Mistral ou Qwen).
- Stockage et récupération des documents avec FAISS ou Chroma.
- Intégration d’un module de reranking pour améliorer la pertinence des réponses.
- Utilisation de SQLAlchemy pour la gestion de la base de données.

