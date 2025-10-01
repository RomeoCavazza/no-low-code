# Interface Web - Gmail Automation

## 🎯 Fonction
Dashboard web moderne pour visualiser et gérer vos emails avec l'assistance de l'IA.

## 📊 Fonctionnalités

### Résumé IA
- Synthèse quotidienne personnalisée
- Badge d'urgence (Faible/Moyenne/Forte)
- Emails prioritaires détectés
- Thèmes clés (tags inline)

### Gestion des emails
- **Épingler** : Marquer comme important
- **Archiver** : Masquer de la vue
- **Supprimer** : Envoyer à la corbeille
- **Restaurer** : Récupérer depuis corbeille

### Filtres
- Recherche temps réel (touche `/`)
- Par expéditeur (compteur si ≥2)
- Épinglés uniquement
- Vue corbeille

### États vides
Messages contextuels adaptés :
- 📭 Boîte vide
- 🗑️ Corbeille vide
- 📌 Pas d'épinglés
- 🔍 Aucun résultat

## 🏗️ Architecture

```
index.html
├── assets/
│   ├── script/script.js    # 1166 lignes
│   └── style/style.css     # 1828 lignes
└── data/
    └── mails-today.json    # Généré par n8n
```

## 🔧 Technologies

- **HTML5** : Structure sémantique
- **CSS3** : Variables, Grid, Flexbox
- **Vanilla JavaScript** : Pur, sans framework
- **localStorage** : Persistance des actions
- **Lucide Icons** : Iconographie moderne

## 🚀 Utilisation

### Accès
```
http://localhost:8080
```

### Actualiser
Bouton "Actualiser" ou :
```bash
curl -X POST http://localhost:5678/webhook/refresh-mails
```

### Flux de données
```
Clic "Actualiser" → Webhook n8n → Gmail API → OpenAI
→ mails-today.json → Rechargement interface
```

## 🎨 Design System

```css
--primary: #3b82f6        /* Bleu principal */
--space-sm: 0.5rem        /* 8px */
--space-md: 1rem          /* 16px */
--space-lg: 1.5rem        /* 24px */
```

## 🐛 Debug

```javascript
// Vérifier l'état
console.log(window.state);

// Réinitialiser
localStorage.clear();
location.reload();
```

---
*Interface web moderne - 100% vanilla JavaScript*
