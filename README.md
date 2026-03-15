<!-- markdownlint-disable MD033 -->
<div align="center">
  <strong>No-Low-Code Workflows</strong>
  <br /><br />
  <img src="https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n">
  <img src="https://img.shields.io/badge/Make-6D00CC?style=for-the-badge&logo=integromat&logoColor=white" alt="Make">
  <img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI">
  <img src="https://img.shields.io/badge/Google_Gemini-4285F4?style=for-the-badge&logo=google&logoColor=white" alt="Gemini">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker">
</div>
<!-- markdownlint-enable MD033 -->

Collection de trois workflows d’automatisation (n8n, Make) avec intégration IA (OpenAI, Gemini), déployables en autonome ou via Docker. Chaque sous-dossier contient le workflow exporté, les assets et, le cas échéant, un frontend ou une démo.

---

## Technical Core

| Layer | Stack |
|-------|--------|
| **Orchestration** | n8n, Make |
| **IA**            | OpenAI GPT-3.5, Google Gemini |
| **Scraping**      | Apify |
| **Stockage**      | Airtable, Google Sheets |
| **APIs**          | Gmail, TikTok (via Apify) |
| **Runtime**       | Docker (Gmail), Make/n8n cloud (autres) |

---

## Workflows

### [Gmail AI Dashboard](gmail/)

Pipeline Gmail : extraction des emails, résumés et détection d’urgence (OpenAI), dashboard web (tri, épinglage, archivage). Déploiement via Docker.

| Rôle | Détail |
|------|--------|
| Extraction | Récupération automatique des emails (Gmail API) |
| Analyse | Résumés + détection d’urgence (OpenAI) |
| UI | Interface web (JavaScript) |
| Déploiement | `docker-compose` |

![Gmail Workflow](gmail/assets/n8n-workflow.png)

---

### [Multi-Scraper IA](multi-scraper/)

Veille automatisée : agrégation de flux RSS et comptes Instagram, enrichissement (résumés GPT, analyse d’images Gemini), déduplication, export vers Google Sheets.

| Rôle | Détail |
|------|--------|
| Agrégation | RSS + Instagram (Apify) |
| Enrichissement | GPT + Gemini (images) |
| Déduplication | Traitement avant export |
| Export | Google Sheets |

Démo : [Google Sheet](https://docs.google.com/spreadsheets/d/17JXOTxNk7-EDYpSQIKgBH-hyClpwn7jkmSknl3Azs1A/edit).

![Make Workflow](multi-scraper/assets/make-workflow.png)

---

### [TikTok Intelligence](tiktok/)

Extraction TikTok (mots-clés ou comptes) : métriques (vues, likes, commentaires, partages), extraction des sous-titres VTT, résumés et insights (OpenAI), export Airtable.

| Rôle | Détail |
|------|--------|
| Source | TikTok via Apify |
| Métriques | Vues, likes, commentaires, partages |
| Transcripts | Sous-titres VTT |
| Analyse | Résumés OpenAI → Airtable |

![TikTok Workflow](tiktok/assets/n8n-workflow.png)

---

## Structure du dépôt

```
no-low-code/
├── gmail/                  # Gmail AI Dashboard (n8n + Docker + frontend)
│   ├── docker-compose.yml
│   ├── json/workflow.json
│   ├── assets/
│   └── frontend/
├── multi-scraper/          # Multi-Scraper (Make → Google Sheets)
│   ├── json/workflow.json
│   └── assets/
└── tiktok/                 # TikTok Intelligence (n8n → Airtable)
    ├── json/workflow.json
    └── assets/
```

---

## Variantes standalone (Productivityio)

Chaque workflow est aussi publié dans un dépôt dédié sous l’organisation Productivityio :

| Workflow        | Dépôt |
|-----------------|-------|
| Gmail           | [workflow-n8n-gmail](https://github.com/Productivityio/workflow-n8n-gmail) |
| Multi-Scraper   | [workflow-make-multi-scraper](https://github.com/Productivityio/workflow-make-multi-scraper) |
| TikTok          | [workflow-n8n-tiktok](https://github.com/Productivityio/workflow-n8n-tiktok) |
