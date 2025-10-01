# TikTok Intelligence Automation

## 🎯 Fonction
Workflow n8n automatisé pour la veille TikTok : extraction de contenu vidéo, génération de transcripts et stockage intelligent dans Airtable.

## 🏗️ Architecture
- **Input** : Formulaire web pour requêtes (mots-clés/comptes + période)
- **Processing** : Apify TikTok Scraper → extraction VTT → transcript IA
- **Output** : Airtable avec données enrichies (métriques, transcript, analyse IA)

## 🚀 Installation rapide

### 1. Prérequis
- Instance n8n (cloud/self-hosted)
- Credentials configurés :
  - Apify (token API)
  - Airtable (Personal Access Token + Base ID)
  - OpenAI (pour l'analyse IA)

### 2. Import
```bash
# Dans n8n : Workflows → Import from File
tiktok/json/workflow.json
```

### 3. Configuration
- **Apify** : Remplacer `YOUR_APIFY_TOKEN` dans le nœud HTTP Request
- **Airtable** : Configurer Base ID et table "Scraped Content"
- **Formulaire** : Accès via webhook URL générée

### 4. Test
1. Accédez au formulaire web
2. Saisissez mot-clé + période
3. Vérifiez les données dans Airtable

## 📊 Fonctionnalités

### Modes de recherche
- **Keyword Search** : Recherche par mots-clés
- **Account Search** : Analyse de comptes spécifiques

### Extraction automatique
- Métriques TikTok (vues, likes, partages)
- Transcripts via sous-titres VTT
- Analyse IA du contenu (via Anthropic/OpenAI)

### Stockage structuré
- Table Airtable "Scraped Content"
- Champs : ID, auteur, texte, transcript, métriques, statut

## 🔧 Dépannage

### Erreurs communes
- **401/403** : Vérifier credentials Apify/Airtable
- **VTT manquant** : Tous les posts n'ont pas de sous-titres
- **Rate limiting** : Réduire `resultsPerPage`, ajouter délais

### Bonnes pratiques
- Utiliser credentials n8n (pas de tokens en clair)
- Tester avec `resultsPerPage` faible
- Exporter workflow après modifications

## 📁 Structure
```
tiktok/
├── json/workflow.json          # Workflow n8n principal
├── screenshots/                # Captures d'écran
│   ├── n8n-workflow.png
│   ├── request-form.png
│   └── data-table.png
└── README.md                   # Cette documentation
```

## 🎬 Utilisation
1. **Formulaire** : Saisir requête + période
2. **Exécution** : Workflow automatique (scraping → transcript → stockage)
3. **Consultation** : Données disponibles dans Airtable
4. **Analyse** : Transcripts et métriques pour veille concurrentielle