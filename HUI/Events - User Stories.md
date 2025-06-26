# 1. Constants
- **Goals Interview Interval** = 1 year
- **Professional Interview Interval** = 2 years
- **Professional 6Y Interview Interval** = 6 years
- **Follow-Up Interview Interval** = 4 months
- **Default Goals Campaign Start Date** = 1st October
- **Goals Campaign Inclusion Interval for new Hires** = 1st February to 31st March

# 2. Goals Interview (EO)
## Overview
- A **Goals Interview (EO)** is required **every year**, during a **campaign** period.
- By default, the campaign starts on next **1st October**.
- If a campaign is already planned, it starts at it's start date.
- A consultant participates to the campaign if he's in the company for 6 months or more.
- If a consultant doesn't participate to the campaign, he will participate to the one the following year.
- If a consultant is during an ongoing campaign:
	- His previous completed event was before the campaign : he's late
	- His previous completed event is during the campaign : he's not late - following campaign on next 1st october
- If the campaign has ended and the consultant has not done his event during, he's late.

### Objective:
Ensure each eligible consultant completes one **Goals Interview (EO)** per year during a defined **campaign period** (typically starting October 1st).

### **Campaign Schedule Logic**

1. **Default Campaign Start**:  
    If no campaign is currently planned in the system, the campaign starts on the **next October 1st** after today.
    
2. **Planned Campaign**:  
    If a campaign exists (retrieved from the DB), its `startDate` and `endDate` are used.
    
3. **Next Campaign Date**:
    - If the campaign is in the **future** (starts after today): return that future campaign’s start date.
    - If the campaign is **missing**: return the next default October 1st date.

### **Consultant Eligibility**

- A consultant is **eligible** to participate in a campaign if they have been employed for **6 months or more** by the campaign start date.
    
- If **not eligible**, the consultant will wait for the **next year's campaign**, by default October 1st + INTERVAL (here, 1 year).

### **Event Completion Rules**

When a campaign **exists** and the consultant is **eligible**:

| Scenario                        | Conditions                                                                                                             | Outcome                                                     |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| ✅ **Completed on time**         | `previousEventEndDate` is **after** campaign `startDate`                                                               | Return **next campaign start date** (next Oct 1st)          |
| ❌ **Late but campaign ongoing** | `previousEventEndDate` is **null or before** campaign `startDate` AND today is **before or within** campaign `endDate` | Return **campaign start date** (so event can still be done) |
| ❌ **Late and campaign ended**   | `previousEventEndDate` is **null or before** campaign `startDate` AND today is **after** campaign `endDate`            | Return **campaign end date** (indicating it’s overdue)      |

### **No Campaign Planned**

- If **no campaign exists** in the system but the consultant is eligible:
    - Return the **next default campaign start** (next October 1st).
        
- If consultant is **not eligible**, return the **next campaign start + INTERVAL**.

---

### 📋 **Test Matrix Design Based on Above Rules**

| Case | Campaign Exists | Hiring Date                            | `previousEventEndDate` | Today’s Date    | Expected Outcome            |
| ---- | --------------- | -------------------------------------- | ---------------------- | --------------- | --------------------------- |
| 1    | ✅               | >6 months before campaign              | ✅ during campaign      | During campaign | Next campaign start         |
| 2    | ✅               | >6 months before campaign              | ❌ before campaign      | During campaign | Campaign start              |
| 3    | ✅               | >6 months before campaign              | ❌ before campaign      | After campaign  | Campaign end                |
| 4    | ✅               | <6 months before campaign              | ❌                      | Before campaign | Next campaign + interval    |
| 5    | ❌               | >6 months before next default campaign | ❌                      | Any time        | Next default campaign start |
| 6    | ❌               | <6 months before next default campaign | ❌                      | Any time        | Next default + interval     |
| 7    | ✅ future        | >6 months before campaign              | ❌                      | Before campaign | Future campaign start       |
| 8    | ✅ future        | <6 months before campaign              | ❌                      | Before campaign | Future campaign + interval  |

### **Edge Cases to Test**

- Hiring exactly 6 months before campaign → Eligible.
    
- `previousEventEndDate == campaignStartDate` → Not "after", so **not on time**.
    
- No previous event but campaign ongoing → Still eligible → return campaign start.
    
- `campaign.endDate == today` → Still considered ongoing.
    
- `previousEventEndDate == today` → On time only if today is after `campaignStartDate`.

| Cas | Campagne | Date d’embauche         | `previousEventEndDate`        | Date actuelle           | Éligible ? | État de l’événement | Résultat attendu                            |
| --- | -------- | ----------------------- | ----------------------------- | ----------------------- | ---------- | ------------------- | ------------------------------------------- |
| 1   | ✅        | > 6 mois avant campagne | ✅ après `startDate`           | Pendant campagne        | ✅          | ✅ À jour            | `nextCampaignStartDate` (campagne suivante) |
| 2   | ✅        | > 6 mois avant campagne | ❌ avant `startDate`           | Pendant campagne        | ✅          | ❌ En retard         | `campaignStartDate` (peut encore le faire)  |
| 3   | ✅        | > 6 mois avant campagne | ❌ avant `startDate`           | Après campagne          | ✅          | ❌ En retard         | `campaignEndDate` (campagne terminée)       |
| 4   | ✅        | < 6 mois avant campagne | ❌                             | Avant campagne          | ❌          | ✅ À jour            | `nextDefaultCampaignStart`                  |
| 5   | ❌        | > 6 mois avant 01/10    | ❌                             | N’importe quand         | ✅          | ❌ En retard         | `nextDefaultCampaignStart` (01/10 prochain) |
| 6   | ❌        | < 6 mois avant 01/10    | ❌                             | N’importe quand         | ❌          | ❌ Inapplicable      | `nextDefaultCampaignStart`                  |
| 7   | ✅ future | > 6 mois avant campagne | ❌                             | Avant campagne          | ✅          | ❌ Pas encore fait   | `campaignStartDate`                         |
| 8   | ✅ future | < 6 mois avant campagne | ❌                             | Avant campagne          | ❌          | ❌ Inapplicable      | `nextDefaultCampaignStart`                  |
| 9   | ✅        | Exactement 6 mois avant | ❌                             | Avant campagne          | ✅          | ❌ Pas encore fait   | `campaignStartDate`                         |
| 10  | ✅        | 1 jour < 6 mois avant   | ❌                             | Avant campagne          | ❌          | ❌ Inapplicable      | `nextDefaultCampaignStart`                  |
| 11  | ✅        | > 6 mois                | == `startDate`                | Pendant campagne        | ✅          | ❌ En retard         | `campaignStartDate`                         |
| 12  | ✅        | > 6 mois                | == `today` (pendant campagne) | Pendant campagne        | ✅          | ✅ À jour            | `nextCampaignStartDate`                     |
| 13  | ✅        | > 6 mois                | null                          | Pendant campagne        | ✅          | ❌ Non réalisé       | `campaignStartDate`                         |
| 14  | ✅        | > 6 mois                | null                          | Après campagne          | ✅          | ❌ Non réalisé       | `campaignEndDate`                           |
| 15  | ✅        | > 6 mois                | ✅ après `startDate`           | Après campagne          | ✅          | ✅ À jour            | `nextCampaignStartDate`                     |
| 16  | ✅        | > 6 mois                | null                          | Aujourd’hui = `endDate` | ✅          | ❌ Non réalisé       | `campaignStartDate` (encore temps)          |

## Scenarios
#### EO for New Hires
- **Hired 15/02/2024**, current date: **01/10/2024**
    - Participates in **2024 campaign**
    - => **NOT LATE**
    - => EO due **now**
- **Hired 01/01/2024**, current date: **01/10/2024**
    - Participates in **2025 campaign**
    - => **NOT LATE**
    - => EO due in **1 year**
- **Hired 01/05/2024**, current date: **01/10/2024**
    - Participates in **2025 campaign**
    - => **NOT LATE**
    - => EO due in **1 year**
#### No previous EO campaign
- **Hired 01/02/2023**, no complete EO campaign yet, current date: **01/08/2023**
    - No campaign yet, first one will start **01/10/2023**
    - => **NOT LATE**
    - => EO due in **2 MONTHS**
- **Hired 01/02/2023**, no complete EO campaign yet, current date: **01/12/2023**
    - Ongoing campaign started **01/10/2023**, not terminated yet
    - No EO completed
    - => **LATE**
    - => Late of **2 MONTHS**
####  Existing previous EO campaign
- Last EO campaign started **01/10/2022**, current date: **01/10/2023**
    - New campaign starts **today (01/10/2023)**
    - => **NOT LATE**
    - => EO due **today**
- Last EO campaign started **01/10/2022**, no EO completed since, current date: **01/12/2023**
    - Current campaign started **01/10/2023**
    - => **LATE**
    - => Late of **2 MONTHS**
- Last EO campaign started **01/10/2023**, EO completed on **01/10/2023**, current date: **01/09/2024**
    - No ongoing campaign yet
    - => **NOT LATE**
    - => Next EO in **1 MONTH**
- Last EO campaign started **01/10/2023**, last EO completed on **01/10/2023**, current date: **01/11/2024**
    - Current campaign started **01/10/2024**
    - => Late of **1 MONTH**
- Last EO campaign started **01/10/2023**, last EO completed on **01/10/2022**, current date: **01/11/2024**
    - Current campaign started **01/10/2024**
    - => Late of **1 MONTH**
# 3. Professional Interview (EP and EP6)
## Overview
- An **EP** must be conducted every **2 years**.
- An **EP6** must be conducted every **6 years**, instead of the **EP**
- An employee is **late for EP** if it has been more than **2 years** since the **last EP completed**.
- A new hire is **late for EP** if it has been more than **2 years** since their **hiring date**.
- An employee is **late for EP6** if it has been more than **6 years** since the **last EP6 completed**.
- A new hire is **late for EP6** if it has been more than **6 years** since their **hiring date**.
- If an **EP6** should take place the same year than an **EP**, then the **EP** is postponed of 2 years.

## Scenarios
#### EP for New Hires
- I was hired the **01/01/2023**, we are the **01/08/2024**
    - => I am **NOT LATE** for EP / EP6
    - => Next EP in **1 YEAR and 5 MONTHS**
    - => Next EP6 in **5 YEARS and 5 MONTHS**
- I was hired the **01/01/2022**, we are the **01/01/2024**
    - => I am **NOT LATE** for EP / EP6
    - => Next EP **TODAY**
    - => Next EP6 in **5 YEARS**
- I was hired the **01/01/2021**, we are the **01/04/2024**
    - => I am **LATE** for EP
    - => I am **NOT LATE** for EP6
    - => Late of **3 MONTHS** for EP
    - => Next EP6 in **4 YEARS and 9 MONTHS**
#### EP every 2 years
- I completed the previous EP the **01/01/2022**, we are the **31/12/2023**
    - => I am **NOT LATE** for EP / EP6
    - => Next EP in **1 DAY**
    - => Next EP6 in **4 YEARS
- I completed the previous EP the **01/01/2022**, we are the **01/01/2024**
    - => I am **NOT LATE** for EP / EP6
    - => Next EP **TODAY**
    - => Next EP6 in **4 YEARS**
- I completed the previous EP the **01/01/2022**, we are the **02/01/2024**
    - => I am **LATE** for EP
    - => I am **NOT LATE** for EP6
    - => Late of **1 DAY** for EP
    - => Next EP6 in **4 YEARS**
#### EP6 after 6 years
- I was hired the **01/01/2018**, we are the **01/01/2024**
	- => I am **NOT LATE** for EP / EP6
	- => Next EP6 **TODAY**
	- => Next EP in **2 YEARS**
- I was hired the **01/01/2018**, we are the **01/01/2023**
	- => I am **NOT LATE** for EP / EP6
	- => Next EP6 in **1 YEAR**
	- => Next EP in **3 YEARS**
- I was hired the **01/01/2018**, we are the **01/01/2025**
	- => I am **NOT LATE** for EP
	- => I am **LATE** for EP6
	- => Late of **1 YEAR** for EP6
	- => Next EP in **1 YEAR**


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