# Interface Web - Gmail Automation

## 🎯 Fonction
Dashboard web moderne pour visualiser et gérer vos emails avec l'assistance de l'intelligence artificielle.

## 🏗️ Architecture technique

```
front-page/
├── index.html                  # Structure HTML5
├── assets/
│   ├── script/
│   │   └── script.js          # Logique applicative (1166 lignes)
│   └── style/
│       └── style.css          # Styles CSS3 (optimisé)
└── data/
    └── mails-today.json       # Données générées par n8n
```

## 📊 Fonctionnalités principales

### 1. Résumé IA quotidien
- **Date** : Jour de l'analyse
- **Niveau d'urgence** : Badge visuel (Faible/Moyenne/Forte)
- **Résumé intelligent** : Synthèse personnalisée par OpenAI
- **Emails prioritaires** : Liste des emails importants détectés
- **Thèmes clés** : Tags inline des sujets principaux
- **Bouton Actualiser** : Déclenchement du workflow n8n

### 2. Filtres avancés
- **Recherche** : Temps réel dans les sujets d'emails
- **Par expéditeur** : Dropdown avec compteur (affiché si ≥2 emails)
- **Épinglés** : Afficher uniquement les emails épinglés
- **Corbeille** : Gérer les emails supprimés

### 3. Gestion des emails
- **Épingler** : Marquer comme important (icône ⭐)
- **Archiver** : Masquer de la vue principale
- **Supprimer** : Envoyer à la corbeille
- **Restaurer** : Récupérer depuis la corbeille
- **Persistance** : Toutes les actions sauvegardées en localStorage

### 4. États vides contextuels
Messages adaptés selon la situation :
- 📭 **Boîte vide** : "Profitez de ce moment de calme !"
- 🗑️ **Corbeille vide** : "Tout est propre ! 🎉"
- 📌 **Pas d'épinglés** : "Épinglez vos emails importants"
- 🔍 **Aucun résultat** : "Essayez d'autres mots-clés"
- 👤 **Filtre expéditeur** : "Aucun email de cet expéditeur"

## 🎨 Design System

### Couleurs
```css
--primary: #3b82f6        /* Bleu principal */
--success: #10b981        /* Vert succès */
--warning: #f59e0b        /* Orange warning */
--danger: #ef4444         /* Rouge danger */
--neutral-50 à 900        /* Échelle de gris */
```

### Espacement
```css
--space-xs: 0.25rem       /* 4px */
--space-sm: 0.5rem        /* 8px */
--space-md: 1rem          /* 16px */
--space-lg: 1.5rem        /* 24px */
--space-xl: 2rem          /* 32px */
```

### Responsive
- **Desktop** : Footer fixe, colonnes larges
- **Tablet** : Adaptation des espacements
- **Mobile** : Footer relatif, design vertical

## 🔧 Technologies

- **HTML5** : Structure sémantique
- **CSS3** : Variables custom, Flexbox, Grid, animations
- **Vanilla JavaScript** : Pur, sans framework (performance optimale)
- **localStorage** : Persistance côté client
- **Lucide Icons** : Icônes modernes et légères

## 📦 Modules JavaScript

### État global (`state`)
```javascript
{
  emails: [],           // Liste complète des emails
  summary: {},          // Résumé IA (urgence, thèmes, priorités)
  states: {},           // États (pinned, trashed, archived)
  senders: []           // Liste des expéditeurs uniques
}
```

### Gestion des filtres (`filters`)
- `togglePinned()` : Basculer vue épinglés
- `toggleTrash()` : Basculer vue corbeille
- `setSearch(query)` : Recherche texte
- `setSender(sender)` : Filtre par expéditeur
- `getCurrent()` : Récupérer filtres actifs

### Rendu (`render`)
- `summary()` : Affichage du résumé IA
- `table()` : Liste des emails
- `senderOptions()` : Dropdown expéditeurs triés
- `emptyState()` : Messages contextuels
- `updateCounters()` : Statistiques

### Actions emails (`emails`)
- `pin(id)` : Épingler/désépingler
- `trash(id)` : Envoyer à corbeille
- `archive(id)` : Archiver
- `restore(id)` : Restaurer depuis corbeille

## 🚀 Utilisation

### Accès
```
http://localhost:8080
```

### Actualiser les données
**Méthode 1 :** Cliquer sur le bouton "Actualiser" dans l'interface

**Méthode 2 :** Appeler le webhook n8n
```bash
curl -X POST http://localhost:5678/webhook/refresh-mails
```

### Flux de données
```
1. Utilisateur clique "Actualiser"
2. Frontend → Webhook n8n
3. n8n → Gmail API (récupération emails)
4. n8n → OpenAI (analyse IA)
5. n8n → Écriture mails-today.json
6. Frontend → Rechargement et affichage
```

## 🎯 Optimisations

- **Cache busting** : Versioning des assets (`?v=1.0`)
- **Lazy rendering** : Rendu conditionnel selon les filtres
- **Event delegation** : Gestion optimisée des événements
- **CSS optimisé** : Suppression des classes mortes et doublons
- **Tri intelligent** : Expéditeurs par ordre décroissant d'emails

## 🐛 Debug

### Vérifier l'état
```javascript
console.log(window.state);
```

### Réinitialiser localStorage
```javascript
localStorage.clear();
location.reload();
```

### Forcer le rechargement
```javascript
loader.getData();
```

### Inspecter les données JSON
```
http://localhost:8080/data/mails-today.json
```

## 🔄 Persistance

Toutes les actions utilisateur sont sauvegardées en **localStorage** :
- Emails épinglés
- Emails archivés
- Emails supprimés (corbeille)
- Ordre personnalisé

Les données persistent entre les sessions et les actualisations.

---
*Interface web moderne et performante - 100% vanilla JavaScript - Sans dépendances*
