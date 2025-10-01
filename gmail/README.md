# Gmail Automation - IA & Dashboard Web

## 🎯 Fonction
Système complet d'automatisation Gmail avec analyse IA pour gérer et visualiser vos emails via une interface web moderne.

## 🏗️ Architecture
```
Gmail API → n8n Workflow → OpenAI GPT-3.5 → JSON → Interface Web
```

**Composants :**
- **n8n** : Workflow d'automatisation (récupération emails + analyse IA)
- **OpenAI** : Analyse intelligente (résumé, urgence, thèmes, priorités)
- **Interface Web** : Dashboard moderne avec filtres et gestion d'emails
- **Docker** : Environnement reproductible et portable

## 🚀 Installation rapide

### 1. Prérequis
- Docker et Docker Compose installés
- Compte Gmail avec API activée
- Clé API OpenAI (GPT-3.5-turbo)

### 2. Lancement
```bash
cd gmail/
docker-compose up -d
```

### 3. Configuration n8n
```bash
# Accéder à n8n
http://localhost:5678

# Importer le workflow
json/workflow.json

# Configurer les credentials
- Gmail OAuth2 (lecture emails)
- OpenAI API Key
```

### 4. Activation
- Activer le workflow dans n8n
- Accéder à l'interface : http://localhost:8080
- Cliquer "Actualiser" pour traiter les emails

## 📁 Structure
```
gmail/
├── docker-compose.yml          # Orchestration Docker
├── json/
│   └── workflow.json           # Workflow n8n complet
├── front-page/                 # Interface web
│   ├── index.html              # Page principale
│   ├── assets/
│   │   ├── script/
│   │   │   └── script.js       # Logique applicative
│   │   └── style/
│   │       └── style.css       # Styles CSS3
│   ├── data/
│   │   └── mails-today.json    # Données générées par n8n
│   └── README.md               # Doc interface
├── screenshots/                # Captures d'écran
├── rapport.md                  # Rapport technique détaillé
└── README.md                   # Ce fichier
```

## 🔗 URLs d'accès

| Service | URL | Description |
|---------|-----|-------------|
| **Interface Web** | http://localhost:8080 | Dashboard principal |
| **n8n Workflow** | http://localhost:5678 | Configuration & monitoring |
| **Données JSON** | http://localhost:8080/data/mails-today.json | Données brutes |

## 📊 Fonctionnalités

### 🤖 Analyse IA (OpenAI GPT-3.5-turbo)
- **Résumé quotidien** : Synthèse personnalisée de vos emails
- **Niveau d'urgence** : Faible, Moyenne, Forte
- **Emails prioritaires** : Détection automatique des emails importants
- **Thèmes clés** : Extraction de 1-2 mots par thème (max 15 caractères)
- **Actions suggérées** : Recommandations IA

### 🌐 Interface Web
- **Dashboard** : Résumé IA + statistiques
- **Recherche** : Temps réel dans les sujets
- **Filtres** : Par expéditeur, épinglés, corbeille
- **Actions** : Épingler, archiver, supprimer, restaurer
- **Persistance** : localStorage pour les actions utilisateur
- **Responsive** : Design adaptatif mobile/desktop
- **États vides** : Messages contextuels selon les filtres

### 🔄 Automatisation
- **Planification** : Exécution automatique quotidienne (18h00)
- **Webhook** : Déclenchement depuis l'interface
- **Manuel** : Exécution à la demande dans n8n
- **Synchronisation** : Mise à jour temps réel

## 🛠️ Commandes utiles

```bash
# Démarrer l'environnement
docker-compose up -d

# Voir les logs
docker-compose logs -f n8n
docker-compose logs -f web

# Redémarrer un service
docker-compose restart n8n

# Arrêter tout
docker-compose down

# Tester le webhook
curl -X POST http://localhost:5678/webhook/refresh-mails
```

## 📖 Documentation

- **[Interface Web](front-page/README.md)** : Guide d'utilisation du dashboard
- **[Workflow n8n](json/README.md)** : Configuration du workflow
- **[Rapport Technique](rapport.md)** : Défis et solutions techniques

## 🎯 Technologies

- **n8n** : Workflow automation open-source
- **OpenAI GPT-3.5-turbo** : LLM pour analyse IA
- **Vanilla JavaScript** : Interface web sans framework
- **Docker** : Conteneurisation et déploiement
- **Gmail API** : Récupération des emails

## 🚧 Défis techniques résolus

1. **Parsing LLM** : Gestion robuste du JSON généré par OpenAI
2. **Connexion n8n-frontend** : Synchronisation webhook/manual/schedule
3. **Volumes Docker** : Partage de données entre conteneurs

---
*Automatisation Gmail complète avec IA - Prête à déployer en 3 commandes.*
