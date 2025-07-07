Base de Données
===============

Le backend utilise **PostgreSQL** avec SQLAlchemy pour l’ORM. L’initialisation se fait via le fichier `init_db.py`.

Les modèles sont probablement définis dans un sous-module de `services` ou `models/`.

Fichiers clés :
- `init_db.py` : initialise la base.
- `conversation_service.py` : interagit avec les historiques de conversation.
- `.env` : contient l’URL de connexion à la base PostgreSQL :

