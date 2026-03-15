<p align="center">
  <img src="assets/n8n-logo.png" alt="n8n Logo" width="120">
</p>

<h1 align="center">TikTok Intelligence</h1>

<p align="center">
  <strong>Automated TikTok monitoring: extraction, transcripts and AI analysis</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n">
  <img src="https://img.shields.io/badge/TikTok-000000?style=for-the-badge&logo=tiktok&logoColor=white" alt="TikTok">
  <img src="https://img.shields.io/badge/Apify-97D700?style=for-the-badge&logo=apify&logoColor=black" alt="Apify">
  <img src="https://img.shields.io/badge/Airtable-18BFFF?style=for-the-badge&logo=airtable&logoColor=white" alt="Airtable">
  <img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI">
</p>

---

## Overview

n8n workflow for TikTok monitoring: extract videos by keywords or accounts, fetch VTT transcripts, and store enriched data in Airtable.

### Technical Core

| Layer | Implementation |
|-------|----------------|
| **Orchestration** | n8n |
| **Source** | Apify (TikTok Scraper) |
| **AI** | OpenAI (summaries, insights) |
| **Storage** | Airtable |
| **Input** | Webhook / web form |

**Architecture** : `Web form → n8n → Apify TikTok → VTT → OpenAI → Airtable`

<p align="center">
  <img src="assets/n8n-workflow.png" alt="n8n Workflow" width="800">
</p>

---

## Features

- **Flexible search** : By keywords or specific accounts
- **TikTok metrics** : Views, likes, comments, shares
- **VTT transcripts** : Automatic subtitle extraction
- **AI analysis** : Summaries and insights via OpenAI
- **Airtable storage** : Structured database

<p align="center">
  <img src="assets/request-form.png" alt="Request form" width="600">
</p>

---

## Quick start

### Prerequisites

| Service | Description |
|---------|-------------|
| n8n | Cloud or self-hosted |
| Apify | Account with TikTok Scraper |
| Airtable | Base |
| OpenAI API | Credits available |

### Step 1: Clone the repository

```bash
git clone https://github.com/RomeoCavazza/no-low-code.git
cd no-low-code/tiktok
```

### Step 2: Set up Airtable

1. Create a new **Base** at [airtable.com](https://airtable.com)
2. Create a table **"Scraped Content"** with columns:

| Column | Type |
|--------|------|
| Video URL | URL |
| Author | Single line text |
| Description | Long text |
| Views | Number |
| Likes | Number |
| Comments | Number |
| Shares | Number |
| Transcript | Long text |
| AI Summary | Long text |
| Created At | Date |

3. Copy the **Base ID** (from the URL: `airtable.com/appXXXXXXX/...`)

### Step 3: Import the workflow

1. Open your **n8n** instance
2. Workflows → **Import from File**
3. Select `json/workflow.json`

### Step 4: Configure credentials

| Service | Configuration |
|---------|---------------|
| Apify | Token from apify.com/account |
| Airtable | API key + Base ID + Table name |
| OpenAI | API key from platform.openai.com |

### Step 5: Activate and use

1. Activate the workflow (toggle **Active** → ON)
2. Copy the webhook URL (first node)
3. Open the form via that URL

### Step 6: Run a search

<p align="center">
  <img src="assets/data-table.png" alt="Airtable results" width="800">
</p>

---

## Form parameters

| Field | Description | Example |
|-------|-------------|---------|
| Keywords | Search keywords | `AI tools, productivity` |
| Accounts | Specific accounts | `@openai, @nvidia` |
| Period | Search period | `7` (days) |
| Results | Number of results | `20` |

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| 401/403 | Check Apify/Airtable credentials |
| Missing VTT | Some videos have no subtitles |
| Rate limiting | Lower `resultsPerPage` |
| Timeout | Increase timeout in n8n |

---

## Project structure

```
tiktok/
├── README.md
├── json/
│   └── workflow.json   # n8n workflow to import
└── assets/
    ├── n8n-logo.png
    ├── n8n-workflow.png
    ├── request-form.png
    └── data-table.png
```
