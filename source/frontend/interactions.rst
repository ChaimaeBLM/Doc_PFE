Interaction Frontend <-> Backend
================================

1. L’utilisateur saisit une requête.
2. L’application appelle `/chat/general` ou un autre endpoint selon le mode.
3. La réponse est affichée dans le chat.

Exemple avec `requests` :

```python
import requests

response = requests.post(
    "http://localhost:8000/chat/general",
    json={"question": "Quels sont les enjeux de la région ?"}
)
print(response.json())
