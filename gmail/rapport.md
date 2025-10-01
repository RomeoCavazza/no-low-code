# Rapport Technique - Gmail Automation avec IA

## Objectif
Système d'automatisation Gmail combinant n8n, IA OpenAI et interface web moderne pour transformer la gestion des emails quotidiens en processus automatisé et intelligent.

## Architecture
```
Gmail API → Workflow n8n → Analyse IA → Interface Web → Stockage local
```

**Composants :**
- **n8n** : Orchestration workflow (récupération + analyse IA)
- **OpenAI GPT-3.5-turbo** : Analyse et résumé des emails
- **Interface vanilla** : HTML/CSS/JS pour performances optimales
- **Docker** : Environnement reproductible

## Défis Techniques Majeurs

### 1. Gestion de la sortie du LLM
**Problème :** L'IA ne respectait pas le format JSON strict requis et générait des réponses de longueur variable.

**Solutions :**
- Suppression du Structured Output Parser n8n qui créait des conflits
- Implémentation de post-traitement JavaScript pour valider et corriger le JSON
- Troncature programmatique des réponses trop longues (priority_emails, key_topics)
- Gestion des différents formats de sortie (objet direct, string JSON, wrapper)

**Code clé :**
```javascript
// Fusion robuste des données LLM
if (item.json.text && typeof item.json.text === 'string') {
  try {
    summary = { ...summary, ...JSON.parse(item.json.text) };
  } catch (e) {}
} else if (item.json.output) {
  summary = item.json.output;
}
```

### 2. Branchement n8n-Frontend
**Problème :** Le webhook n8n pouvait "sauter" le workflow LLM et retourner des données vides au frontend.

**Solutions :**
- Correction des connexions dans le workflow n8n (tous les triggers doivent passer par le même Merge node)
- Ajout de validation côté frontend pour gérer les données null/undefined
- Implémentation de cache busting avec timestamps pour forcer le rechargement
- Gestion des états d'erreur avec messages contextuels

**Code clé :**
```javascript
// Gestion des données null
data = data || {};
if (!data || typeof data !== 'object') {
  console.error('Invalid data format:', data);
  return;
}
```

### 3. Gestion du Docker local
**Problème :** Les volumes Docker n'étaient pas correctement montés, empêchant l'écriture des fichiers JSON.

**Solutions :**
- Configuration précise des volumes dans docker-compose.yml
- Alignement des chemins entre workflow n8n (/files) et volumes Docker (./site/data:/files)
- Gestion des permissions système pour l'écriture des fichiers
- Tests de validation des montages de volumes

**Configuration finale :**
```yaml
volumes:
  - ./site/data:/files  # n8n écrit dans /files
  - ./site:/app         # serveur web lit depuis /app
```

## Solutions Techniques

### Workflow n8n optimisé
- **3 déclencheurs** : webhook, schedule, manual
- **Filtres Gmail** : `newer_than:1d -category:promotions` pour limiter les coûts IA
- **Prompt IA** personnalisé avec contraintes de longueur explicites
- **Post-traitement** JavaScript pour validation et correction

### Interface web robuste
- **Gestion d'état** centralisée avec localStorage
- **Recherche temps réel** avec debouncing
- **Filtres avancés** : expéditeur, tri, statuts
- **Actions utilisateur** : épingler, archiver, supprimer
- **Design responsive** avec CSS variables

### Environnement Docker
- **Services** : n8n + serveur web Python
- **Volumes** : données partagées entre services
- **Réseau** : communication inter-conteneurs
- **Configuration** : variables d'environnement optimisées

## Choix d'Architecture

### Séparation des responsabilités
- **n8n** : Logique métier et intégrations APIs
- **Frontend** : Présentation et interaction utilisateur
- **Docker** : Isolation et reproductibilité

### Technologies sélectionnées
- **n8n** vs Zapier : Plus de contrôle et personnalisation
- **GPT-3.5-turbo** vs Claude : Maturité et coût optimisé
- **Vanilla JS** vs Framework : Performance et simplicité