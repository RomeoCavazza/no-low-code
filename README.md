### no-low-code — Workflows d’automatisation (Make & n8n)

Ce dossier rassemble des travaux sur des outils d’automatisation no code / low code, avec deux workflows prêts à l’import: un scénario Make pour l’agrégation multi‑sources vers Google Sheets et un workflow n8n focalisé TikTok vers Airtable.

### Contenu du dossier
- **Make/**: workflow d’agrégation « AI Monthly » (sources: RSS, Instagram, TikTok) vers Google Sheets.
  - Blueprint: `Make/make-workflow.json`
  - Guide: `Make/README.md`
- **n8n/**: workflow de veille TikTok → Airtable, avec formulaire d’entrée et extraction de transcript (VTT).
  - Blueprint: `n8n/n8n-workflow.json`
  - Guide: `n8n/README.md`

### Aperçu rapide
- **Make (AI Monthly)**: agrège des contenus sur une niche et une période donnée (RSS/Instagram/TikTok) puis écrit dans un Google Sheet (onglet par défaut `Agrégateur`).
  - Google Sheet de démonstration: [Lien Google Sheets](https://docs.google.com/spreadsheets/d/17JXOTxNk7-EDYpSQIKgBH-hyClpwn7jkmSknl3Azs1A/edit?gid=0#gid=0)
- **n8n (TikTok → Airtable)**: interroge l’acteur Apify TikTok, récupère les sous‑titres pour produire un transcript, et charge les données dans Airtable (onglet « Scraped Content »). Formulaire simplifié pour créer des requêtes.
  - Base Airtable de démonstration: [Lien Airtable](https://airtable.com/appUKygDScJYHelFj/pagKUI8oSIrjRYGFA)

### Structure
```
no-low-code/
  Make/
    make-workflow.json
    make-screenshots/
      data-sheet.png
      make-workflow.png
    README.md
  n8n/
    n8n-workflow.json
    n8n-screenshots/
      data-table.png
      n8n-workflow.png
      request-form.png
    README.md
  README.md (ce fichier)
```

### Quickstart
1) Ouvrez le guide dédié à l’outil que vous souhaitez utiliser:
   - Make: voir `Make/README.md`
   - n8n: voir `n8n/README.md`
2) Importez le blueprint (`make-workflow.json` ou `n8n-workflow.json`).
3) Configurez les connexions/credentials (Google, Apify, Airtable, etc.).
4) Exécutez un test avec un faible volume d’items.
5) Planifiez les exécutions selon vos besoins (scheduler Make / activation n8n).
x
### Sécurité & bonnes pratiques
- Ne versionnez pas de secrets (tokens, clés API) en clair dans les JSON.
- Utilisez les gestionnaires d’identifiants des plateformes (Make Connections, n8n Credentials) et/ou des variables d’environnement.
- Respectez les limites d’API (rate limits) et ajoutez des temporisations si nécessaire.
- Conservez une copie exportée des blueprints après modifications et documentez les changements.

### Documentation détaillée
- Guide Make: `Make/README.md`
- Guide n8n: `n8n/README.md`