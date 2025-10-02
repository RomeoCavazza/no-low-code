
---

## 🚧 Difficultés rencontrées

1. **Branchement des données dans n8n**  
   - Pas trivial de fusionner les sorties Gmail + résumé IA.  
   - J’ai dû écrire plusieurs expressions JS pour que le JSON reste propre.  

2. **Coordination front ↔ back**  
   - Le bouton « reload » devait appeler un webhook pour rafraîchir les données.  
   - La synchronisation des fichiers JSON avec Docker a nécessité des ajustements (permissions + volumes).  

3. **Dockerisation**  
   - Quelques conflits de droits d’accès au dossier `data/` dans une image dockerisé (a nécessité plusieurs essais)
   - 
---

## 🤔 Ressenti personnel

J’ai pris beaucoup de plaisir à réaliser cette mission.  
- C’était un vrai **challenge technique**, surtout la partie merge dans n8n et la mise en place du front.  
- J’ai appris à mieux documenter mes projets et à penser en termes de **setup reproductible**.  
- J’ai confirmé que l’automatisation + IA + interface utilisateur, c’est vraiment le domaine où je veux me spécialiser.  

👉 Environ **3 jours de travail au total** :  
- 1 jour pour le workflow n8n,  
- 1 soirée pour le front,  
- 1 jour pour la doc, tests et packaging.  

C’est une mission marquante pour moi, et une très bonne pièce dans mon portfolio.  

---
