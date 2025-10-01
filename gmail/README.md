# Gmail Automation - IA & Dashboard Web

## 🎯 Fonction
Système complet d'automatisation Gmail avec analyse IA pour gérer et visualiser vos emails via une interface web moderne.

## 🏗️ Architecture
```
Gmail API → n8n Workflow → OpenAI GPT-3.5 → JSON → Interface Web
```

---

## 🚀 Quickstart

### 1. Cloner le projet
```bash
git clone https://github.com/RomeoCavazza/no-low-code.git
cd no-low-code/gmail
```

### 2. Lancer Docker
```bash
docker-compose up -d
# Attendre 30 secondes
```

### 3. Accéder à n8n
```
http://localhost:5678
```

### 4. Importer le workflow
- Import from File → `json/workflow.json`

### 5. Configurer Gmail OAuth2
1. [Google Cloud Console](https://console.cloud.google.com/) → Créer projet
2. Activer **Gmail API**
3. Créer credentials **OAuth 2.0 Web Application**
4. URI de redirection : `http://localhost:5678/rest/oauth2-credential/callback`
5. Dans n8n : Credentials → Gmail OAuth2 → Connecter

### 6. Configurer OpenAI
1. [OpenAI Platform](https://platform.openai.com/api-keys) → Créer clé API
2. Dans n8n : Credentials → OpenAI → Coller la clé

### 7. Activer le workflow
Toggle "Active" → ON (bleu)

### 8. Tester
```bash
# Dans n8n : cliquer "Test workflow"
# OU via curl :
curl -X POST http://localhost:5678/webhook/refresh-mails
```

### 9. Accéder à l'interface
```
http://localhost:8080
```

### 10. Utiliser
- Cliquer "Actualiser" pour traiter les emails
- Explorer le résumé IA
- Filtrer, rechercher, gérer vos emails

---

## 📊 Fonctionnalités

### Analyse IA
- Résumé quotidien personnalisé
- Détection d'urgence (Faible/Moyenne/Forte)
- Emails prioritaires automatiques
- Thèmes clés (1-2 mots)

### Interface Web
- Dashboard avec résumé IA
- Recherche temps réel
- Filtres avancés (expéditeur, épinglés, corbeille)
- Actions (épingler, archiver, supprimer)
- Design responsive

### Automatisation
- Exécution quotidienne (18h00)
- Déclenchement webhook/manuel
- Persistance des actions

## 📁 Structure

```
gmail/
├── docker-compose.yml          # Orchestration
├── json/workflow.json          # Workflow n8n
├── front-page/                 # Interface web
│   ├── index.html
│   ├── assets/script/script.js
│   ├── assets/style/style.css
│   └── data/mails-today.json
├── rapport.md                  # Rapport technique
└── README.md                   # Ce fichier
```

## 🔗 URLs

| Service | URL |
|---------|-----|
| **Interface Web** | http://localhost:8080 |
| **n8n** | http://localhost:5678 |
| **JSON** | http://localhost:8080/data/mails-today.json |

## 🛠️ Commandes utiles

```bash
# Logs
docker-compose logs -f n8n

# Redémarrer
docker-compose restart n8n

# Arrêter
docker-compose down
```

## 🐛 Dépannage

**Workflow ne s'exécute pas :**  
→ Vérifier credentials Gmail + OpenAI

**Interface vide :**  
→ Exécuter le workflow au moins une fois

**Erreur quota Gmail :**  
→ Limites API (100/jour gratuit)

## 📖 Documentation

- [Interface Web](front-page/README.md)
- [Workflow n8n](json/README.md)  
- [Rapport Technique](rapport.md)

---
*Installation en 10 étapes - Prêt à l'emploi*
