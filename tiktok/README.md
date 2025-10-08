# TikTok Intelligence Automation

Workflow n8n pour veille TikTok : extraction vidéo, transcripts et stockage Airtable.

## Architecture

**Input** : Formulaire web (mots-clés/comptes + période)  
**Processing** : Apify TikTok Scraper → extraction VTT → transcript IA  
**Output** : Airtable (métriques, transcript, analyse IA)

## Installation

### Prérequis
- Instance n8n (cloud/self-hosted)
- Credentials : Apify, Airtable, OpenAI

### Setup
1. n8n → Workflows → Import from File → `json/workflow.json`
2. Configurer credentials (Apify token, Airtable Base ID)
3. Accéder au formulaire via webhook URL

## Fonctionnalités

- **Recherche** : Par mots-clés ou comptes spécifiques
- **Extraction** : Métriques TikTok + transcripts VTT + analyse IA
- **Stockage** : Table Airtable "Scraped Content"

## Dépannage

- **401/403** : Vérifier credentials
- **VTT manquant** : Tous les posts n'ont pas de sous-titres
- **Rate limiting** : Réduire `resultsPerPage`