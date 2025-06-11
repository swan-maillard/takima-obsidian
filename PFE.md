
```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 3 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```

## **Résumé**

Ce rapport présente le travail réalisé dans le cadre de mon Projet de Fin d’Études (PFE) chez Takima, une ESN basée à Paris. J'ai été intégré à l’équipe en charge du développement de l’application interne HUI, un outil de gestion RH et managérial. J’ai participé à son amélioration continue à travers trois axes principaux : la création d’un module de feedbacks pour les consultants, l’amélioration du module de gestion des entretiens, et l’optimisation des pipelines CI/CD. Ce projet, en plus d'apporter une valeur ajoutée à l'entreprise et à faire monter en compétence les consultants, contribue à un meilleur suivi des consultants, plus gratifiant. Ce rapport détaille le déroulement du stage sur les 6 mois, l’ensemble des choix techniques que j'ai pu effectuer, et les résultats que j'ai fourni à l'issu du PFE. Enfin, j'explorerai les évolutions futures des projets auxquels j'ai participé.

---

## **Abstract**

_(Traduction en anglais du résumé ci-dessus)_

---

## **Introduction**

Au cours d'un stage de 6 mois effectué dans l'entreprise Takima, j'ai pu mettre en oeuvre mon **Projet de Fin d'Etudes** (PFE) et clore ainsi ces 5 dernières années d'études à l'INSA Lyon, et plus particulièrement les 3 dernières années au département Informatique.

Takima est une Entreprise de Services du Numérique (ESN) fondée en 2000 par , d'abord sous le nom d'E-business-information. Basée à Paris et comptant plus de 200 employés, le rôle de Takima est d’accompagner des clients - en général d'autres entreprises - à mettre en oeuvre des projets numériques allant du développement d'applications web à la gestion d'infrastructure. Pour se démarquer des autres ESN, Takima mise sa stratégie sur un accompagnement et une formation importante des nouveaux arrivants.

Afin de continuer à former ses consultants en inter-missions et ses nouveaux employés sur les technologies à l'état de l'art, tout en répondant à des besoins internes à l'entreprise, Takima a ouvert divers projets internes. Parmi ces projets figure **HUI**, une application web interne destinée aux RH et aux managers afin de suivre les parcours professionnels des consultants, leurs divers entretiens, leurs formations, leurs missions et les événements marquants de leur carrière. HUI a été pensée pour répondre aux besoins spécifiques de Takima, et vient s'interconnecter avec les autres applications internes de l'entreprise - permettant une gestion plus fine que ce que les solutions du marché pouvaient apporter.

Bien que l’application HUI soit déjà déployée et entièrement fonctionnelle, elle est encore en phase d’amélioration continue - tant au niveau de ses fonctionnalités qu'au niveau de son intégration dans l'infrastructure informatique de Takima.

Mon Projet de Fin d'Etudes s'inscrit donc dans ce besoin d'amélioration continu à travers divers objectifs me permettant de monter en compétences sur différents aspects de l'informatique en entreprise. Les objectifs m'ayant été fixés sont les suivants :

- Concevoir et développer un **module de feedback** permettant aux managers et aux clients de formuler des retours sur les consultants. Un effort particulier doit être mis sur le respect des règles de l'entreprise et règles RGPD quand au contenu et aux politiques de conservation des feedbacks.

- Enrichir le **module de gestion des entretiens** afin d'offrir une vue des managers ayant des entretiens en retard avec leurs consultants.
    
- Optimiser le processus **d'intégration continue** et **déploiement continu** de l'application dans l'infrastructure de l'entreprise, et mise en place de **bonnes pratiques DevOps**.

Le projet s'est déroulé au sein de l'équipe HUI dans un cadre agile, en suivant une organisation en sprints : approche itérative avec une livraison de nouvelles fonctionnalités toutes les 2 semaines. J'ai ainsi participé à toutes les cérémonies Scrum (daily meetings, poker planning, rétrospectives, reviews) et à la définition et conception des besoins. Ce mode de fonctionnement m'a permis de m'intégrer progressivement et de monter rapidement en compétences.

Ce rapport est découpé en six grandes parties. Je vais d'abord présenter le déroulement du stage et mon intégration dans le projet, puis je ferai une étude de l'existant à mon arrivée - sur l'état technique de HUI et sur les pratiques DevOps actuelles. Je développerai ensuite les propositions techniques majeures que j'ai apportées durant le PFE, ainsi qu'une réflexion sur les enjeux environnementaux et sociétaux liés au projet. Enfin, je proposerai un bilan personnel des compétences acquises et de l'expérience professionnelle que ce stage m'aura apporté, puis quelques perspectives futures concernant le projet.


---

## **1. Déroulement du stage**

### **1.1. Welcome Pool**

La première semaine du stage a commencée par la **Welcome Pool**, une semaine d'intégration intensive commune à tous les nouveaux stagiaires. Nous sommes une dizaine de stagiaires a être arrivés en février. Répartis en équipes de quatre, nous avons dû développer et déployer une application simple en utilisant JEE (Java Entreprise Edition) sans utiliser de gestionnaire de dépendances, et sans être guidé. A la fin de la semaine, nous avons effectué une simulation de présentation client, afin d'évaluer nos compétences techniques et relationnelles.

La Welcome Pool, bien qu'intensive, nous a permis de nous familiariser directement avec l’exigence de Takima mais a également permis de renforcer la cohésion d'équipe avec les autres stagiaires.

### **1.2. Formation approfondie**

Les deux mois suivants la Welcome Pool, j'ai eu la chance de participer à la formation **Master 3** de Takima, qui consiste en une mise à niveau intense centrées sur les différentes thématiques importantes aux consultants en développement web.

Cette formation était structurée autour d'un fil rouge : le développement back et front, la mise en place de pipelines CI/CD et le déploiement d'une application web de marketplace. Chaque chapitre était décomposée en cours théoriques, en pratique individuelle, et ponctuée par des revues de code de la part de consultants expérimentés.

Nous avons ainsi été formé sur les technologies suivantes :

- **Dev / DevOps** : Git, Docker, Docker Compose, GitLab CI/CD, TDD, tests unitaires

- **Back-end** : Java, Maven, REST APIs, Spring (Boot, MVC, Data), Hibernate, JPA, PostgreSQL, Flyway

- **Front-end** : JavaScript/TypeScript, React, Angular

Les cours et les revues de code étaient assurées par des développeurs seniors qui partageaient non seulement leurs compétences techniques, mais aussi leurs années de bonnes pratiques concrètes.
Bien que cette formation ne fasse pas à proprement parler de mon Projet de Fin d'Etudes, elle a largement consolidé mon socle technique et m'a permis d'acquérir de nombreux bons réflexes.

### **1.3. Intégration au projet HUI

Début avril, j'ai finalement intégré l'équipe en charge de **HUI** afin de commencer mon PFE. Comme expliqué dans l'introduction, HUI est une application interne centralisant les événements clés de la carrière des consultants afin d'assurer le suivi RH et managérial.

Les premiers jours m'ont permis de découvrir le contexte du projet, d'intégrer la code base et l'environnement de développement à mon ordinateur, et de lire les documentations utilisateur et technique. Bien que la code base ne soit pas énorme comparé à celles que l'on peut trouver dans des grosses entreprises, elle est significativement plus conséquente que tout ce que j'ai pu voir dans un contexte scolaire, et il a fallu un certain temps d'adaptation. De plus, HUI s'interface avec plusieurs outils utilisés au sein de Takima, comme SAP pour la gestion des employés, Google Apps, ainsi que des services de signature électronique pour la gestion des entretiens légalement obligatoires (entretiens d'objectifs et entretiens professionnels).

Le projet suit une méthodologie agile, c'est-à-dire que l'on adopte une approche flexible et réactive face aux évolutions des besoins formulés par le client (ici les client est Takima). Cela permet de proposer des déploiements en production plus fréquents, et de travailler de manière itérative, en amélioration continue. En pratique, HUI implémente cette agilité via la méthode Scrum : des sprints de 2 semaines et diverses cérémonies agiles. L'équipe est composée de huit développeurs et d'un référent technique, mais il n'y a pas de Scrum Master ni de Product Owner : nous sommes tous responsable de l'organisation du projet, de la communication avec les utilisateurs finaux (les managers et les RH) et des définition des besoins.

Dans le cadre de cette méthode Scrum, j'ai activement participé au cérémonies agiles suivantes :
- daily meetings,
- poker plannings,
- backlog refinements,
- sprint reviews,
- sprint retrospectives

Durant chaque sprint - un sprint correspondant à une itération de 2 semaines entre deux présentations client - les tâches sont planifiées et suivies via l'application Jira, afin de pouvoir développer efficacement en équipe.

Chaque fonctionnalité développée suit le processus suivant :
- revue du code par un autre membre de l'équipe,
- phase de QA (assurance qualité) par un autre membre de l'équipe afin de s'assurer que la fonctionnalité fonctionne correctement sur un environnement proche de celui de la production,
- si la revue de code et la phase de QA ont été validées, la fonctionnalité est marquée comme terminée.

De plus, chaque jour un différent membre de l'équipe est assigné en tant que *firefighter* et est chargé de détecter et de corriger tout incident en production.

---

## **2. État de l’art et étude de l’existant**

### **2.1 Solutions du marché**

Aujourd'hui, le marché de la gestion d'entreprise offre plusieurs solutions logicielles pour la gestion RH et managériale. Ces solutions sont progressivement apparues suite au besoin qui s'est fait ressentir de la part des entreprises d'avoir une vision plus globale de leurs employés, et de pouvoir correctement les suivre et récompenser leurs efforts. Parmi les solutions les plus connues, on peut citer :

- **Workday** : solution très complète, utilisée majoritairement par les grandes entreprises pour la gestion des employés, la paie, les entretiens, le recrutement et la formation.

- **Lucca** : solution française dédiée aux PME/ETI, offrant des outils de gestion des congés, des notes de frais, des entretiens annuels, du temps de travail, etc.

Bien que ces solutions soient complètes et relativement flexibles, elle présentent des limitations, notamment lorsqu'il s'agit de répondre à des besoins d'entreprises plus spécifiques ou à une organisation interne peu conventionnelle.

### **2.2 Limites de ces solutions pour Takima**

Takima est une entreprise qui souhaite mettre le suivi des consultants en avant. L'organisation de la hiérarchie est pensée horizontalement afin de réduire la distance entre un manager et un consultant et de prôner un suivi qualitatif des carrières, centrée sur l'implication du consultant.

Dans ce contexte, les outils du marché se révèlent être trop généralistes. Ils ne permettent pas de suivre avec précision les événements spécifiques auxquels Takima accorde de la valeur. Ces solutions sont également moins flexibles pour s'intégrer aux autres outils internes de Takima.

Ce sont ces limites qui ont amenées Takima à développer leurs propres outils de gestion RH et managériale. HUI n'est pas la seule application interne développée, il y a par exemple Itewa qui s'occupe de la gestion RH pure comme le suivi du temps de travail, des congés, des paies et des notes de frais. Une autre application, Tima, est centrée sur les processus de recrutement. Avec HUI pour gérer la carrière des employés, Takima s'est développer une vraie suite applicative interne et interconnectée permettant de répondre aux besoins spécifiques et à la culture de l'entreprise.

### **2.3 Architecture et modules de HUI**

HUI est une application monolithique reposant sur des stacks modernes :

- **Back-end** : API REST en **Kotlin** avec **Spring Boot**, structurée selon une architecture par fonctionnalité (*by feature*) pour faciliter l'ajout de nouvelles fonctionnalités.

- **Front-end** : Single Page Application (SPA) développée en **React** avec **TypeScript** et utilisant la librairie de composant **Antd** pour offrir une expérience utilisateur (UX) plaisante.

- **Base de données** : **PostgreSQL**, utilisée avec **Flyway** pour le versionnage des schémas et la gestion des migrations.

- **CI/CD** : Automatisation des builds, des tests et du déploiement vue **Gitlab CI**, **Docker** et **Kubernetes / Helm** pour l'orchestration. 

- **Monitoring et qualité de code** : **Sentry** est utilisé pour la gestion des erreurs en prod, **SonarQube** pour l'analyse statique de la qualité de code (duplication, couverture de tests, etc.), et **ArgoCD** et **Rancher** assurent le suivi des pods SonarQube sur les différents environnements (dev, preprod et prod).


Lorsque j'ai rejoint le projet, HUI était déjà déployée fonctionnelle, déployée en production et utilisée. Les modules suivants étaient déjà en place :

- Un module **d'encadrement** avec un suivi des managers, la possibilité d'assigner des managers aux consultants, d'assigner des coachs aux managers débutants, et enfin de programmer des formations en interne.

- Un module de **campagne d'entretiens** afin de gérer les périodes durant lesquelles les entretiens ont lieu. Divers types d'entretiens sont gérés par HUI, comme les entretiens d'objectifs, les entretiens professionnels (tous les 2 et 6 ans), les entretiens de suivi, mais également les événements moins formels comme les "One to one", ou les team building.

- Un module **d'événement clé des employés**, afin de suivre l'évolution des carrières et de garder une trace des événements marquants auxquels ils ont participé. On y retrouve leurs missions, leurs certifications, les conférences qu'ils ont données, les articles écrits, etc. Ces événements clés sont visibles sous forme de timeline sur le profil du consultant.

- Un module de **gestion des missions** pour visualiser les différentes missions en cours et les consultants et commerciaux assignés.

- Une **page consultant** récapitulant toutes les informations liées à un consultant, comme ses formations, ses derniers entretiens, ses événements marquants, etc.

- Une liaison avec des systèmes tiers, notamment avec le micro-service interne **AppUser** qui fait la connexion entre les outils Takima et **SAP**, mais également avec le micro-service interne **Messaging** qui gère l'envoi des mails. Des outils externes comme **Google Apps** et **HelloSign** pour les signatures électroniques sont également intégrés à HUI. Enfin, HUI intègre **Keycloak** pour déléguer la gestion de l'authentification et des rôles / permissions.


### **2.4 Pratiques DevOps et CI/CD en entreprise**

Les pratiques DevOps ont pour objectif de rapprocher les équipes de développement (Dev) et d’exploitation (Ops) pour accélérer les cycles de développement et fiabiliser les livraisons.

En entreprise, ces pratiques s’appuient généralement sur des **pipelines CI/CD (Continuous Integration / Continuous Deployment)** automatisés. Leur rôle est de :

- **Intégrer en continu** les nouvelles fonctionnalités, en assurant leur bon fonctionnement via des tests automatisés.
    
- **Déployer automatiquement** les applications dans des environnements de test, de préproduction ou de production, selon des règles prédéfinies.
    
- **Réduire les erreurs humaines** et les délais entre la création d’une fonctionnalité et sa disponibilité pour les utilisateurs.
    
- **Améliorer la traçabilité** et la reproductibilité des déploiements.
    

Chez Takima, ces pratiques sont largement adoptées. Les pipelines GitLab CI sont utilisés quotidiennement, avec des jobs dédiés au build, aux tests, à l’analyse statique de code (SonarQube), au packaging (Docker) et au déploiement (Kubernetes via Helm Charts et ArgoCD).

---

## **3. Propositions scientifiques et techniques**

### **3.1 Création du module de feedbacks**

#### **Objectifs et besoins fonctionnels**

Afin de mieux pouvoir suivre les consultants tout au long de leur carrière, qu'ils soient en interne ou chez un client, Takima a exprimé le besoin de pouvoir remplir des feedbacks sur les consultants. Ces feedbacks doivent permettre de tracer des retours qualitatifs réguliers sur les employés, en dehors des entretiens annuels classiques. Ils doivent pouvoir être remplis par les managers internes à Takima, mais également par les clients chez lesquels se trouvent le consultant. De tels feedbacks - qu'ils soient positifs ou négatifs - permettent un suivi plus fin et continu de la performance et de la progression de chaque employé, et facilitent la préparation des entretiens futurs.

Au moment où j'ai intégré le projet, la prise de feedback était gérée via un classeur Google Sheets, partagé par la direction des opérations. Les managers pouvaient remplir leurs commentaires via un formulaire Google Form, et chaque feedback devait ensuite être traité et transféré dans le Google Sheet par un.e responsable.

Nous avons organisé des réunions avec les utilisateurs finaux afin de correctement définir le besoin, et ensuite concevoir les différentes user stories. Chaque user story correspond à une fonctionnalité du module, et peut être assimilé à un "parcours utilisateur" : tel utilisateur ayant tel droit, pourra voir telle page, et effectuer telle action qui aura telle répercussion sur le reste du système. Les user stories sont définies en tant que ticket dans l'application Jira. 
Lors des cérémonies de Poker Planning, nous estimons la complexité de chaque ticket afin de pouvoir planifier notre sprint (période de 2 semaines de travail) et ainsi chiffrer un devis auprès du client. Ici, le client est Takima, donc nous ne chiffrons par réellement de devis, mais cette méthode de travail nous entraîne pour les missions chez des clients.

Nous avons donc pu définir les exigences fonctionnelles suivantes :
- Un manager peut créer un feedback sur un consultant. Le manager peut également jouer le rôle de rapporteur, et inscrire un feedback au nom du client.
- Un feedback est horodaté. Les dates de création et de dernière modification sont enregistrées.
- Les feedbacks doivent pouvoir être rédigé à un format "Notion-like". Notion est une application de prise de note possédant un éditeur augmenté : il est possible de formater le texte (gras, italique, etc.), de rajouter des titres et des sections, des url, des extraits de code, des images, etc. Notion est largement adopté au sein de Takima, et les managers souhaitent pouvoir utiliser toutes ses fonctionnalités lors de la rédaction d'un feedback.
- Lorsqu'un feedback est créé, il est enregistré à l'état de "brouillon".
- Un feedback peut être marqué par un tag `warning` s'il est prioritaire.
- Un feedback peut être marqué par des tags de catégories.
- Certains employés ont le rôle de "validateur de feedback". Ils ont donc accès à une interface listant tous les feedback émis.
- Il est possible de filtrer les feedbacks sur différents champs, tels que le nom du consultant concerné, l'état du feedback ou les tags appliqués.
- Un validateur doit pouvoir automatiquement valider les feedback qu'il rédige, sans passer par l'état brouillon.
- Un validateur a également accès à une interface de validation. Cette interface permet de naviguer parmi les feedback à l'état brouillon. Il est alors possible de :
	- Refuser le feedback s'il ne suit pas les politiques de l'entreprise. Un feedback ne doit pas porter de jugement de valeur. Il doit seulement faire état de faits.
	- Valider le feedback s'il est jugé acceptable.
	- Modifier puis valider le feedback, si une simple modification est suffisante pour le rendre acceptable.
- Un feedback refusé doit être supprimé de la base de donnée. En effet, un consultant peut réclamer à tout moment l'intégralité des informations que Takima possède à son sujet. Dans ce contexte, et pour respecter les règles RGPD, il n'est pas possible de conserver des feedbacks qui ont été refusés car ne respectent pas les politiques de l'entreprise.
- Enfin, il faut pouvoir importer un document csv contenant les feedbacks des années précédentes. Le contenu du csv doit automatiquement être convertit au format Notion-like afin d'être cohérent avec le reste de l'application.

#### **Conception technique**

Avant de me lancer dans le développement, j'ai dû réfléchir à la conception technique des feedbacks, notamment leur intégration dans la base de données. L'entité `Feedback` a été introduite dans le modèle de données et contient :
- `id` (L'UUID du feedback)
- `subject_id` (référence au consultant concerné)
- `advisor_id`(référence à l'auteur du feedback)
- `creator_id` (référence au rapporteur du feedback)
- `feedback_content` (contenu du feedback au format Notion-like)
- `feedback_state` (état du feedback : brouillon, refusé, validé ou validé après modification)
- `feedback_context` (contexte dans lequel le feedback a été écrit : mission, formation, etc.)
- `creation_date` (date de création)
-  `last_modification_date` (date de dernière modification)
- `last_modification_user_id` (référence à l'utilisateur ayant effectué la dernière modification)
- `is_warning` (vrai si le feedback est annoté du tag `warning`)
- `tags` (liste facultative des tags associés au feedback)

Du côté API, il a également fallu concevoir les différents endpoints accessibles. Un endpoint permet de lier un URL à un contrôleur dont le but est d'effectuer des actions spécifiques et de renvoyer au client une réponse formatée. Nous utilisons le type d'architecture REST pour la conception de notre API, qui doit par conséquent suivre certaines bonnes pratiques :
- L'API doit exposer des **resources identifiables**. Dans le cas du module de feedback, la resource manipulée est le **feedback**, identifiable via son UUID.
- Les requêtes doivent suivre un certain formalisme avec les verbes d'actions HTTP : **POST** pour créer un feedback, **PUT** pour le modifier, **DELETE** pour le supprimer, etc.
- Les contrôleurs doivent renvoyer les codes HTTP prévisibles selon l'action effectuée : **200** pour un succès, **201** pour une création, **404** pour une resource introuvable, etc.

Les endpoints à développer sont donc les suivants :
- **GET /feedbacks** (renvoie la liste des feedbacks)

Sur le front-end, un **formulaire React/TypeScript** permet la création et l’affichage des feedbacks dans un composant réutilisable. L'intégration avec l’API a été réalisée en suivant les conventions REST existantes.

#### **Développement**

Le développement a été découpé en user stories, intégrées à un sprint Scrum. Le back-end Kotlin a été étendu pour exposer les endpoints `POST`, `GET` et `DELETE` liés aux feedbacks. Côté front, l’accent a été mis sur l’expérience utilisateur et l’intégration fluide avec la timeline existante.

#### **Tests et validation**

Les tests incluent :

- **Tests unitaires back-end** (service et repository)
    
- **Tests front-end** (affichage conditionnel, interactions)
    
- **Tests de bout en bout** manuels sur staging
    
- **Code review et QA par un pair**
    

Le module a été validé et déployé en production après une phase d’essai sur un environnement restreint.


### **3.2 Amélioration du module des entretiens**

#### **Analyse de l’existant**

Le module des entretiens existait déjà, mais souffrait de plusieurs limitations :

- Interface peu intuitive (manque de filtres, surcharge d’information)
    
- Difficulté à relier les différents types d’entretien entre eux (objectifs, suivi, annuel)
    
- Mauvaise gestion de l’historique (modifications non tracées, peu d’exports possibles)
    

#### **Cahier des charges**

Les améliorations souhaitées comprenaient :

- **Refonte UX** : interface plus claire avec filtres et affichage par consultant
    
- **Ajout de typage** des entretiens pour faciliter leur suivi (Objectif / Suivi / Professionnel / Annuel)
    
- **Historisation** des modifications (audit log)
    
- **Amélioration du PDF export** pour les entretiens
    

#### **Choix techniques**

La structure de la base a été revue pour introduire une **entité `EntretienType`**. Un système d’`AuditLog` générique a été mis en place côté back pour historiser les actions critiques (création, modification, suppression).

Côté front, le composant React a été refactoré pour utiliser `React Hook Form` et des hooks personnalisés, facilitant la lisibilité et la maintenance.

#### **Implémentation**

Le projet a été réparti sur deux sprints. Une migration Flyway a été introduite pour adapter la base de données. La logique métier a été découplée dans des services dédiés pour améliorer la testabilité.

#### **Résultats obtenus**

- **Expérience utilisateur fortement améliorée**
    
- **Gain de temps pour les managers** lors de la saisie et de la consultation
    
- Meilleure **traçabilité** des données RH
    
- **Retours utilisateurs positifs** dès le premier mois d'utilisation


### **3.3 Optimisation des pipelines CI/CD**

#### **Analyse de l’existant**

Les pipelines GitLab CI initiaux étaient :

- **Longs à exécuter** (~12 minutes en moyenne)
    
- **Redondants** (copie de logique entre différents jobs)
    
- **Peu maintenables** (fichiers `.gitlab-ci.yml` lourds et peu factorisés)
    

#### **Réorganisation avec GitLab Components**

Takima a amorcé la migration vers les **GitLab CI Components**, une fonctionnalité permettant de créer des templates réutilisables. J’ai participé à :

- La **création de jobs templates** (tests, build Docker, analyse Sonar)
    
- La **refactorisation** du fichier `.gitlab-ci.yml` principal
    
- La **centralisation de la logique** commune dans des includes partagés entre projets
    

#### **Benchmark des stratégies de caching**

Plusieurs stratégies ont été testées pour accélérer les pipelines :

- **Cache de dépendances Maven et Node** selon le hash du fichier `pom.xml` ou `package-lock.json`
    
- **Utilisation de Docker layer caching** sur runners auto-hébergés
    
- **Minimisation des jobs parallèles inutiles**
    

Des benchmarks ont été menés sur des branches de test, en comparant les temps d'exécution sur plusieurs runs successifs.

#### **Résultats et gains mesurés**

- **Réduction du temps moyen de build de 12 à 7 minutes**
    
- **Réduction du nombre de fichiers `.gitlab-ci.yml` par projet (de 3 à 1)**
    
- **Moins de 30% d’échecs dus à des erreurs transitoires de CI**
    

#### **Bonnes pratiques DevOps mises en place**

- **Linting YAML** et validation automatique des pipelines via GitLab CI Lint
    
- **Tagging systématique des images Docker**
    
- **Documentation** des composants partagés pour les futurs projets
    
- Mise en place d’un **guide de contribution DevOps** interne pour l’équipe HUI


---

## **4. Réflexions sur les enjeux environnementaux et sociétaux** 

- Réduction de l’empreinte carbone par l’optimisation des pipelines CI/CD
    
- Contribution à une meilleure qualité de vie au travail via les outils RH internes
    
- Accessibilité numérique : prise en compte dans les interfaces
    
- Sécurité des données RH : enjeu éthique et réglementaire
    
- Impacts du numérique responsable dans le cadre d’un développement interne
    

---

## **5. Bilan personnel**

- Compétences techniques acquises (React, GitLab CI/CD, DevOps, etc.)
    
- Compétences humaines et professionnelles (agilité, travail en équipe, gestion de projet)
    
- Réflexion sur la posture d’ingénieur dans une ESN
    
- Apports de cette expérience pour le futur professionnel

---

## **6. Conclusion et perspectives**

- Synthèse des apports du stage
    
- Impact global sur le projet HUI et pour Takima
    
- Limites du travail réalisé
    
- Pistes d’amélioration et de poursuite (ex : tests automatisés, analytics avancé, IA pour feedbacks RH...)

---

## **Bibliographie**

- Toutes les ressources citées dans le rapport : articles, documentation technique, normes, blogs professionnels...
    
- Format cohérent (APA, IEEE ou autre)    

---

## **Annexes** _(non comptabilisées dans les 30 pages)_

- Captures d’écran des interfaces
    
- Diagrammes (ex : architecture, pipelines GitLab)
    
- Extraits de code pertinents
    
- Exemples de requêtes ou de configurations
    
- Résultats bruts de benchmarks
