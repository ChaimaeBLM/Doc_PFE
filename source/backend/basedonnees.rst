Base de Données
===============

Le backend repose sur **PostgreSQL** comme système de gestion de base de données, avec **SQLAlchemy** comme ORM (Object Relational Mapping).

Ce module définit deux modèles principaux : `Conversation` et `Message`, qui permettent de gérer les sessions de chat et l'historique des échanges.

Modèles SQLAlchemy
------------------

Conversation
~~~~~~~~~~~~

Le modèle `Conversation` représente une session de discussion entre l'utilisateur et le chatbot.

.. code-block:: python

    class Conversation(Base):
        __tablename__ = "conversations"

        id = Column(Integer, primary_key=True, index=True)
        session_id = Column(String(255), unique=True, index=True)
        user_id = Column(String(255), nullable=True)
        title = Column(String(500), nullable=True)
        created_at = Column(DateTime, default=datetime.utcnow)
        updated_at = Column(DateTime, default=datetime.utcnow, onupdate=datetime.utcnow)

        messages = relationship("Message", back_populates="conversation", cascade="all, delete-orphan")

**Champs :**

- `id` : identifiant unique de la conversation.
- `session_id` : identifiant de session (UUID ou équivalent).
- `user_id` : identifiant utilisateur (optionnel).
- `title` : titre de la conversation (affichage côté frontend).
- `created_at` / `updated_at` : timestamps de création et de mise à jour.
- `messages` : relation avec les objets `Message`.

Message
~~~~~~~

Le modèle `Message` stocke les échanges individuels au sein d'une conversation.

.. code-block:: python

    class Message(Base):
        __tablename__ = "messages"

        id = Column(Integer, primary_key=True, index=True)
        conversation_id = Column(Integer, ForeignKey("conversations.id"))
        question = Column(Text, nullable=False)
        answer = Column(Text, nullable=False)
        context_used = Column(Text, nullable=True)
        chat_type = Column(String(50), nullable=False)
        timestamp = Column(DateTime, default=datetime.utcnow)

        conversation = relationship("Conversation", back_populates="messages")

**Champs :**

- `id` : identifiant unique du message.
- `conversation_id` : clé étrangère vers `Conversation`.
- `question` : texte de la question posée.
- `answer` : texte de la réponse générée.
- `context_used` : contenu contextuel utilisé par le module RAG.
- `chat_type` : type de tâche ("general", "diagnostic", etc.).
- `timestamp` : date de création du message.

Connexion à la base de données
------------------------------

URL de connexion PostgreSQL :

.. code-block:: python

    DATABASE_URL = os.getenv(
        "DATABASE_URL",
        "postgresql://postgres:Cboualam2000@localhost:5432/rag_webapp"
    )

Elle peut être définie dans un fichier `.env`.

Initialisation des tables :

.. code-block:: python

    def create_tables():
        Base.metadata.create_all(bind=engine)

Cette fonction crée toutes les tables si elles n'existent pas encore.

Gestion des sessions avec SQLAlchemy :

.. code-block:: python

    def get_db():
        db = SessionLocal()
        try:
            yield db
        finally:
            db.close()

