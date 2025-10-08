# Multi-Scraper - Veille IA Automatisée

Workflow Make pour agrégation multi-sources de veille IA : flux RSS + comptes Instagram tech vers Google Sheets avec enrichissement IA.

## Architecture

**Sources** : Flux RSS IA + Instagram (NVIDIA, OpenAI, Google, Microsoft, etc.)  
**Processing** : Extraction → Enrichissement IA (OpenAI GPT-3 + Gemini Pro)  
**Output** : Google Sheets structuré

## Installation

### Prérequis
- Compte Make
- Credentials : Google Sheets, OpenAI API, Gemini API, Apify

### Setup
1. Make → Templates → Import Blueprint → `json/workflow.json`
2. Configurer credentials et spreadsheet ID
3. Test manuel → Planifier exécution

## Fonctionnalités

- **RSS** : Extraction + résumé IA
- **Instagram** : Scraping + analyse images (Gemini)
- **Déduplication** automatique
- **Export** structuré : titre, URL, date, source, résumé IA

## Démo

[Google Sheet de démonstration](https://docs.google.com/spreadsheets/d/17JXOTxNk7-EDYpSQIKgBH-hyClpwn7jkmSknl3Azs1A/edit)

## Dépannage

- **API limits** : Vérifier quotas OpenAI/Gemini
- **Rate limiting** : Réduire fréquence d'exécution
- **Permissions** : Vérifier accès Google Sheets