# n8n – Lokales Setup (Docker)

Beispiel `.env`:
```
N8N_PROTOCOL=http
N8N_HOST=127.0.0.1
N8N_PORT=5678
N8N_SECURE_COOKIE=false
N8N_EDITOR_BASE_URL=http://127.0.0.1:5678
WEBHOOK_URL=http://127.0.0.1:5678/
```

Hinweise: Browser **hart neuladen** bei Cookie-Warnung; bei „Error connecting to n8n“ Editor/Base-URL prüfen; Redirects & `User-Agent` in HTTP-Nodes setzen.
