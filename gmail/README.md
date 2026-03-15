<p align="center">
  <img src="assets/n8n-logo.png" alt="n8n Logo" width="120">
</p>

<h1 align="center">📧 Gmail AI Dashboard</h1>

<p align="center">
  <strong>Automatisation Gmail avec analyse IA et interface web moderne</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI">
  <img src="https://img.shields.io/badge/Gmail_API-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Gmail API">
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript">
</p>

---

## Aperçu

Ce workflow extrait automatiquement vos emails Gmail, les analyse avec OpenAI GPT-3.5, et affiche les résultats dans une interface web élégante.

### Technical Core

| Layer | Implementation |
|-------|----------------|
| **Orchestration** | n8n |
| **IA** | OpenAI GPT-3.5 |
| **Données** | Gmail API |
| **Interface** | Vanilla JS, HTML5, CSS3, localStorage |
| **Runtime** | Docker + docker-compose |

**Architecture** : `Gmail API → n8n → OpenAI GPT-3.5 → JSON → Interface Web`

Détail du pipeline n8n :

```
Trigger (Schedule/Webhook/Manual)
    ↓
Gmail API - Get Messages (24h)
    ↓
Extract & Clean Data
    ↓
OpenAI Analysis → JSON
    ↓
Write File → /data/mails-today.json
```

**Déclencheurs** : Schedule (quotidien 18h00) · Webhook `/webhook/refresh-mails` · Manual (bouton "Test workflow")

<p align="center">
  <img src="assets/n8n-workflow.png" alt="n8n Workflow" width="800">
</p>

---

## Fonctionnalités

- **Extraction Gmail** : Récupération automatique des derniers emails
- **Analyse IA** : Résumé et catégorisation par OpenAI
- **Dashboard Web** : Résumé IA quotidien avec badge d'urgence ; gestion des emails (épingler, archiver, supprimer, restaurer) ; filtres recherche temps réel (`/`), par expéditeur, épinglés ; états vides contextuels
- **Webhook** : Rafraîchissement à la demande
- **Dockerisé** : Déploiement en une commande

**Stack interface** : HTML5, CSS3, Vanilla JavaScript, localStorage · Icons : Lucide

<p align="center">
  <img src="assets/front-page.png" alt="Interface Web" width="800">
</p>

---

## Guide de démarrage rapide

### Prérequis

| Outil | Description |
|-------|-------------|
| Docker | Engine + Compose |
| Compte Google | Avec Gmail activé |
| OpenAI API | Avec crédits disponibles |

### Étape 1 : Cloner le repository

```bash
git clone https://github.com/Productivityio/workflow-n8n-gmail.git
cd workflow-n8n-gmail
```

### Étape 2 : Préparer les permissions

```bash
docker run --rm -v "$(pwd)/frontend/data:/data" alpine sh -c "chmod -R 777 /data"
```

### Étape 3 : Démarrer les services

```bash
docker-compose up -d
# Attendre 30 secondes pour l'initialisation
```

### Étape 4 : Importer le workflow

1. Ouvrir **http://localhost:5678**
2. Menu → **Import from File** → `json/workflow.json`

### Étape 5 : Configurer les credentials

#### Gmail OAuth2

1. [Google Cloud Console](https://console.cloud.google.com/) → Créer un projet
2. Activer **Gmail API**
3. Créer un **OAuth 2.0 Client ID** (type: Web app)
4. Configurer :
   - Authorized origins : `http://localhost:5678`
   - Redirect URI : `http://localhost:5678/rest/oauth2-credential/callback`
5. Dans n8n : nœud "Get many messages" → Create credential → Connecter

#### OpenAI

1. Créer une API key sur [platform.openai.com](https://platform.openai.com/api-keys)
2. Dans n8n : nœud "Basic LLM Chain" → Create credential → Coller la key

### Étape 6 : Tester et activer

```bash
# Test dans n8n : Bouton "Test workflow"
cat frontend/data/mails-today.json

# Activer le workflow : Toggle "Active" → ON
# Webhook manuel : 
curl -X POST http://localhost:5678/webhook/refresh-mails
```

---

## Points d'accès

| Service | URL |
|---------|-----|
| Interface web | http://localhost:8080 |
| n8n | http://localhost:5678 |
| JSON généré | http://localhost:8080/data/mails-today.json |

**Flux interface** : Clic "Actualiser" → Webhook n8n → Gmail API → OpenAI → `mails-today.json` → rechargement de l’interface.

---

## Monitoring

```bash
docker-compose logs -f n8n
curl -X POST http://localhost:5678/webhook/refresh-mails
```

---

## Documentation

| Fichier | Description |
|---------|-------------|
| `rapport.md` | Difficultés techniques rencontrées |

---

## Dépannage

| Problème | Solution |
|----------|----------|
| Erreur OAuth | Vérifier les redirect URIs dans Google Console |
| JSON vide | Tester manuellement le workflow dans n8n |
| Port occupé | Modifier les ports dans `docker-compose.yml` |
| Debug interface | `console.log(window.state)` pour l’état ; `localStorage.clear()` pour réinitialiser |

---

<p align="center">
  Made by <a href="https://github.com/Productivityio">Productivityio</a>
</p>
