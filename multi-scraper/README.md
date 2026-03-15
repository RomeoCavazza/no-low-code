<p align="center">
  <img src="assets/make-logo.png" alt="Make Logo" width="160">
</p>

<h1 align="center">🔍 Multi-Scraper IA</h1>

<p align="center">
  <strong>Automated AI monitoring: RSS + Instagram → enriched Google Sheets</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Make-6D00CC?style=for-the-badge&logo=integromat&logoColor=white" alt="Make">
  <img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI">
  <img src="https://img.shields.io/badge/Google_Gemini-4285F4?style=for-the-badge&logo=google&logoColor=white" alt="Google Gemini">
  <img src="https://img.shields.io/badge/Google_Sheets-34A853?style=for-the-badge&logo=googlesheets&logoColor=white" alt="Google Sheets">
  <img src="https://img.shields.io/badge/Apify-97D700?style=for-the-badge&logo=apify&logoColor=black" alt="Apify">
</p>

---

## Overview

Make workflow for multi-source AI monitoring: RSS feeds + Instagram tech accounts → Google Sheets with automatic AI enrichment.

### Technical Core

| Layer | Implementation |
|-------|----------------|
| **Orchestration** | Make |
| **Sources** | RSS, Apify (Instagram) |
| **AI** | OpenAI GPT-3.5, Google Gemini (images) |
| **Storage** | Google Sheets |
| **Runtime** | Make cloud |

**Architecture** : `RSS + Instagram → Make → OpenAI + Gemini → Google Sheets`

<p align="center">
  <img src="assets/make-workflow.png" alt="Make Workflow" width="800">
</p>

---

## Features

- **RSS aggregation** : Major AI feeds (NVIDIA, OpenAI, Google, Microsoft…)
- **Instagram scraping** : Tech accounts via Apify
- **AI enrichment** : GPT-3 summaries + Gemini Pro image analysis
- **Deduplication** : Avoids duplicates automatically
- **Structured export** : Title, URL, date, source, AI summary

<p align="center">
  <img src="assets/data-sheet.png" alt="Google Sheets output" width="800">
</p>

---

## Quick start

### Prerequisites

| Service | Description |
|---------|-------------|
| Make | Free or paid account |
| Google Sheets | Google account |
| OpenAI API | Credits available |
| Gemini API | Google AI Studio |
| Apify | For Instagram scraping |

### Step 1: Clone the repository

```bash
git clone https://github.com/RomeoCavazza/no-low-code.git
cd no-low-code/multi-scraper
```

### Step 2: Create the Google Sheet

1. Create a new Google Sheet
2. Add columns: `Title | URL | Date | Source | AI Summary`
3. Copy the spreadsheet ID (from the URL)

### Step 3: Import the workflow

1. Open [Make.com](https://make.com)
2. Scenarios → **Create a new scenario**
3. Menu (⋮) → **Import Blueprint**
4. Select `json/workflow.json`

### Step 4: Configure credentials

| Service | Configuration |
|---------|----------------|
| Google Sheets | Connect Google account + spreadsheet ID |
| OpenAI | API key from platform.openai.com |
| Gemini | API key from Google AI Studio |
| Apify | Token from apify.com/account |

### Step 5: Configure sources

1. **RSS** : Edit feed URLs in the RSS module
2. **Instagram** : Edit the list of accounts to scrape

### Step 6: Test and schedule

```
1. Click "Run once" to test
2. Check the Google Sheet
3. Enable scheduling (e.g. every 6h)
```

---

## Demo

[Demo Google Sheet](https://docs.google.com/spreadsheets/d/17JXOTxNk7-EDYpSQIKgBH-hyClpwn7jkmSknl3Azs1A/edit)

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| API limits | Check OpenAI/Gemini quotas |
| Rate limiting | Reduce run frequency |
| Permissions | Check Google Sheets access |
| Instagram blocked | Check Apify token and quotas |

---

## Project structure

```
multi-scraper/
├── README.md
├── json/
│   └── workflow.json   # Make blueprint to import
└── assets/
    ├── make-logo.png
    ├── make-workflow.png
    └── data-sheet.png
```
