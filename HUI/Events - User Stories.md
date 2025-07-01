# 1. Constants
- **Goals Interview Interval** = 1 year
- **Professional Interview Interval** = 2 years
- **Professional 6Y Interview Interval** = 6 years
- **Follow-Up Interview Interval** = 4 months
- **Default Goals Campaign Start Date** = 1st October
- **Goals Campaign Inclusion Interval for new Hires** = 1st February to 31st March

# 2. Goals Interview (EO)

1. **Un collaborateur est éligible à un EO** si **au moins 6 mois** se sont écoulés depuis sa **date d’embauche**.
    
2. S’il n’a **jamais passé d’entretien d’objectifs**, c’est la **date d’embauche** qui sert de référence.
    
3. Le **prochain EO** doit se faire **tous les 12 mois** après le dernier réalisé (ou après la date d’embauche s’il n’y en a jamais eu).
    
4. En présence d’une **campagne planifiée** (définie par `campaignStart`), l’EO peut (et doit) être rattaché à cette période.
    
5. En l’absence de campagne, on utilise une **date par défaut** : le **1er octobre** de l’année en cours (ou de l’année suivante si la date est déjà passée).
    
6. Si l’EO a déjà été fait dans la période de campagne, on reporte au **1er octobre de l’année suivante**.
    
7. Si une campagne est **en cours** et que l'EO n'est pas fait, il est **en retard** et la date renvoyée est celle du **début de campagne**.
    
8. Si une campagne est **terminée** et que l'EO n'est pas fait, il est **en retard** et la date renvoyée est celle de la **fin de campagne**.
9. Si aucune campagne n'est planifiée mais que l'EO est en retard (+12 mois) alors on affiche un retard.

### Cas particuliers

#### 📅 Campagne planifiée (présente dans le système)

- **Entretien déjà réalisé pendant la campagne** → planifier le prochain à **1er octobre de l’année suivante**.
    
- **Entretien non réalisé, mais la campagne est en cours** → utiliser la **date de début de la campagne**.
    
- **Entretien non réalisé, et la campagne est terminée** → utiliser la **date de fin de la campagne**.
    
- **Entretien effectué exactement le jour de début de campagne** → considéré comme **réalisé à temps** → prochain entretien à 1er octobre année suivante.

#### 📅 Campagne non planifiée

- **Éligible + pas d’entretien** → date de l’événement = **date par défaut (1er octobre)**.
    - Si aujourd’hui est **après** le 1er octobre → prendre l’année suivante.
        
- **Pas encore éligible** → reporter au **1er octobre de l’année suivante**.
    
-  **Éligible + entretien passé il y a plus d’un an** → planifier à la **date anniversaire** du dernier entretien (+12 mois).
    
- **Éligible + jamais passé d’entretien + embauché depuis > 1 an** → planifier à la **date d’embauche + 12 mois**.


# 3. Professional Interview (EP and EP6)

## EP
1. **Un entretien professionnel (EP)** est requis tous les **2 ans**.
    
2. Un collaborateur devient **éligible à un EP** après **2 ans d’ancienneté**.
    
3. S’il n’a **jamais passé d’EP**, c’est la **date d’embauche** qui sert de référence.
    
4. Si un **EP6** est requis (entretien spécifique tous les 6 ans), il **prime sur l’EP** → dans ce cas, **on ne planifie pas d’EP** (`return null`).
    
5. En présence d'une **campagne planifiée** (`campaignStart`), l’EP peut être intégré à la campagne :
    
    - Si la campagne est **en cours**, et que le collaborateur est **éligible**, l’entretien est planifié à la **date de début de campagne**.
        
    - Si la personne n’est **pas éligible**, on calcule la **date théorique hors campagne** (1er juin 2 ans après le dernier EP / après l'embauche).
    
7. Si l’EP a déjà été fait dans la période de campagne, on reporte au **1er juin dans 2 ans**.
    
8. Si une campagne est **en cours** et que l'EP n'est pas fait, il est **en retard** et la date renvoyée est celle du **début de campagne**.
    
9. Si une campagne est **terminée** et que l'EP n'est pas fait, il est **en retard** et la date renvoyée est celle de la **fin de campagne**.
    
10. Si **aucune campagne n’est planifiée**, et le collaborateur est en retard de plus de 2 ans, alors son retard est :
    
    - À la date du **dernier EP + 2 ans** (si disponible).
        
    - Sinon, à la **date d’embauche + 2 ans**.

### Eligibilité & planification

| Cas                                                               | Résultat attendu               |
| ----------------------------------------------------------------- | ------------------------------ |
| 📅 Campagne en cours, EP fait à temps                             | `defaultCampaignStart + 2 ans` |
| 📅 Campagne en cours, EP non fait, collaborateur **éligible**     | `campaignStart`                |
| 📅 Campagne en cours, EP non fait, collaborateur **non éligible** | `previousEventEndDate + 2 ans` |
| 📅 Campagne en cours, pas d’EP, collaborateur éligible            | `campaignStart`                |
| 📅 Campagne en cours, pas d’EP, collaborateur non éligible        | `hiringDate + 2 ans`           |
| 📅 Campagne prévue, collaborateur éligible                        | `campaignStart`                |
### Aucune campagne

| Cas                                                          | Résultat attendu                             |
| ------------------------------------------------------------ | -------------------------------------------- |
| ❌ Aucune campagne, pas d’EP, collaborateur éligible          | `defaultCampaignStart`                       |
| ❌ Aucune campagne, dernier EP > 2 ans                        | `previousEventEndDate + 2 ans`               |
| ❌ Aucune campagne, jamais fait d’EP, embauché il y a > 2 ans | `hiringDate + 2 ans`                         |
| ❌ Aucune campagne, EP6 requis                                | `null` (pas d’entretien professionnel prévu) |

# 4. Follow-Up Interview (ES)

## Overview
- An **ES** must be conducted every **4 months**.
- An employee is **ignored** for ES if their **Career Tracking** is `LIGHTWEIGHT` or `RH`.
- If an **EO** is completed, the **next ES** is **postponed by 4 months** from the EO date.
- An employee is **late** if it has been more than 4 months since the **last ES completed**, unless an EO was completed in the meantime.

## Scenarios
#### ES every 4 months
- Last ES on **01/01/2024**, we are **01/05/2024**
    - => I am **NOT LATE**
    - => Next ES **TODAY**
- Last ES on **01/01/2024**, we are **01/06/2024**
    - => I am **LATE**
    - => Late of **1 MONTH**
  #### ES postponed if EO
- Last EO on **01/03/2024**, last ES before that on **01/01/2024**, we are **01/06/2024**
    - => Next ES is **postponed to 01/07/2024**
    - => I am **NOT LATE**
    - => Next ES in **1 MONTH**
- Last EO on **01/03/2024**, no ES since, we are **01/08/2024**
    - => I am **LATE**
    - => Late of **1 MONTH
#### Lightweight Career Tracks
- My career track is `LIGHTWEIGHT`, we are **any date**
    - => I am **IGNORED** for ES
- My career track is `RH`, we are **any date**
    - => I am **IGNORED** for ES