# Back v1.69.0
[HUI-1538] feat : Replaced contexts by tags and added filters by tags
[HUI-1590] fix: add a method on keycloak service to get all user from both role and group 
[HUI-1606] fix : duplicate users in get request
[HUI-1600] added metadata field to HighlightUpdateDto
[HUI-1550] tech: refacto package permission provider for reducing duplication
[HUI-1594] safe database migration workflow
[HUI-1578] Added back Yapir config
[HUI-1527] tech : added tests on highlight package
[HUI-1588] New endpoint to retrieve all *OMs
[HUI-1534] tech: add unit tests on SpecificationUtils class 
[HUI-1070] Add resilience with retries and circuit breakers on external API calls

# Front v3.60.0
[HUI-1612] fix : Change the translation message when there is no campaigns
[HUI-1538] feat : Replaced contexts by tags and fix filters and style etc
[1488] fix : button not visible when creating campaign
[HUI-1578] Added Front Yapir config
[HUI-1580] feat : added a confirmation modal on context change
[HUI-1577] feat : Change the translation for context in feedbacks 
[HUI-1588] Formation creation modal now displays *OMs for Speakers and all managers for participants
[HUI-1596] fix: added WFV in roles allowed to see the validation tab
[HUI-1546] design: skeleton for dashboard manager card edited




Nous avons déployé les nouvelles versions **v1.69.0 (Back)** et **v3.60.0 (Front)** de notre application. Cette mise à jour apporte plusieurs améliorations techniques, de nouvelles fonctionnalités et des correctifs importants :

### **Améliorations principales côté Back :**
- Amélioration du service Keycloak pour récupérer les rôles et groupes des utilisateurs,
- Nouveau point d’accès pour récupérer tous les TOM, POM et DOM.,
- Renforcement de la résilience des appels aux API externes (retries & circuit breakers),
- Refactorisation et ajout de tests pour améliorer la stabilité du code.

###  **Nouveautés côté Front :**
- Simplification des filtres pour les feedbacks : les _contextes_ sont désormais remplacés par des _tags_,
- 
- Affichage corrigé des intervenants (POM et TOM) et des participants (managers) lors de la création d'une formation,
- Amélioration de l'UI/UX de la page de validation des feedbacks,
- Nouvelles permissions pour accéder à l’onglet de validation
    
- Affichage amélioré du tableau de bord manager
