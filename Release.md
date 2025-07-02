Nous avons déployé les nouvelles versions **v1.69.0 (Back)** et **v3.60.0 (Front)** de notre application. Cette mise à jour apporte plusieurs améliorations techniques, de nouvelles fonctionnalités et des correctifs importants :

### **Améliorations principales côté Back :**
- Amélioration du service Keycloak pour récupérer les rôles et groupes des utilisateurs,
- Renforcement de la résilience des appels aux API externes (retries & circuit breakers),
- Intégration de Yapir (IA faisant des retours sur la qualité du code),
- Re-factorisation et ajout de tests pour améliorer la stabilité du code.

###  **Nouveautés côté Front :**
- Simplification des filtres pour les feedbacks : les _contextes_ sont désormais remplacés par des _tags_,
- Amélioration de l'UI/UX de la page de validation des feedbacks,
- Amélioration du chargement du tableau de bord manager,
- Distinction des rôles pouvant visualiser les warnings,
- Affichage corrigé des intervenants (POM et TOM) et des participants (managers) lors de la création d'une formation.
