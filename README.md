# Workflows d’Automatisation No-Code / Low-Code

Portfolio de **3 projets d’automatisation professionnels** : orchestration de workflows, intégration d’APIs et développement full-stack.

---

![n8n](https://img.shields.io/badge/n8n-EA4C89?logo=n8n\&logoColor=white)
![Make](https://img.shields.io/badge/Make-0085FF?logo=make\&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker\&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?logo=openai\&logoColor=white)
![Anthropic](https://img.shields.io/badge/Anthropic-000000?logo=anthropic\&logoColor=white)
![Gemini](https://img.shields.io/badge/Google%20Gemini-4285F4?logo=google\&logoColor=white)
![Apify](https://img.shields.io/badge/Apify-FF9900?logo=apify\&logoColor=white)
![Airtable](https://img.shields.io/badge/Airtable-18BFFF?logo=airtable\&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?logo=googlesheets\&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript\&logoColor=black)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5\&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3\&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?logo=linux\&logoColor=black)
![NixOS](https://img.shields.io/badge/NixOS-5277C3?logo=nixos\&logoColor=white)

---

## Projets

### 1. [Gmail Automation avec IA](gmail/)

Système complet qui récupère vos emails quotidiennement, les analyse avec **OpenAI** pour générer un résumé intelligent avec détection d’urgence, puis les affiche dans une interface web moderne avec fonctions de tri, épinglage et archivage.
Déployé en **Docker** avec **n8n** pour l’orchestration.

**Stack** : n8n · OpenAI GPT-3.5 · Docker · Vanilla JS
**Démo** : [localhost:8080](http://localhost:8080) | [n8n](http://localhost:5678)

---

### 2. [Multi-Scraper – Veille IA](multi-scraper/)

Workflow **Make** qui agrège automatiquement du contenu tech depuis des flux RSS spécialisés et des comptes **Instagram** (NVIDIA, OpenAI, Google…), enrichit chaque post avec des résumés IA et analyse d’images via **Gemini**, puis centralise le tout dans **Google Sheets** avec déduplication.

**Stack** : Make · Google Sheets · OpenAI · Gemini · Apify
**Démo** : [Google Sheet](https://docs.google.com/spreadsheets/d/17JXOTxNk7-EDYpSQIKgBH-hyClpwn7jkmSknl3Azs1A/edit)

---

### 3. [TikTok Intelligence → Airtable](tiktok/)

Workflow **n8n** avec formulaire web permettant de scraper **TikTok** par mots-clés ou comptes, d’extraire automatiquement les transcripts depuis les sous-titres VTT, d’analyser le contenu avec l’IA, et de stocker toutes les données enrichies dans **Airtable** pour analyse.

**Stack** : n8n · Apify · Airtable · Anthropic · OpenAI

---

## Structure

```
no-low-code/
├── gmail/                  # Gmail Automation
│   ├── docker-compose.yml
│   ├── json/workflow.json
│   └── front-page/
├── multi-scraper/          # Multi-Scraper Make
│   └── json/workflow.json
└── tiktok/                 # TikTok Scraper
    └── json/workflow.json
```

---

## Technologies principales

**Automation** : n8n · Make · Docker

**IA** : OpenAI GPT-3.5 · Google Gemini · Anthropic Claude

**APIs** : Gmail · Apify · Airtable · Google Sheets

**Frontend** : Vanilla JavaScript · HTML5 · CSS3

---

## Contact

[romeo.cavazza@gmail.com](mailto:romeo.cavazza@gmail.com) · [LinkedIn](https://www.linkedin.com/in/romeo-cavazza/)
