# Multi-Scraper - Veille IA Automatisée

## 🎯 Fonction
Workflow Make pour l'agrégation multi-sources de veille intelligence artificielle : flux RSS spécialisés + comptes Instagram tech vers Google Sheets avec enrichissement IA.

## 🏗️ Architecture
- **Sources** : Flux RSS IA + comptes Instagram tech (NVIDIA, OpenAI, Google, Microsoft, etc.)
- **Processing** : Extraction contenu → Enrichissement IA (OpenAI GPT-3 + Gemini Pro)
- **Output** : Google Sheets structuré avec métadonnées et résumés IA

## 🚀 Installation rapide

### 1. Prérequis
- Compte Make (ex-Zapier) actif
- Credentials configurés :
  - Google Sheets (connexion Drive)
  - OpenAI API (GPT-3.5-turbo)
  - Google Gemini API
  - Apify (Instagram scraper)

### 2. Import
```bash
# Dans Make : Templates → Import Blueprint
multi-scraper/json/workflow.json
```

### 3. Configuration
- **Google Sheets** : Configurer connexion et ID du spreadsheet
- **OpenAI** : Token API pour enrichissement contenu
- **Gemini** : API key pour analyse d'images Instagram
- **Apify** : Token pour scraping Instagram

### 4. Test
1. Exécuter le workflow manuellement
2. Vérifier les données dans Google Sheets
3. Planifier l'exécution automatique

## 📊 Sources de données

### Flux RSS IA
- RSS Feed 1 : Veille IA généraliste
- RSS Feed 2 : Actualités tech spécialisées

### Comptes Instagram
- **Tech Giants** : NVIDIA, OpenAI, Google, Microsoft, Apple
- **Research** : MIT, Stanford, DeepMind, Anthropic
- **Startups** : Hugging Face, Tesla, SpaceX

## 🔧 Fonctionnalités

### Traitement automatique
- **RSS** : Extraction articles + résumé IA + stockage
- **Instagram** : Scraping posts + analyse images (Gemini) + stockage
- **Déduplication** : Évite les doublons dans Google Sheets
- **Enrichissement** : Résumés IA, catégorisation, sentiment

### Sortie structurée
- **Colonnes** : Titre, URL, date, source, résumé IA, métadonnées
- **Format** : Google Sheets avec onglet "Agrégateur"
- **Historique** : Conservation des données précédentes

## 🔗 Démo
[Google Sheet de démonstration](https://docs.google.com/spreadsheets/d/17JXOTxNk7-EDYpSQIKgBH-hyClpwn7jkmSknl3Azs1A/edit)

## 🔧 Dépannage

### Erreurs communes
- **API limits** : Vérifier quotas OpenAI/Gemini
- **Instagram rate limiting** : Réduire fréquence d'exécution
- **Google Sheets** : Vérifier permissions et format

### Bonnes pratiques
- Planifier exécution quotidienne/hebdomadaire
- Monitorer les quotas API
- Sauvegarder le workflow après modifications

## 📁 Structure
```
multi-scraper/
├── json/workflow.json          # Blueprint Make "AI Monthly"
├── screenshots/                # Captures d'écran
│   ├── make-workflow.png       # Interface Make
│   └── data-sheet.png          # Résultat Google Sheets
└── README.md                   # Cette documentation
```

## 🎬 Utilisation
1. **Configuration** : Credentials et connexions
2. **Exécution** : Workflow automatique (RSS + Instagram → IA → Sheets)
3. **Consultation** : Données enrichies dans Google Sheets
4. **Veille** : Monitoring continu de l'écosystème IA