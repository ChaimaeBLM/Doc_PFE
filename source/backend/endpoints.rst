Endpoints API
=============

Ce backend expose plusieurs routes API via FastAPI, permettant d’interagir avec le système intelligent. Ci-dessous sont décrits les principaux endpoints.

.. contents::
   :local:
   :depth: 1

---

1. POST `/api/general-qa`
-------------------------

**Description :**  
Effectue un diagnostic général à partir d'une question utilisateur en exploitant un pipeline RAG.

**Requête JSON attendue** :

.. code-block:: json

    {
      "question": "Quels sont les principaux problèmes de la région ?",
      "session_id": "abc123",
      "user_id": "user456",
      "save_to_db": true
    }

**Réponse JSON** :

.. code-block:: json

    {
      "query": "Quels sont les principaux problèmes de la région ?",
      "answer": "Les principaux problèmes identifiés sont ...",
      "success": true,
      "session_id": "abc123",
      "sources": [
        {
          "filename": "rapport_region.pdf",
          "snippet": "Selon le rapport annuel, la région souffre de ...",
          "metadata": { "source": "chemin/rapport_region.pdf" }
        }
      ]
    }

**Comportement :**

- Valide que la question contient au moins 3 caractères.
- Utilise la fonction `handle_general_qa` pour le traitement.
- Peut sauvegarder la conversation si `save_to_db = true`.
- Renvoie les documents source utilisés par le module RAG (limité à 3).

---

2. POST `/api/diagnosis`
------------------------

**Description :**  
Lance un diagnostic sectoriel ou territorial à partir d’un besoin utilisateur.

**Requête JSON attendue** :

.. code-block:: json

    {
      "question": "Comment améliorer l'accès à l'eau potable dans cette province ?",
      "session_id": "abc123",
      "user_id": "user456",
      "save_to_db": true
    }

**Réponse JSON** :

Même structure que `/api/general-qa`, mais la logique métier passe par la fonction `handle_diagnosis`.

**Comportement :**

- Analyse le problème selon une approche sectorielle (éducation, santé, etc.).
- Renvoie une réponse structurée.
- Retourne une liste de sources contextuelles utilisées.

---

3. POST `/api/conversation-history`
-----------------------------------

**Description :**  
Récupère l’historique des messages pour une session spécifique.

**Requête JSON attendue** :

.. code-block:: json

    {
      "session_id": "abc123",
      "limit": 10
    }

**Réponse JSON** :

.. code-block:: json

    {
      "messages": [
        {
          "question": "Quels sont les projets en cours ?",
          "answer": "Actuellement, trois projets sont en cours ...",
          "timestamp": "2025-07-10T12:30:00Z"
        },
        ...
      ]
    }

**Comportement :**

- Utilise la fonction `get_conversation_history(session_id, limit)` pour interroger la base.
- Les messages sont triés dans l’ordre chronologique.

---

4. GET `/`
----------

**Description :**  
Endpoint de vérification d’état (health check).

**Réponse JSON** :

.. code-block:: json

    {
      "message": "AI Assistant backend is running!"
    }

**Utilité :**

- Permet de vérifier que le serveur est actif.
- Peut être utilisé dans des systèmes de supervision (ex. : Docker Healthcheck, monitoring).

---
