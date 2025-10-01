# Workflow n8n - Gmail Automation

## 🎯 Fonction
Workflow n8n pour récupérer les emails Gmail, les analyser avec OpenAI GPT-3.5-turbo, et générer un JSON exploitable.

## 🏗️ Architecture

```
Trigger (Schedule/Webhook/Manual)
    ↓
Gmail API - Get Messages (24h, hors promotions)
    ↓
Extract & Clean Data (JavaScript)
    ↓
OpenAI Analysis → JSON Summary
    ↓
Merge Results → Convert to Binary
    ↓
Write File → /files/mails-today.json
```

## 📊 Déclencheurs

- **Schedule** : Automatique quotidien à 18h00
- **Webhook** : `/webhook/refresh-mails` (depuis l'interface)
- **Manual** : Bouton "Test workflow" dans n8n

## 🔧 Configuration

### Credentials requises

**1. Gmail OAuth2**
- Scope : `gmail.readonly`
- URI redirection : `http://localhost:5678/rest/oauth2-credential/callback`

**2. OpenAI**
- Model : `gpt-3.5-turbo`
- Temperature : 0.7

### Paramètres du workflow

**Gmail query** : `newer_than:1d -category:promotions`  
**Output path** : `/files/mails-today.json`  
**Webhook path** : `/webhook/refresh-mails`

## 📤 Format de sortie

```json
{
  "day": "2025-10-01",
  "total": 15,
  "urgency_level": "moyenne",
  "tl_dr": "Résumé personnalisé...",
  "priority_emails": [
    {"id": "abc", "reason": "Réponse recruteur"}
  ],
  "key_topics": ["emploi", "sécurité"],
  "suggested_actions": ["Répondre au recruteur"],
  "emails": [...]
}
```

## 🚀 Installation

### 1. Import
Dans n8n : **Import from File** → `json/workflow.json`

### 2. Credentials
- Gmail OAuth2 : Créer dans Google Cloud Console
- OpenAI : Ajouter clé API

### 3. Test
- Exécuter manuellement
- Vérifier `/files/mails-today.json`

### 4. Activation
Toggle "Active" → Exécution automatique à 18h00

## 🐛 Dépannage

**LLM retourne null**  
→ Vérifier connexion "Basic LLM Chain" → "Merge Results"

**JSON parsing failed**  
→ Vérifier le prompt et température (0.7)

**File not found**  
→ Vérifier volume Docker : `./front-page/data:/files`

**Gmail quota exceeded**  
→ Espacer les exécutions, vérifier quotas Google Cloud

## 📊 Monitoring

```bash
# Logs
docker-compose logs -f n8n

# Test webhook
curl -X POST http://localhost:5678/webhook/refresh-mails
```

---
*Workflow n8n robuste - Prêt pour production*
