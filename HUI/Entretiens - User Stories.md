# 1. Entretien d'Objectifs (EO)

1. **Un collaborateur est éligible à un EO** si **au moins 6 mois** se sont écoulés depuis sa **date d’embauche**.
    
2. S’il n’a **jamais passé d’entretien d’objectifs**, c’est la **date d’embauche** qui sert de référence.
    
3. Le **prochain EO** doit se faire **tous les 12 mois** après le dernier réalisé (ou après la date d’embauche s’il n’y en a jamais eu).
    
4. En présence d’une **campagne planifiée** (définie par `campaignStart`), l’EO peut (et doit) être rattaché à cette période.
    
5. En l’absence de campagne, on utilise une **date par défaut** : le **1er octobre** de l’année en cours (ou de l’année suivante si la date est déjà passée).
    
6. Si une campagne est **en cours** et que l'EO n'est pas fait, il est **en retard** et la date renvoyée est celle du **début de campagne**.
    
7. Si une campagne est **terminée** et que l'EO n'est pas fait, il est **en retard** et la date renvoyée est celle de la **fin de campagne**.

8. Si aucune campagne n'est planifiée mais que l'EO est en retard et que l'on est **avant le 1er octobre** alors on affiche un **retard** et la date renvoyée est celle de son dernier EO + 1 an

9. Si aucune campagne n'est planifiée mais que l'EO est en retard et que l'on est **après le 1er octobre** alors on affiche un **retard** et la date renvoyée est celle du **1er octobre passé**

# 2. Entretien Professionnel (EP and EP6)

1. **Un entretien professionnel (EP)** est requis tous les **2 ans**.
    
2. Un collaborateur devient **éligible à un EP** après **2 ans d’ancienneté**.
    
3. S’il n’a **jamais passé d’EP**, c’est la **date d’embauche** qui sert de référence.
    
4. Si un **EP6** est requis (entretien spécifique tous les 6 ans), il **prime sur l’EP** → dans ce cas, **on ne planifie pas d’EP** mais bien un **EP6**
    
5. En présence d'une **campagne planifiée** l’EP peut être intégré à la campagne :
    
    - Si la campagne est **en cours**, et que le collaborateur est **éligible**, l’entretien est planifié à la **date de début de campagne**.
        
    - Si la personne n’est **pas éligible**, on calcule la **date théorique hors campagne** (1er avril 2 ans après le dernier EP / après l'embauche).
    
6. Si l’EP a déjà été fait dans la période de campagne, on reporte au **1er avril dans 2 ans**.
    
7. Si une campagne est **en cours** et que l'EP n'est pas fait, il est **en retard** et la date renvoyée est celle du **début de campagne**.
    
8. Si une campagne est **terminée** et que l'EP n'est pas fait, il est **en retard** et la date renvoyée est celle de la **fin de campagne**.
    
9. Si **aucune campagne n’est planifiée**, que l'on est **avant le 1er avril** et le collaborateur est en retard de plus de 2 ans, alors son retard est :
    
    - À la date du **dernier EP + 2 ans** (si disponible).
        
    - Sinon, à la **date d’embauche + 2 ans**.
    
10. Si **aucune campagne n’est planifiée**, que l'on est **après le 1er avril** et le collaborateur est en retard de plus de 2 ans, alors la date de retard renvoyée est celle du **1er avril passé**
    
11. Si **aucune campagne n’est planifiée**, que l'on est **avant le 1er avril**, que le collaborateur est éligible à **un EP6** et est en retard de plus de 6 ans, alors son retard est :
    
    - À la date du **dernier EP6 + 6 ans** (si disponible).
        
    - Sinon, à la **date d’embauche + 6 ans**.

12. Si **aucune campagne n’est planifiée**, que l'on est **après le 1er avril**, que le collaborateur est éligible à **un EP6** et est en retard de plus de 6 ans, alors la date de retard renvoyée est celle du **1er avril passé**

# 3. Entretien de Suivi (ES)

## EP
1. **Un entretien de suivi (ES)** est requis si aucun entretien n'a eu lieu dans les **4 derniers mois** 
    
	1. Par exemple, si un **EO ou EP** a eu lieu 4 mois après le dernier **ES**, le prochain ES aura lieu **4 mois après l'EO ou EP**