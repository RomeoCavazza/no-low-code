<p align="center">
  <img src="assets/n8n-logo.png" alt="n8n Logo" width="120">
</p>

<h1 align="center">Gmail AI Dashboard</h1>

<p align="center">
  <strong>Gmail automation with AI analysis and modern web interface</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI">
  <img src="https://img.shields.io/badge/Gmail_API-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Gmail API">
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript">
</p>

---

## Overview

This workflow automatically fetches your Gmail messages, analyses them with OpenAI GPT-3.5, and displays results in a web interface.

### Technical Core

| Layer | Implementation |
|-------|----------------|
| **Orchestration** | n8n |
| **AI** | OpenAI GPT-3.5 |
| **Data** | Gmail API |
| **Interface** | Vanilla JS, HTML5, CSS3, localStorage |
| **Runtime** | Docker + docker-compose |

**Architecture** : `Gmail API → n8n → OpenAI GPT-3.5 → JSON → Web Interface`

Pipeline detail:

```
Trigger (Schedule/Webhook/Manual)
    ↓
Gmail API - Get Messages (24h)
    ↓
Extract & Clean Data
    ↓
OpenAI Analysis → JSON
    ↓
Write File → /data/mails-today.json
```

**Triggers** : Schedule (daily 6pm) · Webhook `/webhook/refresh-mails` · Manual ("Test workflow" button)

<p align="center">
  <img src="assets/n8n-workflow.png" alt="n8n Workflow" width="800">
</p>

---

## Features

- **Gmail extraction** : Automatic fetch of latest emails
- **AI analysis** : Summary and categorisation via OpenAI
- **Web dashboard** : Daily AI summary with urgency badge; email actions (pin, archive, delete, restore); real-time search filter (`/`), by sender, pinned; contextual empty states
- **Webhook** : Refresh on demand
- **Docker** : One-command deploy

**Interface stack** : HTML5, CSS3, Vanilla JavaScript, localStorage · Icons: Lucide

<p align="center">
  <img src="assets/front-page.png" alt="Web Interface" width="800">
</p>

---

## Quick start

### Prerequisites

| Tool | Description |
|------|-------------|
| Docker | Engine + Compose |
| Google account | Gmail enabled |
| OpenAI API | Credits available |

### Step 1: Clone the repository

```bash
git clone https://github.com/RomeoCavazza/no-low-code.git
cd no-low-code/gmail
```

### Step 2: Prepare permissions

```bash
docker run --rm -v "$(pwd)/frontend/data:/data" alpine sh -c "chmod -R 777 /data"
```

### Step 3: Start services

```bash
docker-compose up -d
# Wait ~30 seconds for init
```

### Step 4: Import the workflow

1. Open **http://localhost:5678**
2. Menu → **Import from File** → `json/workflow.json`

### Step 5: Configure credentials

#### Gmail OAuth2

1. [Google Cloud Console](https://console.cloud.google.com/) → Create a project
2. Enable **Gmail API**
3. Create **OAuth 2.0 Client ID** (type: Web application)
4. Set:
   - Authorized origins: `http://localhost:5678`
   - Redirect URI: `http://localhost:5678/rest/oauth2-credential/callback`
5. In n8n: "Get many messages" node → Create credential → Connect

#### OpenAI

1. Create an API key at [platform.openai.com](https://platform.openai.com/api-keys)
2. In n8n: "Basic LLM Chain" node → Create credential → Paste key

### Step 6: Test and activate

```bash
# In n8n: "Test workflow" button
cat frontend/data/mails-today.json

# Activate workflow: Toggle "Active" → ON
# Manual webhook:
curl -X POST http://localhost:5678/webhook/refresh-mails
```

---

## Endpoints

| Service | URL |
|---------|-----|
| Web interface | http://localhost:8080 |
| n8n | http://localhost:5678 |
| Generated JSON | http://localhost:8080/data/mails-today.json |

**Interface flow** : Click "Refresh" → n8n webhook → Gmail API → OpenAI → `mails-today.json` → interface reload.

---

## Monitoring

```bash
docker-compose logs -f n8n
curl -X POST http://localhost:5678/webhook/refresh-mails
```

---

## Documentation

| File | Description |
|------|-------------|
| `rapport.md` | Technical issues encountered |

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| OAuth error | Check redirect URIs in Google Console |
| Empty JSON | Run the workflow manually in n8n |
| Port in use | Change ports in `docker-compose.yml` |
| Interface debug | `console.log(window.state)` for state; `localStorage.clear()` to reset |
