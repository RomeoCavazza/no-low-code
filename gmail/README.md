# Gmail Automation - IA & Dashboard Web

> Automatisez votre Gmail avec OpenAI et visualisez vos emails via une interface web moderne.

**Architecture :** Gmail API → n8n → OpenAI GPT-3.5 → JSON → Interface Web

---

## ⚡ Quickstart (5 minutes)

### Prérequis
- Docker installé
- Compte Google (Gmail)
- Compte OpenAI avec crédits

### ⚠️ 4 points critiques avant de commencer

1. **Clone sparse** (gain 70% de bande passante)
2. **OAuth2 Gmail** : URLs exactes requises
3. **OpenAI API** : Générer une NOUVELLE clé
4. **Permissions Docker** : `chmod 777` AVANT docker-compose

---

## 🚀 Installation

### 1. Cloner le projet
```bash
git clone --depth 1 --filter=blob:none --sparse https://github.com/RomeoCavazza/no-low-code.git
cd no-low-code
git sparse-checkout set gmail
cd gmail
```

### 2. Préparer les permissions
```bash
docker run --rm -v "$(pwd)/front-page/data:/data" alpine sh -c "chmod -R 777 /data"
```
> ⚠️ **Sans cette étape** → Erreur "Forbidden by access permissions"

### 3. Lancer Docker
```bash
docker-compose up -d
# Attendre 30 secondes que n8n démarre
```

### 4. Accéder à n8n et importer le workflow
1. Ouvrir : **http://localhost:5678**
2. Menu (☰) → **Import from File**
3. Sélectionner : `json/workflow.json`
4. Cliquer **Import**

### 5. Configurer Gmail OAuth2

#### a) Google Cloud Console
1. [console.cloud.google.com](https://console.cloud.google.com/apis/credentials?project=gen-lang-client-0001397937) → Créer projet
2. Activer **Gmail API**
3. Créer **OAuth 2.0 Client ID** (Web application)
4. **⚠️ Authorized JavaScript origins :**
   ```
   http://localhost:5678
   ```
5. **⚠️ Authorized redirect URIs :**
   ```
   http://localhost:5678/rest/oauth2-credential/callback
   ```
6. **OAuth consent screen → Scopes :**
   ```
   https://www.googleapis.com/auth/gmail.readonly
   ```

#### b) Dans n8n
1. Cliquer sur le nœud **"Get many messages"** (Gmail)
2. Credential → **Create New**
3. Coller **Client ID** + **Client Secret**
4. **Connect my account** → Autoriser Gmail
5. ✅ Vérifier "Connected"

### 6. Configurer OpenAI
1. [platform.openai.com](https://platform.openai.com/api-keys) → **Copier immédiatement**
2. Dans n8n, cliquer sur le nœud **"Basic LLM Chain"**
3. Credential → **Create New**
4. Coller l'**API Key**
5. ✅ Sauvegarder

### 7. Tester
```bash
# Dans n8n : Cliquer "Test workflow"
# Vérifier la création du fichier :
cat front-page/data/mails-today.json
```

### 8. Activer & Utiliser
- Toggle **"Active"** → ON (exécution quotidienne 18h00)
- Interface web : http://localhost:8080
- Webhook manuel : `curl -X POST http://localhost:5678/webhook/refresh-mails`

---

## 🎯 Fonctionnalités

**Analyse IA**
- Résumé quotidien personnalisé
- Détection urgence (Faible/Moyenne/Forte)
- Emails prioritaires automatiques
- Thèmes clés extraits

**Interface Web**
- Dashboard avec résumé IA
- Recherche temps réel
- Filtres (expéditeur, épinglés, corbeille)
- Actions (épingler, archiver, supprimer)

**Automatisation**
- Exécution quotidienne (18h00)
- Déclenchement webhook/manuel
- Persistance locale (JSON)

---

## 🔗 URLs

| Service | URL |
|---------|-----|
| **Interface** | http://localhost:8080 |
| **n8n** | http://localhost:5678 |
| **JSON** | http://localhost:8080/data/mails-today.json |

---

## 🐛 Dépannage rapide

| Problème | Solution |
|----------|----------|
| "Forbidden by access permissions" | `docker run --rm -v "$(pwd)/front-page/data:/data" alpine sh -c "chmod -R 777 /data"` |
| OAuth2 Gmail ne connecte pas | Vérifier URLs exactes (voir étape 4) |
| "Invalid API Key" OpenAI | Générer nouvelle clé API |
| Interface vide | Exécuter workflow au moins 1 fois |
| LLM retourne null | Vérifier connexion "Basic LLM Chain" → "Merge Results" (port Input 2) |

**Problèmes détaillés ?** → Voir [rapport.md](rapport.md) section "Difficultés Rencontrées"

---

## 📖 Documentation

- **[README.md](README.md)** - Quickstart (ce fichier)
- **[rapport.md](rapport.md)** - Difficultés rencontrées & solutions techniques
- **[json/README.md](json/README.md)** - Configuration workflow n8n
- **[front-page/README.md](front-page/README.md)** - Documentation interface

---

## 🛠️ Commandes utiles

```bash
# Logs
docker-compose logs -f n8n

# Redémarrer
docker-compose restart

# Arrêter
docker-compose down

# Test permissions
docker exec n8n touch /files/test.txt && docker exec n8n rm /files/test.txt
```

---

## 📦 Structure

```
gmail/
├── README.md              # Quickstart
├── rapport.md             # Difficultés & solutions
├── docker-compose.yml     # Config Docker
├── json/
│   ├── workflow.json      # Workflow n8n
│   └── README.md
├── front-page/
│   ├── index.html
│   ├── assets/
│   ├── data/              # Généré automatiquement
│   └── README.md
└── screenshots/
```

---

**🎉 Prêt en 15 minutes** - [Voir les difficultés techniques](rapport.md)
