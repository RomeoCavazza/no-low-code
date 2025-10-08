# Gmail Automation - IA & Dashboard Web

Automatisation Gmail avec analyse OpenAI et interface web moderne.

**Architecture** : Gmail API → n8n → OpenAI GPT-3.5 → JSON → Interface Web

## Installation

### Prérequis
- Docker
- Compte Google (Gmail)
- Compte OpenAI avec crédits

### 1. Cloner et préparer
```bash
git clone --depth 1 --filter=blob:none --sparse https://github.com/RomeoCavazza/no-low-code.git
cd no-low-code && git sparse-checkout set gmail && cd gmail
docker run --rm -v "$(pwd)/front-page/data:/data" alpine sh -c "chmod -R 777 /data"
```

### 2. Démarrer
```bash
docker-compose up -d
# Attendre 30 secondes
```

### 3. Configurer n8n
1. Ouvrir http://localhost:5678
2. Menu → Import from File → `json/workflow.json`

### 4. Configurer credentials

**Gmail OAuth2** :
- Google Cloud Console → Créer projet → Activer Gmail API
- OAuth 2.0 Client ID (Web app)
- Authorized origins : `http://localhost:5678`
- Redirect URI : `http://localhost:5678/rest/oauth2-credential/callback`
- Scope : `https://www.googleapis.com/auth/gmail.readonly`
- Dans n8n : nœud "Get many messages" → Create credential → Connecter

**OpenAI** :
- Créer API key sur [platform.openai.com](https://platform.openai.com/api-keys)
- Dans n8n : nœud "Basic LLM Chain" → Create credential → Coller key

### 5. Tester et activer
```bash
# Test dans n8n : Bouton "Test workflow"
cat front-page/data/mails-today.json

# Activer workflow : Toggle "Active" → ON
# Webhook manuel : curl -X POST http://localhost:5678/webhook/refresh-mails
```

## Accès

| Service | URL |
|---------|-----|
| Interface web | http://localhost:8080 |
| n8n | http://localhost:5678 |
| JSON généré | http://localhost:8080/data/mails-today.json |

## Documentation

- `rapport.md` - Difficultés techniques rencontrées
- `json/README.md` - Configuration workflow n8n
- `front-page/README.md` - Documentation interface
