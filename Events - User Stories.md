# 1. Constants
- **Goals Interview Interval** = 1 year
- **Professional Interview Interval** = 2 years
- **Professional 6Y Interview Interval** = 6 years
- **Follow-Up Interview Interval** = 4 months
- **Default Goals Campaign Start Date** = 1st October
- **Goals Campaign Inclusion Interval for new Hires** = 1st February to 31st March

# 2. Goals Interview (EO)
## Overview
- A EO every year
- An employee is late if it has been more than 1 year since the **last EO completed**
- A new hire is late if it has been more than 1 year since its **hiring date**

## Scenarios
- I was hired the **01/01/2023**, we are the **01/08/2023**
	- => I am **NOT LATE**
	- => Next EO in **5 MONTHS**
- I was hired the **01/01/2023**, we are the **01/01/2024**
	- => I am **NOT LATE**
	- => Next EO in **TODAY**
- I was hired the **01/01/2023**, we are the **01/04/2024**
	- => I am **LATE**
	- => Late of **3 MONTHS**
- I completed the previous EO the **01/01/2023**, we are the **31/12/2023**
	- => I am **NOT LATE**
	- => Next EO in **1 DAY**
- I completed the previous EO the **01/01/2023**, we are the **01/01/2024**
	- => I am **NOT LATE**
	- => Next EO in **TODAY**
- II completed the previous EO the **01/01/2023**, we are the **02/01/2024**
	- => I am **LATE**
	- => Late of **1 DAY**

Great! You’ve detailed the constants and logic for the **Goals Interview (EO)** part and are now moving on to the **Professional Interview (EP)** section. Let’s continue by building the **Professional Interview (EP)** section to match the format of the EO part:

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
- Last ES on **01/01/2024**, we are **01/05/2024**
    - => I am **NOT LATE**
    - => Next ES **TODAY**
- Last ES on **01/01/2024**, we are **01/06/2024**
    - => I am **LATE**
    - => Late of **1 MONTH**
- Last EO on **01/03/2024**, last ES before that on **01/01/2024**, we are **01/06/2024**
    - => Next ES is **postponed to 01/07/2024**
    - => I am **NOT LATE**
    - => Next ES in **1 MONTH**
- Last EO on **01/03/2024**, no ES since, we are **01/08/2024**
    - => I am **LATE**
    - => Late of **1 MONTH
- `career_track = "LIGHTWEIGHT"`, we are **any date**
    - => I am **IGNORED** for ES
- `career_track = "RH"`, we are **any date**
    - => I am **IGNORED** for ES