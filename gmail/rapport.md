# Rapport – Gmail Automation

## Étapes clés du projet

**MVP initial** : mise en place du workflow n8n → récupération Gmail (via schedule) → analyse OpenAI → écriture dans un fichier JSON.

**Défi 1 – Sortie AI** : l’IA ne renvoyait pas toujours du JSON propre → ajout d’un merge + post-traitement pour fiabiliser la sortie.  

**Défi 2 – Multi-triggers** : ajout de 3 modes d’entrée (manual, webhook, schedule) → coordination complexe mais indispensable pour flexibilité d’usage.  

**Défi 3 – Lien backend / frontend** : création d’un volume Docker partagé pour connecter la sortie n8n (JSON) au front HTML/CSS/JS.  

**Défi 4 – Reload via Webhook** : bouton “Actualiser” → envoi cURL au webhook → exécution workflow → mise à jour du JSON → rafraîchissement instantané du front.  

**Défi 5 – Interface responsive** : résumé en haut + liste en bas (mobile), ou vue côte-à-côte (desktop). Mise en forme via Cursor pour CSS/JS.  

**Défi 6 – Packaging final** : regroupement workflow, Docker et site web dans un seul dossier → Quick Start documenté (install en <15 min).  

## Points forts
- Chaîne complète : **cURL → webhook → JSON → front** validée et fonctionnelle.  
- Workflow **n8n relié directement à une interface web**.  
- UX minimaliste mais efficace (reload, tri, affichage responsive).

## Points à renforcer
- **Dépendance à Docker** : nécessite que l’environnement Docker tourne en continu.
- **Pas encore de base de données** : persistance limitée à un fichier JSON local.  
