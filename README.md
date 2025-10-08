# Workflows d'Automatisation No-Code/Low-Code

Portfolio de 3 projets d'automatisation professionnels : orchestration de workflows, intégration d'APIs et développement full-stack.

## Projets

### 1. [Gmail Automation avec IA](gmail/)
Système complet qui récupère vos emails quotidiennement, les analyse avec OpenAI pour générer un résumé intelligent avec détection d'urgence, puis les affiche dans une interface web moderne avec fonctions de tri, épinglage et archivage. Déployé en Docker avec n8n pour l'orchestration.

**Stack** : n8n · OpenAI GPT-3.5 · Docker · Vanilla JS  
**Démo** : [localhost:8080](http://localhost:8080) | [n8n](http://localhost:5678)

### 2. [Multi-Scraper - Veille IA](multi-scraper/)
Workflow Make qui agrège automatiquement du contenu tech depuis des flux RSS spécialisés et des comptes Instagram (NVIDIA, OpenAI, Google, etc.), enrichit chaque post avec des résumés IA et analyse d'images via Gemini, puis centralise le tout dans Google Sheets avec déduplication.

**Stack** : Make · Google Sheets · OpenAI · Gemini · Apify  
**Démo** : [Google Sheet](https://docs.google.com/spreadsheets/d/17JXOTxNk7-EDYpSQIKgBH-hyClpwn7jkmSknl3Azs1A/edit)

### 3. [TikTok Intelligence → Airtable](tiktok/)
Workflow n8n avec formulaire web permettant de scraper TikTok par mots-clés ou comptes, d'extraire automatiquement les transcripts depuis les sous-titres VTT, d'analyser le contenu avec l'IA, et de stocker toutes les données enrichies dans Airtable pour analyse.

**Stack** : n8n · Apify · Airtable · Anthropic · OpenAI

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

## Technologies

**Automation** : n8n, Make, Docker  
**IA** : OpenAI GPT-3.5, Google Gemini, Anthropic Claude  
**APIs** : Gmail, Apify, Airtable, Google Sheets  
**Frontend** : Vanilla JavaScript, HTML5, CSS3

## Contact

**Roméo Cavazza**  
[romeo.cavazza@gmail.com](mailto:romeo.cavazza@gmail.com) | [LinkedIn](https://www.linkedin.com/in/romeo-cavazza/) | [GitHub](https://github.com/RomeoCavazza)
