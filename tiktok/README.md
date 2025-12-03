<p align="center">
  <img src="assets/n8n-logo.png" alt="n8n Logo" width="120">
</p>

<h1 align="center">🎵 TikTok Intelligence</h1>

<p align="center">
  <strong>Veille TikTok automatisée : extraction, transcripts et analyse IA</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n">
  <img src="https://img.shields.io/badge/TikTok-000000?style=for-the-badge&logo=tiktok&logoColor=white" alt="TikTok">
  <img src="https://img.shields.io/badge/Apify-97D700?style=for-the-badge&logo=apify&logoColor=black" alt="Apify">
  <img src="https://img.shields.io/badge/Airtable-18BFFF?style=for-the-badge&logo=airtable&logoColor=white" alt="Airtable">
  <img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI">
</p>

---

## Aperçu

Workflow n8n pour veille TikTok : extraction de vidéos par mots-clés ou comptes, récupération des transcripts VTT, et stockage enrichi dans Airtable.

**Architecture** : `Formulaire Web → n8n → Apify TikTok → VTT → OpenAI → Airtable`

<p align="center">
  <img src="assets/n8n-workflow.png" alt="n8n Workflow" width="800">
</p>

---

## Fonctionnalités

- **Recherche flexible** : Par mots-clés ou comptes spécifiques
- **Métriques TikTok** : Vues, likes, commentaires, partages
- **Transcripts VTT** : Extraction automatique des sous-titres
- **Analyse IA** : Résumé et insights via OpenAI
- **Stockage Airtable** : Base de données structurée

<p align="center">
  <img src="assets/request-form.png" alt="Formulaire de requête" width="600">
</p>

---

## Guide de démarrage rapide

### Prérequis

| Service | Description |
|---------|-------------|
| n8n | Cloud ou self-hosted |
| Apify | Compte avec TikTok Scraper |
| Airtable | Base de données |
| OpenAI API | Avec crédits disponibles |

### Étape 1 : Cloner le repository

```bash
git clone https://github.com/Productivityio/workflow-n8n-tiktok.git
cd workflow-n8n-tiktok
```

### Étape 2 : Préparer Airtable

1. Créer une nouvelle **Base** sur [airtable.com](https://airtable.com)
2. Créer une table **"Scraped Content"** avec les colonnes :

| Colonne | Type |
|---------|------|
| Video URL | URL |
| Author | Single line text |
| Description | Long text |
| Views | Number |
| Likes | Number |
| Comments | Number |
| Shares | Number |
| Transcript | Long text |
| AI Summary | Long text |
| Created At | Date |

3. Copier le **Base ID** (dans l'URL : `airtable.com/appXXXXXXX/...`)

### Étape 3 : Importer le workflow

1. Ouvrir votre instance **n8n**
2. Workflows → **Import from File**
3. Sélectionner `json/workflow.json`

### Étape 4 : Configurer les credentials

| Service | Configuration |
|---------|---------------|
| Apify | Token depuis apify.com/account |
| Airtable | API key + Base ID + Table name |
| OpenAI | API key depuis platform.openai.com |

### Étape 5 : Activer et utiliser

1. Activer le workflow (toggle **Active** → ON)
2. Copier l'URL du webhook (premier nœud)
3. Accéder au formulaire via cette URL

### Étape 6 : Lancer une recherche

<p align="center">
  <img src="assets/data-table.png" alt="Résultats Airtable" width="800">
</p>

---

## Paramètres du formulaire

| Champ | Description | Exemple |
|-------|-------------|---------|
| Keywords | Mots-clés de recherche | `AI tools, productivity` |
| Accounts | Comptes spécifiques | `@openai, @nvidia` |
| Period | Période de recherche | `7` (jours) |
| Results | Nombre de résultats | `20` |

---

## Dépannage

| Problème | Solution |
|----------|----------|
| 401/403 | Vérifier credentials Apify/Airtable |
| VTT manquant | Certaines vidéos n'ont pas de sous-titres |
| Rate limiting | Réduire `resultsPerPage` |
| Timeout | Augmenter le timeout dans n8n |

---

## Structure du projet

```
workflow-n8n-tiktok/
├── README.md           # Ce fichier
├── json/
│   └── workflow.json   # Workflow n8n à importer
└── assets/
    ├── n8n-logo.png
    ├── n8n-workflow.png
    ├── request-form.png
    └── data-table.png
```

---

<p align="center">
  Made by <a href="https://github.com/Productivityio">Productivityio</a>
</p>
