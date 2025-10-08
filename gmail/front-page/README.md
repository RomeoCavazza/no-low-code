# Interface Web - Gmail Automation

Dashboard web pour visualiser et gérer vos emails avec assistance IA.

## Fonctionnalités

- Résumé IA quotidien avec badge d'urgence
- Gestion emails : épingler, archiver, supprimer, restaurer
- Filtres : recherche temps réel (`/`), par expéditeur, épinglés
- États vides contextuels

## Technologies

**Stack** : HTML5, CSS3, Vanilla JavaScript, localStorage  
**Icons** : Lucide

## Utilisation

**Accès** : http://localhost:8080

**Actualiser** :
```bash
curl -X POST http://localhost:5678/webhook/refresh-mails
```

**Flux** : Clic "Actualiser" → Webhook n8n → Gmail API → OpenAI → `mails-today.json` → Interface

## Debug

```javascript
console.log(window.state);      // État actuel
localStorage.clear();            // Réinitialiser
```
