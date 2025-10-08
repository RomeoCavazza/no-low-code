# Workflows d'Automatisation No-Code/Low-Code

Portfolio de 3 projets d'automatisation professionnels : orchestration de workflows, intégration d'APIs et développement full-stack.

## Projets

### 1. [Gmail Automation avec IA](gmail/)
Automatisation Gmail avec analyse IA et dashboard web.

**Stack** : n8n · OpenAI GPT-3.5 · Docker · Vanilla JS  
**Démo** : [localhost:8080](http://localhost:8080) | [n8n](http://localhost:5678)

### 2. [Multi-Scraper - Veille IA](multi-scraper/)
Agrégation multi-sources de veille IA (RSS + Instagram) vers Google Sheets.

**Stack** : Make · Google Sheets · OpenAI · Gemini · Apify  
**Démo** : [Google Sheet](https://docs.google.com/spreadsheets/d/17JXOTxNk7-EDYpSQIKgBH-hyClpwn7jkmSknl3Azs1A/edit)

### 3. [TikTok Intelligence → Airtable](tiktok/)
Monitoring TikTok avec extraction de transcripts vers Airtable.

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
