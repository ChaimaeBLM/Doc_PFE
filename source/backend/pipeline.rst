Chaîne RAG (Retrieval-Augmented Generation)
===========================================

Ce module implémente le pipeline principal de génération augmentée par récupération (**RAG**) en utilisant **LangChain**. Il permet de créer deux types de chaînes :

- Une chaîne RAG simple (`get_rag_chain`)
- Une chaîne RAG avec reranking (`get_rag_chain_with_reranker`)

Les fonctions exploitent un modèle LLM (Mistral ou fine-tuné) ainsi qu'un index vectoriel FAISS chargé via `load_vectorstore_faiss()`.

Imports et Initialisation
-------------------------

.. code-block:: python

    llm = load_llm()
    llm_finetune = load_llm_finetune()
    retriever = load_vectorstore_faiss().as_retriever(search_kwargs={"k": 5})
    vectorstore = load_vectorstore_faiss()

- `llm` : modèle de génération standard.
- `llm_finetune` : version fine-tunée pour tâches spécialisées.
- `retriever` : récupérateur initial basé sur FAISS (top-5 par défaut).
- `vectorstore` : accès direct à la base vectorielle FAISS.

Chaîne RAG avec reranking
-------------------------

.. code-block:: python

    def get_rag_chain_with_reranker(llm, prompt, top_k_retrieval=5, top_k_rerank=3):
        ...

Cette fonction configure une chaîne `RetrievalQA` utilisant un reranker basé sur un **CrossEncoder** (`ms-marco-MiniLM-L-6-v2`).

Étapes du pipeline :
1. **Récupération initiale** : top-k documents depuis FAISS.
2. **Reranking** : classement des documents selon leur pertinence vis-à-vis de la requête via un CrossEncoder.
3. **Sélection finale** : top-k reranked documents sont passés au modèle LLM.

### RerankedRetriever (interne)

Une classe personnalisée `RerankedRetriever` hérite de `BaseRetriever` et surcharge la méthode `_get_relevant_documents`.

.. code-block:: python

    class RerankedRetriever(BaseRetriever):
        def _get_relevant_documents(query: str, ...) -> List[Document]:
            ...

