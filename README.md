<p align="center">
  <img src="https://img.shields.io/badge/Automation_Workflows-6D00CC?style=for-the-badge" alt="Automation Workflows">
</p>

<h1 align="center">⚡ No-Low-Code Workflows</h1>

<p align="center">
  <strong>3 projets d'automatisation professionnels : orchestration, IA et intégrations</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n">
  <img src="https://img.shields.io/badge/Make-6D00CC?style=for-the-badge&logo=integromat&logoColor=white" alt="Make">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI">
  <img src="https://img.shields.io/badge/Google_Gemini-4285F4?style=for-the-badge&logo=google&logoColor=white" alt="Google Gemini">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Apify-97D700?style=for-the-badge&logo=apify&logoColor=black" alt="Apify">
  <img src="https://img.shields.io/badge/Airtable-18BFFF?style=for-the-badge&logo=airtable&logoColor=white" alt="Airtable">
  <img src="https://img.shields.io/badge/Google_Sheets-34A853?style=for-the-badge&logo=googlesheets&logoColor=white" alt="Google Sheets">
  <img src="https://img.shields.io/badge/Gmail_API-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Gmail API">
  <img src="https://img.shields.io/badge/TikTok-000000?style=for-the-badge&logo=tiktok&logoColor=white" alt="TikTok">
</p>

---

## Workflows

### 📧 [Gmail AI Dashboard](gmail/)

Automatisation Gmail avec analyse IA et interface web moderne.

| Feature | Description |
|---------|-------------|
| Extraction | Récupération automatique des emails |
| Analyse IA | Résumé et détection d'urgence (OpenAI) |
| Dashboard | Interface web avec tri, épinglage, archivage |
| Docker | Déploiement en une commande |

**Stack** : `n8n` · `OpenAI GPT-3.5` · `Docker` · `JavaScript`

<p align="center">
  <img src="gmail/assets/n8n-workflow.png" alt="Gmail Workflow" width="700">
</p>

---

### 🔍 [Multi-Scraper IA](multi-scraper/)

Veille IA automatisée : RSS + Instagram → Google Sheets enrichi.

| Feature | Description |
|---------|-------------|
| Agrégation | Flux RSS IA + comptes Instagram tech |
| Enrichissement | Résumés GPT + analyse images Gemini |
| Déduplication | Évite les doublons automatiquement |
| Export | Google Sheets structuré |

**Stack** : `Make` · `OpenAI` · `Gemini` · `Apify` · `Google Sheets`

**Démo** : [Google Sheet](https://docs.google.com/spreadsheets/d/17JXOTxNk7-EDYpSQIKgBH-hyClpwn7jkmSknl3Azs1A/edit)

<p align="center">
  <img src="multi-scraper/assets/make-workflow.png" alt="Make Workflow" width="700">
</p>

---

### 🎵 [TikTok Intelligence](tiktok/)

Extraction TikTok avec transcripts et analyse IA → Airtable.

| Feature | Description |
|---------|-------------|
| Recherche | Par mots-clés ou comptes spécifiques |
| Métriques | Vues, likes, commentaires, partages |
| Transcripts | Extraction automatique des sous-titres VTT |
| Analyse IA | Résumé et insights via OpenAI |

**Stack** : `n8n` · `Apify` · `Airtable` · `OpenAI`

<p align="center">
  <img src="tiktok/assets/n8n-workflow.png" alt="TikTok Workflow" width="700">
</p>

---

## Structure

```
no-low-code/
├── gmail/                  # Gmail AI Dashboard
│   ├── docker-compose.yml
│   ├── json/workflow.json
│   ├── assets/
│   └── frontend/
├── multi-scraper/          # Multi-Scraper IA
│   ├── json/workflow.json
│   └── assets/
└── tiktok/                 # TikTok Intelligence
    ├── json/workflow.json
    └── assets/
```

---

## Technologies

| Catégorie | Outils |
|-----------|--------|
| **Automation** | n8n, Make, Docker |
| **IA** | OpenAI GPT-3.5, Google Gemini |
| **Scraping** | Apify |
| **Databases** | Airtable, Google Sheets |
| **APIs** | Gmail, TikTok |
| **Frontend** | JavaScript, HTML5, CSS3 |

---

## Repos séparés (Productivityio)

Ces workflows sont également disponibles individuellement :

| Workflow | Repo |
|----------|------|
| Gmail | [workflow-n8n-gmail](https://github.com/Productivityio/workflow-n8n-gmail) |
| Multi-Scraper | [workflow-make-multi-scraper](https://github.com/Productivityio/workflow-make-multi-scraper) |
| TikTok | [workflow-n8n-tiktok](https://github.com/Productivityio/workflow-n8n-tiktok) |

---

<p align="center">
  Made by <a href="https://github.com/RomeoCavazza">Romeo Cavazza</a>
</p>
