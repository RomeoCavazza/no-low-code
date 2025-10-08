# Workflow n8n - Gmail Automation

Workflow pour récupérer emails Gmail, analyser avec OpenAI, et générer JSON.

## Architecture

```
Trigger (Schedule/Webhook/Manual)
    ↓
Gmail API - Get Messages (24h)
    ↓
Extract & Clean Data
    ↓
OpenAI Analysis → JSON
    ↓
Write File → /files/mails-today.json
```

## Déclencheurs

- **Schedule** : Quotidien à 18h00
- **Webhook** : `/webhook/refresh-mails`
- **Manual** : Bouton "Test workflow"

## Configuration

### 1. Import
n8n → Menu → Import from File → `json/workflow.json`

### 2. Credentials
Voir les instructions détaillées dans le [README principal](../README.md#4-configurer-credentials)

## Monitoring

```bash
# Logs
docker-compose logs -f n8n

# Test webhook
curl -X POST http://localhost:5678/webhook/refresh-mails
```
