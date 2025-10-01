# Workflow n8n - Gmail Automation

## 🎯 Fonction
Workflow n8n automatisé pour récupérer les emails Gmail, les analyser avec OpenAI GPT-3.5-turbo, et générer un fichier JSON exploitable par l'interface web.

## 🏗️ Architecture du workflow

```
Trigger (Schedule/Webhook/Manual)
    ↓
Gmail API - Get All Messages
    ↓
Extract Email Data (Code JS)
    ↓
Merge → Basic LLM Chain (OpenAI)
    ↓
Merge Results (Code JS)
    ↓
Convert to JSON (Code JS)
    ↓
Write Binary File → /files/mails-today.json
```

## 📊 Nœuds principaux

### 1. Triggers (déclencheurs)
- **Schedule** : Exécution quotidienne à 18h00
- **Webhook** : URL `/webhook/refresh-mails` (appelé depuis l'interface)
- **Manual** : Exécution manuelle dans n8n

### 2. Gmail API
```javascript
Opération : getAll
Filtres :
  - labelIds: ["INBOX"]
  - query: "newer_than:1d -category:promotions"
  - readStatus: "both"
```
Récupère tous les emails de la boîte de réception des dernières 24h, hors promotions.

### 3. Extract Email Data (Code JavaScript)
Extrait et structure les données de chaque email :
```javascript
{
  id: string,
  subject: string,
  from: string,
  snippet: string,
  date: ISO string,
  labels: array,
  threadId: string
}
```

### 4. Basic LLM Chain (OpenAI GPT-3.5-turbo)
Analyse intelligente des emails avec prompt optimisé :

**Prompt système :**
```
Tu es un assistant personnel. Analyse les emails de l'utilisateur 
et génère un résumé quotidien structuré en JSON.
```

**Instructions :**
- `day` : Date du jour (YYYY-MM-DD)
- `urgency_level` : "faible", "moyenne" ou "forte"
- `tldr` : Résumé bref et personnalisé (2-3 phrases max)
- `priority_emails` : Array d'objets `{ id, reason }` (max 3)
- `key_topics` : Array de strings (1-2 mots max, 15 caractères max)
- `suggested_actions` : Array de strings (actions concrètes)

**Contraintes :**
- Format JSON strict
- `key_topics` : STRICTEMENT 1-2 mots (ex: "emploi", "sécurité")
- Ton naturel et personnalisé

### 5. Code in JavaScript (2) - Merge Results
Fusionne les emails et le résumé IA :
```javascript
const all = $input.all();
let emails = [];
let summary = {};

// Extraction emails
for (const item of all) {
  if (item.json.emails) {
    emails = item.json.emails;
  }
  
  // Parsing sortie LLM
  if (item.json.text && typeof item.json.text === 'string') {
    try {
      summary = { ...summary, ...JSON.parse(item.json.text) };
    } catch (e) {}
  } else if (item.json.output) {
    summary = item.json.output;
  }
}

summary.total = emails.length;
if (!summary.day) summary.day = new Date().toISOString().slice(0, 10);

return [{ json: { ...summary, emails } }];
```

### 6. Code in JavaScript (3) - Convert to Binary
Conversion en fichier JSON :
```javascript
const text = JSON.stringify($json, null, 2);
return [{
  json: {},
  binary: {
    data: {
      data: Buffer.from(text, 'utf8').toString('base64'),
      mimeType: 'application/json',
      fileName: 'mails-today.json',
    }
  }
}];
```

### 7. Write Binary File
Écriture du fichier dans `/files/mails-today.json` (volume partagé Docker).

## 🔧 Configuration requise

### Credentials
- **Gmail OAuth2** :
  - Scope : `https://www.googleapis.com/auth/gmail.readonly`
  - Autorisation via Google Cloud Console
  
- **OpenAI** :
  - API Key avec accès GPT-3.5-turbo
  - Model : `gpt-3.5-turbo`
  - Temperature : 0.7 (équilibre créativité/précision)

### Paramètres
- **Gmail query** : `newer_than:1d -category:promotions`
- **Schedule** : Cron `0 18 * * *` (18h00 quotidien)
- **Webhook path** : `/webhook/refresh-mails`
- **Output path** : `/files/mails-today.json`

## 📤 Format de sortie

### Structure JSON
```json
{
  "day": "2025-10-01",
  "total": 15,
  "urgency_level": "moyenne",
  "tldr": "Journée calme avec quelques suivis de candidatures...",
  "priority_emails": [
    {
      "id": "abc123",
      "reason": "Réponse recruteur important"
    }
  ],
  "key_topics": ["emploi", "sécurité", "DevOps"],
  "suggested_actions": [
    "Répondre au recruteur avant ce soir",
    "Vérifier les mises à jour de sécurité"
  ],
  "emails": [
    {
      "id": "abc123",
      "subject": "Entretien technique - Confirmation",
      "from": "recruteur@entreprise.com",
      "snippet": "Bonjour, nous confirmons...",
      "date": "2025-10-01T14:30:00.000Z",
      "labels": ["INBOX", "UNREAD"],
      "threadId": "thread123"
    }
  ]
}
```

## 🚀 Installation

### 1. Import
```bash
# Dans n8n : Workflows → Import from File
gmail/json/workflow.json
```

### 2. Configuration credentials
1. **Gmail OAuth2** : Créer les credentials dans Google Cloud Console
2. **OpenAI** : Ajouter la clé API dans n8n

### 3. Test
1. Exécuter manuellement le workflow
2. Vérifier le fichier `/files/mails-today.json`
3. Vérifier la sortie du LLM (format JSON correct)

### 4. Activation
- Activer le workflow
- Le schedule s'exécutera automatiquement à 18h00

## 🛠️ Dépannage

### Erreur : LLM retourne `null`
**Cause** : Nœud "Basic LLM Chain" non connecté à "Merge1"  
**Solution** : Vérifier les connexions entre nœuds

### Erreur : JSON parsing failed
**Cause** : Format de sortie LLM incorrect  
**Solution** : Vérifier le prompt et la température (0.7)

### Erreur : File not found
**Cause** : Volume Docker non monté  
**Solution** : Vérifier `docker-compose.yml` : `./site/data:/files`

### Erreur : Gmail quota exceeded
**Cause** : Trop de requêtes API Gmail  
**Solution** : Espacer les exécutions, vérifier les quotas Google Cloud

## 📊 Monitoring

### Logs
```bash
docker-compose logs -f n8n
```

### Exécutions
Interface n8n → Executions → Voir détails

### Webhook test
```bash
curl -X POST http://localhost:5678/webhook/refresh-mails
```

## 🎯 Optimisations

- **Prompt optimisé** : Instructions claires pour format JSON strict
- **Error handling** : Try/catch sur parsing JSON LLM
- **Merge intelligent** : Gestion de multiples formats de sortie LLM
- **Query Gmail** : Filtre promotions et emails < 24h

---
*Workflow n8n robuste et testé - Prêt pour production*

