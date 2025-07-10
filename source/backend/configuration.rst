Configuration du Backend
========================

Ce fichier contient les constantes de configuration utilisées par les différents composants du backend (modèle LLM, vecteurs, embeddings, etc.). Il centralise les chemins vers les modèles, les documents sources, et les paramètres de découpage de texte pour l’indexation RAG.

Chemins des Modèles
-------------------

.. code-block:: python

    MODEL_PATH = "models/mistral-7b-instruct-v0.1.Q4_K_M.gguf"

Modèle de génération principal utilisé pour répondre aux questions. Il s'agit d'une version quantifiée (Q4_K_M) du modèle **Mistral-7B Instruct**, au format GGUF, compatible avec des exécutions optimisées (ex. : `llama.cpp`, `llama-cpp-python`, ou `ctransformers`).

.. code-block:: python

    FINETUNED_MODEL_PATH = "models/unsloth.F16.gguf"

Modèle fine-tuné sur une tâche spécifique, probablement avec QLoRA ou Unsloth. Utilisé pour des cas d’usage spécialisés (ex. : suggestion de projets ou diagnostic sectoriel).

Paramètres RAG
--------------

.. code-block:: python

    CHROMA_DB_DIR = "chroma_db"

Chemin vers le dossier contenant la base vectorielle **ChromaDB**. Cette base stocke les représentations vectorielles des documents pour la phase de récupération (Retriever).

.. code-block:: python

    EMBEDDING_MODEL = "dangvantuan/sentence-camembert-base"

Modèle utilisé pour générer les embeddings textuels. Ici, un modèle **CamemBERT** optimisé pour la langue française, compatible avec `sentence-transformers`.

.. code-block:: python

    SOURCE_DOCS_PATH = "data"

Répertoire contenant les documents sources utilisés pour la vectorisation. Tous les fichiers dans ce dossier sont segmentés puis vectorisés pour être indexés dans ChromaDB.

Découpage des documents
------------------------

.. code-block:: python

    CHUNK_SIZE = 1000
    CHUNK_OVERLAP = 50

Ces deux paramètres sont utilisés pour diviser les documents textes avant leur vectorisation :

- `CHUNK_SIZE` : taille maximale (en caractères) de chaque segment de texte (chunk).
- `CHUNK_OVERLAP` : nombre de caractères de chevauchement entre deux segments consécutifs pour éviter les pertes de contexte.

Ces réglages sont essentiels pour améliorer la qualité des résultats lors de l'interrogation RAG, notamment avec `RecursiveCharacterTextSplitter` de LangChain.

Résumé
------

+----------------------+-------------------------------------------------------------+
| **Paramètre**        | **Description**                                             |
+======================+=============================================================+
| `MODEL_PATH`         | Modèle principal (instruct Mistral 7B quantifié)           |
| `FINETUNED_MODEL_PATH` | Modèle fine-tuné spécialisé (ex. : projet, diagnostic)     |
| `CHROMA_DB_DIR`      | Répertoire des vecteurs ChromaDB                           |
| `EMBEDDING_MODEL`    | Modèle d’embedding CamemBERT pour le français              |
| `SOURCE_DOCS_PATH`   | Répertoire des documents sources                           |
| `CHUNK_SIZE`         | Longueur des segments de texte (en caractères)             |
| `CHUNK_OVERLAP`      | Chevauchement entre segments pour ne pas perdre de contexte |
+----------------------+-------------------------------------------------------------+

