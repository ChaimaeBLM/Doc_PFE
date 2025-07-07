Endpoints API
=============

Les routes de l’API sont définies dans le dossier `api/`.

Exemples (à adapter à ton code exact) :

**POST** `/chat/general`
- Utilise `GeneralChat` dans `services/tasks/GeneralChat.py`.
- Reçoit une question utilisateur, renvoie une réponse générée par le modèle.

**POST** `/chat/diagnostic`
- Utilise `TerritoryDiagnosisService`, basé sur des documents de diagnostic territorial vectorisés.

**POST** `/chat/projet`
- Utilise `ProjectEvaluationService` pour évaluer la faisabilité d’un projet ou en suggérer un.

