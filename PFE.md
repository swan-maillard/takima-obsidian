
```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 4 # Include headings up to the specified level
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

### **1.1 Welcome Pool**

La première semaine du stage a commencée par la **Welcome Pool**, une semaine d'intégration intensive commune à tous les nouveaux stagiaires. Nous sommes une dizaine de stagiaires a être arrivés en février. Répartis en équipes de quatre, nous avons dû développer et déployer une application simple en utilisant JEE (Java Entreprise Edition) sans utiliser de gestionnaire de dépendances, et sans être guidé. A la fin de la semaine, nous avons effectué une simulation de présentation client, afin d'évaluer nos compétences techniques et relationnelles.

La Welcome Pool, bien qu'intensive, nous a permis de nous familiariser directement avec l’exigence de Takima mais a également permis de renforcer la cohésion d'équipe avec les autres stagiaires.

### **1.2 Formation approfondie**

Les deux mois suivants la Welcome Pool, j'ai eu la chance de participer à la formation **Master 3** de Takima, qui consiste en une mise à niveau intense centrées sur les différentes thématiques importantes aux consultants en développement web.

Cette formation était structurée autour d'un fil rouge : le développement back et front, la mise en place de pipelines CI/CD et le déploiement d'une application web de marketplace. Chaque chapitre était décomposée en cours théoriques, en pratique individuelle, et ponctuée par des revues de code de la part de consultants expérimentés.

Nous avons ainsi été formé sur les technologies suivantes :
- **Dev / DevOps** : Git, Docker, Docker Compose, GitLab CI/CD, TDD, tests unitaires
- **Back-end** : Java, Maven, REST APIs, Spring (Boot, MVC, Data), Hibernate, JPA, PostgreSQL, Flyway
- **Front-end** : JavaScript/TypeScript, React, Angular

Les cours et les revues de code étaient assurées par des développeurs seniors qui partageaient non seulement leurs compétences techniques, mais aussi leurs années de bonnes pratiques concrètes.

A la fin de la formation, j'ai dû effectuer une simulation de présentation client de la market place fonctionnelle et déployée sur serveur que j'ai développé en intégralité durant les 2 mois.

![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUfXmQAMKhMJ7ctr5-OW5g-9IBZ9bMjva53-c2KvPqdGnpiRpKYDWTgh4hkZdmpay6iy4PsDQCgSjQEw5NL8Sx5-Okeo3E_iC10spyZN3GjRqUtAD9H69yk8F581GVP8FWMqPq3Wyg=s2048?key=_wr7buDxjlhSrQDWgzosB7PO)
Capture d'écran de la page d'accueil de la Market Place


Bien que cette formation ne fasse pas à proprement parler de mon Projet de Fin d'Etudes, elle a largement consolidé mon socle technique et m'a permis d'acquérir de nombreux bons réflexes.

### **1.3 Intégration au projet HUI

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

### **2.1 Solutions sur le marché**

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

Voici un diagramme résumant les technologies utilisées dans l'application :

![[Pasted image 20250614180130.png]]


Lorsque j'ai rejoint le projet, HUI était déjà déployée fonctionnelle, déployée en production et utilisée. Les modules suivants étaient déjà en place :

- Un module **d'encadrement** avec un suivi des managers, la possibilité d'assigner des managers aux consultants, d'assigner des coachs aux managers débutants, et enfin de programmer des formations en interne.

- Un module de **campagne d'entretiens** afin de gérer les périodes durant lesquelles les entretiens ont lieu. Divers types d'entretiens sont gérés par HUI, comme les entretiens d'objectifs, les entretiens professionnels (tous les 2 et 6 ans), les entretiens de suivi, mais également les événements moins formels comme les "One to one", ou les team building.

- Un module **d'événement clé des employés**, afin de suivre l'évolution des carrières et de garder une trace des événements marquants auxquels ils ont participé. On y retrouve leurs missions, leurs certifications, les conférences qu'ils ont données, les articles écrits, etc. Ces événements clés sont visibles sous forme de timeline sur le profil du consultant.

- Un module de **gestion des missions** pour visualiser les différentes missions en cours et les consultants et commerciaux assignés.

- Une **page consultant** récapitulant toutes les informations liées à un consultant, comme ses formations, ses derniers entretiens, ses événements marquants, etc.

- Une liaison avec des systèmes tiers, notamment avec le micro-service interne **AppUser** qui fait la connexion entre les outils Takima et **SAP**, mais également avec le micro-service interne **Messaging** qui gère l'envoi des mails. Des outils externes comme **Google API** et **HelloSign** pour les signatures électroniques sont également intégrés à HUI. Enfin, HUI intègre **Keycloak** pour déléguer la gestion de l'authentification et des rôles / permissions.

Voici le schéma d'architecture C4 qui décrit le contexte autour de HUI, ses composants principaux, et avec quels systèmes l'application interagit :

![[Pasted image 20250614180450.png]]

Un diagramme C4 plus détaillé, centré sur les couches services et contrôleurs de HUI est également disponible en Annexe.

### **2.4 Pratiques DevOps et CI/CD en entreprise**

Les pratiques DevOps ont pour objectif d'accélérer les cycles de développements et de fiabiliser les livraisons en automatisant les tâches qui ne sont pas directement liées au développement. En général, ces pratiques s'appuient sur des **pipelines CI/CD (Continuous Integration / Continuous Deployment)**. Ces pipelines ont pour objectif de :

- **Intégrer en continu** les nouvelles fonctionnalités développées en s'assurant de leur bon fonctionnement en faisant passer des tests automatisés ou en effectuant des analyses statiques de la qualité de code.

- **Déployer automatiquement** les applications dans des environnements de test, de préproduction et de production en s'assurant de la cohérence entre les différents environnements.

- **Réduire les erreurs humaines** car les tâches effectuées par les pipelines sont répétitives, et peuvent parfois mener à des erreurs des opérateurs lorsqu'elles ne sont pas réalisées automatiquement. 

- **Réduire les délais** entre l'ajout d'une nouvelle fonctionnalité ou d'un correctif et de sa disponibilité pour les utilisateurs finaux.

- **Améliorer la traçabilité** et la reproductibilité des tests et des déploiements..

Chez Takima, les pipelines CI/CD sont mises en place avec **Gitlab CI** qui permet de définir les comportements pour chaque étape de la pipeline, de la compilation au déploiement. Sur HUI, les pipelines sont utilisées quotidiennement : lorsqu'une branche (qui correspond à une fonctionnalité, une amélioration tech ou un correctif) est poussée sur Gitlab, une pipeline se déclenche automatiquement avec des jobs dédiés au build, aux tests, à l'analyse statique du code (analyse SonarQube) et au packaging (création d'image Docker et upload sur un registre d'image). Ainsi, avant même d'effectuer une revue de code, il est possible de s'assurer que tous les tests passent et donc que les modifications sont rétro-compatibles.

Lorsque la branche est validée (Revue de code et QA approuvées), des jobs permettent de déployer l'application sur les différents environnements (mise à jour des pods Kubernetes avec Helm Charts).

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
- **GET /feedbacks?page={page}&size={size}** (renvoie une liste paginée des feedbacks)
- **POST /feedbacks** (création d'un feedback)
- **PUT /feedbacks/{id}** (validation, refus ou modification d'un feedback)

Enfin, côté front-end, il a fallu créer de nouveaux composants. Le framework **React** utilisé sur HUI permet de créer des composants réutilisables dans diverses parties de l'application, et ainsi de rendre le code plus concis et maintenable. Les ajouts et modifications front que j'ai effectuées sont les suivantes :
- Ajout d'une page de création d'un feedback via un formulaire
- Ajout d'une page listant les feedbacks
- Ajout d'une page permettant de modifier et valider les feedbacks. Cette page contient :
	- Un encart avec la liste des feedbacks à valider,
	- Un encart avec les informations sur le feedback sélectionné, un champ de contenu modifiable au format Notion-like, et des boutons de validation et refus,
	- Des flèches pour naviguer entre les différents feedbacks à valider.


#### **Développement**

Le développement du module a duré environ deux mois. J’ai avancé progressivement en suivant les user stories définies au début du projet, en lien avec les utilisateurs finaux. Chaque fonctionnalité était liée à un ticket Jira qu’on estimait pendant les poker plannings. Pas mal d’allers-retours ont été nécessaires, surtout pour ajuster certains comportements métiers ou l’interface, en fonction des retours à la fin de chaque sprint.

Un des points un peu techniques a été l’intégration de l’éditeur Notion-like. On voulait vraiment garder l’expérience de rédaction qu’ont les managers dans Notion, donc j’ai dû chercher un éditeur React qui permette ça, et le customiser pour qu’il gère les cas qu’on voulait : mise en forme, tags, extraits de code, etc. L’import CSV a aussi demandé pas mal d’attention, notamment pour convertir proprement le contenu au format Notion-like.

La gestion des rôles (créateur, rapporteur, validateur) et des transitions d’état entre brouillon, validé, refusé, etc., a été un autre sujet important. Il fallait que tout soit cohérent, sans laisser la possibilité de contourner les règles par erreur ou oubli.

#### **Tests et validation**

Côté qualité, j’ai suivi la politique de couverture de tests à 80 %, mesurée avec SonarQube. Les tests unitaires ont été écrits pour les services et les repositories côté back. J’ai aussi ajouté des tests front pour vérifier que les bons éléments s’affichaient selon le rôle de l’utilisateur, et que les actions déclenchaient bien les bons appels API.

En plus des tests automatisés, j’ai fait des tests manuels complets sur l’environnement de staging, en simulant les différents parcours utilisateurs (création, validation, refus, etc.). Chaque ticket passait aussi par une phase de code review et de QA avec un autre membre de l’équipe. En théorie, on vise zéro bug en prod, mais dans la réalité il y a eu quelques petits retours après le déploiement. Heureusement, les retours des managers ont été rapides, ce qui a permis de corriger rapidement.

Le module est maintenant en prod, et les managers ont commencé à l’utiliser pour suivre les consultants. Les premiers retours sont globalement positifs, notamment sur l’ergonomie de la page de validation.

#### **Évolutions futures**

À terme, l’idée serait d’intégrer les feedbacks dans les entretiens annuels et les entretiens d’objectifs. Ça permettrait aux managers d’avoir une vue directe des retours précédents pendant la préparation de l’entretien, et de mieux suivre l’évolution du consultant dans le temps.

Une autre évolution prévue concerne le système de validation. Aujourd’hui, un feedback ne peut être modifié que par une seule personne à la fois, ce qui peut vite devenir bloquant. On réfléchit à un système qui permettrait à plusieurs validateurs d’intervenir en parallèle sans conflit (genre gestion de verrou ou édition concurrente). Il y a aussi l’idée d’ajouter des stats ou des indicateurs globaux à partir des feedbacks, mais ça demandera sans doute une autre phase de conception.

### **3.2 Amélioration du module des entretiens**

#### **Analyse de l’existant**

Un module d'entretiens, et plus généralement d'événements, avait déjà été développé sur Hui avant mon arrivée sur le projet. Ce module permet de créer des événements entre des employés (par exemple un entretien entre un manager et son consultant), puis de gérer tout le cycle de vie de l'événement. 

Il existe plusieurs types d'événements gérés par Hui :
- Les **Entretiens d'Objectifs** ont lieu tous les ans entre un manager et son consultant. Cet entretien a pour but de faire un tour d'horizon de ce que le consultant a réalisé durant l'année, ainsi que des possibles difficultés qu'il a pu traverser. C'est également le moment pour le consultant de négocier son augmentation de salaire et de définir ses objectifs pour l'année à venir.
- Les **Entretiens Professionnels** ont lieu tous les deux ans, généralement entre un représentant RH et un employé. Ces entretiens sont imposés par la loi. Il s'agit alors de discuter de l'évolution professionnelle de l'employé, afin de déterminer les différents axes sur lesquels Takima peut agir pour contribuer à cette évolution. Tous les **6 ans**, l'entretien professionnel est plus conséquent, afin de faire un bilan plus global sur la carrière de l'employé et de réfléchir son évolution à plus long terme.
- Les **Entretiens de Suivi** ont lieu tous les 4 mois. Il s'agit d'un entretien entre un manager et un consultant, plus court que les 3 précédents. L'objectif de l'entretien de suivi est de garder contact avec le consultant tout au long de l'année, et d'être capable de réagir si celui-ci a des problèmes chez le client pour lequel il travail. Certains consultants bénéficient d'un **suivi de carrière allégé**, auquel cas ils ne font plus l'objet d'un suivi régulier, et c'est au manager et au consultant d'organiser ces entretiens quand ils le souhaitent.
- Les **One to One** sont des entretiens informels entre deux employés. Ils ne font pas l'objet d'un suivi quelconque et peuvent porter sur n'importe quel sujet.
- Les **Team Buildings** sont des événements ludiques entre un manager et une équipe afin de renforcer leurs cohésion et d'apprendre à se connaître davantage.

Chaque manager peut accéder à la liste de ses événements avec ses managés, et y appliquer des filtres. Une fois un événement créé, il doit passer par une série d'étapes. Prenons l'exemple d'un entretien d'objectif :
1. Au moment de créer un entretien d'objectif, le manager doit spécifier le consultant concerné, la description de l'entretien, et des notes facultatives.
2. Une fois créé, l'entretien passe à l'étape "Brouillon". Le manager peut alors décider de modifier les participants, la description, ou les notes, puis de passer à l'étape "Rédaction".
3. En passant à l'étape "Rédaction", un document d'entretien Google Docs est automatiquement généré depuis un template. Le manager doit alors pré-remplir ce document en prévision de l'entretien. Il peut également faire une demande d'accompagnement, par exemple s'il s'agit du premier entretien qu'il anime.
4. Une fois la phase "Rédaction" terminée, le manager doit déterminer la date et l'heure de l'entretien afin de passer à la phase "Planifiée".
5. Lorsque l'entretien a été effectué entre les 2 partis, l'événement entre dans sa phase de "Signature". Il faut alors attendre que le manager et le consultant signe un document électronique attestant que l'entretien a eu lieu. Cette signature est automatiquement gérée via l'API Dropbox Sign. Une fois signé, le manager peut rentrer dans la phase de "Debrief".
6. Le manager est alors invité à remplir un Google Form pour débriefer l'entretien. Lorsqu'il a terminé, alors seulement l'entretien est considéré comme "Terminé".

Construit sur le module de gestion des événements, un module de **campagne d'entretien** a également été mis en place. Ce module permet de créer des campagnes pour les entretiens d'objectifs et professionnels. Ces campagnes visent à simplifier les processus d'entretiens, en les étalant automatiquement sur une période donnée. Les managers n'ont alors plus besoin de créer leurs entretiens individuellement : tous les champs seront pré-remplis au moment de la création d'une campagne.

A l'heure actuelle, le module de campagne n'a été intégré qu'aux entretiens d'objectifs, mais il est prévu de l'intégrer également aux entretiens professionnels dans le future proche.

Un nouveau besoin est ressorti de ce module d'entretien. Un rôle important au sein de Takima est celui de TOM (Tutors of Managers). Les TOM ont pour objectifs de guider et gérer les managers Takima. Sur HUI, les TOM ont accès à une page "Dashboard Manager", sur laquelle ils peuvent voir la liste de tous les managers Takima. Ils peuvent ensuite accéder aux informations détaillées de chaque manager. Pour offrir une vue globale des avancements de chaque entretien, les TOM souhaiteraient pouvoir visualiser les statuts des entretiens entre chaque manager et ses consultants.

#### **Cahier des charges**

Le premier besoin spécifié par les TOM était donc d'avoir une vue d'ensemble de l'avancement des entretiens pour chaque manager. Concrètement, le dashboard des managers doit afficher - en dessous de chaque manager - leur nombre d'entretiens en cours, en retard ou à venir avec les consultants qu'il encadre. Ces statistiques doivent être affichées pour les 3 types d'entretiens suivants :
- les entretiens d'objectifs,
- les entretiens professionnels,
- les entretiens de suivi.

Il doit également être possible de filtrer les managers en fonction des types d'entretiens en retard. La liste doit être triée selon le plus grand nombre d'entretiens professionnels en retard. Cela permettra aux TOM d'avoir un meilleur suivi des managers en période d'entretiens, et de pouvoir relancer ceux qui ont trop de retards.

En addition de cette vue globale des managers, les TOM voudraient avoir des statistiques plus détaillées sur le profil des managers. Pour chacun de leurs consultants managés, le profil doit afficher - pour chacun des 3 types d'entretiens énoncés précédemment - les informations suivantes :
- Si l'entretien est à venir, dans combien de temps il doit avoir lieu.
- Si l'entretien est en retard, de combien de temps il est en retard.
- Si l'entretien est en cours, à quelle étape il se trouve.

Après avoir pris connaissance de ce besoin initial, il a fallu définir un cahier des charges plus précis. Pour cela, j'ai participé à plusieurs réunions avec les TOM afin de discuter des différents cas de figure à gérer. Nous nous sommes rapidement rendu compte que la définition du besoin était plus difficile à rédiger que prévu. En effet, tous les types d'entretiens diffèrent dans leurs comportements, et ont chacun des subtilités propres.

Pour nous aider dans la rédaction du cahier des charges, nous avons défini des scénarios concrets auquel se référer pour chaque cas de figure. Cela nous a permit de mieux imaginer tous les scénarios possibles et de ne pas oublier de cas limites. Cette manière de faire est également idéale en prévision de la rédaction des tests unitaires et des tests d'intégration.

Pour chacun des types d'entretien, nous avons donc défini les règles suivantes à implémenter :

- **Entretien d'objectif (EO) :**
	- Règles...

- **Entretien professionnel (EP) :**
	- Règles...

- **Entretien de suivi (ES) :**
	- Règles...

#### **Conception technique**

La conception technique étant guidée par un besoin fonctionnel fort, de par le cahier des charges très détaillé, j'ai décidé d'utiliser une approche de Test-Driven-Development (TDD) côté back-end. Le TDD est une bonne pratique de développement, permettant de produire un résultat fonctionnel plus rapidement en minimisant l'apparition de bugs. Cette approche demande cependant de la rigueur, et force à correctement définir les besoins fonctionnels en amont. Il s'agit d'un bon entraînement pour moi qui ai en général l'habitude de commencer à développer directement tête baissée, puis de régler les bugs lorsqu'ils apparaissent, inévitablement.

Le principe du TDD est le suivant :
1. **Rédaction de tests qui échouent** :  
    On commence par écrire des **tests unitaires** qui expriment clairement ce que le code _doit faire_, sans encore l’avoir implémenté. Par exemple : "Si un manager n’a pas créé l’entretien d’objectif prévu pour l’année en cours, alors l’état doit être ‘en retard’". À ce stade, les tests échouent logiquement.
    
2. **Développement pour faire passer les tests** :  
    Ensuite, on développe **juste ce qu’il faut** pour que les tests passent. Pas de logique inutile ou d’optimisation prématurée : uniquement ce qui permet de faire valider la règle.
    
3. **Ré-factorisation du code** :  
    Une fois tous les tests passés, on repasse sur le code pour le **ré-factoriser**, le simplifier, ou le découper en fonctions plus lisibles – tout en s’assurant que les tests continuent de passer.

![[Pasted image 20250614185436.png]]
Schéma expliquant le Test Driven Development


Pour ce besoin fonctionnel, je n'ai pas eu besoin de créer de créer ou modifier les entités en base de données puisque toutes les informations nécessaires étaient déjà disponible. Les entités et leurs propriétés principales que j'ai dû utiliser sont les suivantes :
- **manager**
	- `user_id` (référence à l'utilisateur concerné)
- **users_link**
	- `parent_id` (référence au manager)
	- `child_id` (référence à l'employé managé)
	- `career_tracking` (type de suivi de carrière de l'employé : standard, allégé ou RH)
- **event**
	- `creator` (référence au créateur de l'entretien, en l'occurrence le manager)
	- `subject` (référence au sujet de l'entretien, en l'occurrence le consultant)
	- `event_type` (type de l'événement : entretien d'objectif, professionnel, de suivi, etc.)
	- `event_state` (état de l'événement : brouillon, rédaction, terminé, etc.)
	- `end_date` (date de fin de l'événement, null si non terminé)
- **campaign**
	- `event_type` (type de l'événement concerné par la campagne : entretien d'objectif, professionnel, etc.)
	- `start_date` (date de début de la campagne)
	- `end_date` (date de fin de la campagne, null si non terminée)

Les pages du dashboard manager et des profils manager existants déjà, je n'ai pas eu besoin de concevoir les endpoints API ni les composants React, mais seulement à y apporter des modifications afin d'y ajouter les informations concernant les états des entretiens pour chaque manager et employé managé.

J'ai également dû créer les composants React pour les filtres portant sur les types d'entretiens en retard, et sur la possibilité de dissocier les nombres d'EP en EP2 et EP6 (afin de faire la distinction entre les Entretiens Professionnels effectués tous les 2 ans et ceux effectués tous les 6 ans, plus importants). La logique de ces filtres a également dû être portée côté back.

#### **Développement**

Le développement de cette nouvelle fonctionnalité a duré environ **un mois**, réparti sur plusieurs sprints. Dès le début du développement, j’ai pu bénéficier de **retours réguliers de la part des TOM**, que ce soit via des échanges informels ou plus formellement lors des **Sprint Reviews**. Cela m’a permis d’itérer rapidement sur les écrans, d’ajuster la logique métier, et surtout de m’assurer que les spécificités métiers complexes autour des entretiens étaient bien respectées.

La plus grande difficulté rencontrée a été d’ordre **technique et organisationnelle**. Dans un premier temps, j’ai voulu **tout gérer dans une seule requête SQL**, avec un grand nombre de jointures, de branchement des différents cas et de sous-requêtes, afin de traiter tous les calculs (états, retards, filtres) directement côté base de données. L’idée initiale était d’avoir une solution optimisée et rapide.

Mais je me suis rapidement heurté à plusieurs limites :
- La requête était **difficile à lire** et donc à maintenir.
- Le moindre bug ou ajustement prenait énormément de temps à localiser.
- Impossible de **tester indépendamment chaque règle** métier.
- Le code back-end devenait un simple relais sans logique, ce qui le rendait **très rigide**.

Face à cela, j’ai fait le choix de **découper la logique**, en gardant :
- Une **requête SQL plus simple** et efficace, qui retourne tous les entretiens d’un manager avec les données brutes nécessaires.
- Puis de **déléguer la logique métier au back-end**, dans un service mieux découpé, testable, et plus facile à faire évoluer.

Bien que j'ai perdu du temps à passer d'une solution à l'autre, je pense avoir fait le bon choix en changeant de stratégie, car ça m’a fait gagner en clarté, et m’a permis de garder la main sur chaque règle en cas d’évolution future. Cela m'a également permis de mettre en place une plus grande couverture de tests unitaires et ainsi de pouvoir s'assurer que chaque bric de la fonctionnalité fonctionnent toujours correctement, même en cas de modification du comportement d'un type d'entretien.

Le développement côté front-end n'a pas posé de problèmes notables.

Voici une version enrichie et développée des sections **Résultats** et **Évolutions futures**, avec davantage de détails, d'analyse et de profondeur.

### **Résultats**

La refonte du module des entretiens et l’ajout de vues spécifiques pour les TOM ont généré plusieurs **résultats significatifs**, tant sur le plan fonctionnel que technique.

Grâce à la nouvelle vue d’ensemble, les TOM peuvent désormais **visualiser rapidement l’état d’avancement des entretiens**, par type et par manager. Ce tableau de bord, auparavant inexistant, est devenu un **outil central de pilotage RH** pour la direction managériale de Takima.

- Les TOM sont en mesure d’identifier les managers qui n’ont pas planifié ou finalisé certains entretiens.
    
- Ils peuvent prioriser leurs relances, en filtrant par type d’entretien (EO, EP, ES) et par niveau de retard.
    
- Cette fonctionnalité a permis une **meilleure coordination entre managers et TOM**, notamment pendant les périodes de campagnes.

Avant cette amélioration, le suivi des entretiens nécessitait **des extractions manuelles**, voire le croisement de données depuis des fichiers Google Sheets. Désormais :

- Toutes les données sont **centralisées dans HUI**, et **actualisées automatiquement**.
    
- Les managers peuvent voir en un coup d'œil les actions à entreprendre.
    
- Le **temps passé à relancer ou rechercher des informations a été réduit** de manière significative.

Le projet a aussi été l’occasion de **mettre en œuvre des méthodes de développement robustes**, comme le TDD (Test-Driven Development) et le découpage clair des responsabilités back/front. Cette rigueur s’est traduite par :

- Une **meilleure couverture de tests**, limitant les régressions.
    
- Une **logique métier centralisée** et plus facile à maintenir.
    
- Une **base technique saine** pour les évolutions futures.


Dès sa mise en ligne, le module a été **rapidement adopté par les TOM**, qui ont exprimé leur satisfaction lors des sprint reviews. Plusieurs retours positifs ont été notés :

- Simplicité d’usage, avec des interfaces **intuitives et bien intégrées**.
    
- Gain de visibilité sur les enjeux managériaux et RH.
    
- Une **relation renforcée entre managers et direction** grâce à une meilleure transparence des suivis.


### **Évolutions futures**

Bien que le module soit déjà pleinement fonctionnel et adopté, plusieurs pistes d’évolution ont été identifiées pour **renforcer encore son utilité, sa portée et son ergonomie**.

À ce jour, seules les campagnes d’**entretiens d’objectifs** sont automatisées. Étendre le système aux **entretiens professionnels** permettrait de :

- Planifier automatiquement les entretiens obligatoires tous les deux ans (et tous les six ans).
    
- Gérer efficacement les échéances légales via des dates de campagne spécifiques.
    
- Soulager les managers de la création manuelle des événements.


Permettre l’**export des entretiens au format CSV ou PDF** offrirait plusieurs avantages :

- Générer des bilans consolidés pour la direction ou les RH.
    
- Préparer plus facilement les revues RH annuelles ou les audits.
    
- Fournir un **accès hors ligne** aux données en cas de besoin.
    

Une évolution plus poussée pourrait même inclure un **tableau de bord exportable dynamique**, avec des graphiques ou des visualisations (camemberts, histogrammes).

Aujourd’hui, la relance des managers reste un processus manuel effectué par les TOM. Ajouter un **système de notifications automatiques** (email, Slack, voire intégration dans les calendriers) permettrait de :

- Réduire le nombre d’oubli ou de retard.
    
- Automatiser les relances à J-15, J-5 ou en cas de non-signature.
    
- Maintenir un rythme régulier dans la tenue des entretiens.


Centraliser tous les **documents liés aux entretiens et feedbacks** dans une timeline unique par collaborateur permettrait de :

- Suivre l’évolution d’un employé dans le temps (objectifs, feedbacks, mobilité…).
    
- Préparer les entretiens professionnels et bilans à 6 ans avec un historique riche.
    
- Donner plus de contexte aux managers, notamment en cas de changement de référent.

### **3.3 Optimisation des pipelines CI/CD**

#### **Analyse de l’existant**

Les différents projets internes à Takima - dont HUI - ont été mis en place avec une démarche de DevOps en tête. Concrètement, la volonté de Takima était de mettre en place des processus d'intégration continue (CI) et de déploiement continu (CD) afin d'automatiser au maximum le cycle de vie des projets, de la phase de développement jusqu'à la mise en production. L'objectif principal est de minimiser les erreurs humaines, d’accélérer les itérations de développement en se concentrant uniquement sur l'essentiel, et de garantir une meilleure qualité de livraison.

Lorsque je suis arrivé sur HUI, cette démarche DevOps était implémentée via la création de **pipelines CI/CD**. Ces pipelines définissaient une suite de tâches automatisées via Gitlab CI. Au moment de pousser des modifications de code sur Gitlab, une pipeline est automatiquement lancée afin d’exécuter les tâches suivantes :
- **Compilation** de l’application (build),
- **Exécution des tests** (unitaires et intégration),
- **Analyse statique du code** (qualité, couverture de code),
- **Packaging du code** en image Docker, stockée dans un container Gitlab, 
- **Déploiement** vers un environnement (développement, préproduction, production).

![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUdoCDvrwQUA4U-CgjUCDRQS3o1UgeMOkbXYZJ6kE0UNR__SW9qWbabgU0Z4B8tYesirEKPBavR39VQktNH7AiIUaUfurPBn80So98JncPR9yWiLYmFay_eaTj9bFfkRf_Y-NBDqLg=s2048?key=2z088As1guQ-ZA8-niVywg)
Schéma décrivant les pipelines CI/CD


Pour chaque projet, les pipelines sont définies dans des fichiers de configuration `.gitlab-ci.yml` décrivant les différentes étapes à exécuter. Chaque étape s'appelle un "job". Dans le cas de HUI, deux fichiers de configuration sont donc définis, pour l'API et pour le front-end.

Cependant, nous nous sommes rendu compte que les pipelines existantes souffraient de plusieurs défauts majeurs. Principalement, leur lenteur d'exécution. Pour HUI, les pipelines pouvaient prendre jusqu'à 30 minutes d'exécution. Dans un contexte agile, avec des livraisons fréquentes - et donc des lancements fréquents de pipelines - une telle lenteur d'exécution est un vrai frein à la productivité. Pour chaque nouvelle fonctionnalité, les pipelines sont lancées au minimum 3 fois : 
- Avant une revue de code lorsque la fonctionnalité est terminée,
- Avant une QA (assurance qualité) au moment de déployer en environnement de développement,
- Avant de fusionner avec la branche principale, lorsque la fonctionnalité est acceptée.

En plus de cela, si des retours apportés en revue de code ou en QA nécessitent des changements de code, une nouvelle pipeline sera lancée lorsque les modifications seront effectuées.

En addition à la baisse de productivité de l'équipe, ces temps d'attente sont également démotivants et peuvent jouer sur le moral de l'équipe. Personnellement, j'étais reluctant à effectuer des QA sur les tickets de mes collègues car je savais que cela impliquerait de lancer une pipeline.

Un autre point négatif de ces pipelines est la redondance des fichiers de configuration et leur manque de maintenabilité. Beaucoup de logique similaires sont copiées entre les différents `.gitlab-ci.yml`.

Etant intéressé par les problématiques DevOps en entreprise, Takima m'a proposé de me pencher sur le sujet d'optimiser les pipelines afin de réduire les temps d'exécution, et de généraliser les définitions des différents jobs afin de centraliser la logique et d'améliorer ainsi la maintenabilité des pipelines. L'idée était dans un premier temps d'apporter ces améliorations au projet HUI, puis dans un second temps - si ces modifications apportent un gain réel - d'étendre l'optimisation des pipelines à tous les projets internes.

#### **Réorganisation avec Gitlab Components**

Dans sa dernière version (v18.0), Gitlab a introduit les **Gitlab Components**. Les Components permettent d'extraire la logique des configurations CI/CD en templates réutilisables et modulaires.

Avant de me pencher sur l'optimisation des performances des pipelines, j'ai d'abord décidé d'extraire la logique des fichiers `.gitlab-ci.yml` et de les réorganiser en Gitlab Components. Pour cela, j'ai crée un nouveau projet appelé `gitlab-component` structuré de la manière suivante :

![[Pasted image 20250614123534.png]]

Le dossier `dockerfiles` définit des fichiers Dockerfile agnostiques au projet, permettant de générer l'image Docker d'une application. J'y ai par exemple défini un `Dockerfile-jre-alpine` qui génère une image Docker d'un projet Java à version variable. Cela permet de supporter des projets avec différentes versions de java, et de pouvoir simplement faire des montées de versions :

```Dockerfile
# Passed arguments
ARG JAVA_LTS_VERSION
ARG ARTIFACT_PATH

# Dynamic image name from java version
ARG IMAGE_NAME=registry.takima.io/school/proxy/eclipse-temurin:${JAVA_LTS_VERSION}-jre-alpine

FROM $IMAGE_NAME

# Create user for running executable
RUN addgroup -S takima -g 1000 && \
    adduser -S runner -G takima -u 1000 && \
    mkdir -p /app && \
    chown -R runner:takima /app

# Copy application jar compiled by the pipeline
COPY --chown=runner:takima $ARTIFACT_PATH /app/app.jar

USER runner

# Run the app
ENTRYPOINT exec java $JAVA_OPTS -jar /app/app.jar
```

Le dossier `templates` contient la logique réutilisable. Les components publics sont accessibles depuis les autres projets (par exemple depuis l'API et le front-end HUI), et peuvent utiliser des components privés. Voici les différents components que j'ai défini pour configurer un projet gradle (HUI API) et node (HUI front-end) :

![[Pasted image 20250614124801.png]]

Les components privés (`gitflow-ci.yml`, `package-kaniko.yml` et `deploy-k8s.yml`) définissent la logique commune à l'architecture et aux pipelines de tous les projets Takima. Ils permettent notamment de définir la gestion d'analyse statique de code, le packaging d'application en image Docker, et le déploiement sur les serveurs Kubernetes de Takima.

Les components publics (`backend-gradle` et `frontend-node`) sont construits par-dessus les components privés, et permettent de redéfinir la logique spécifique à chaque technologie, notamment pour les jobs d'installation de dépendances, de build et de tests.

Les Gitlab Components permettent également de définir des **inputs**. Les inputs sont des variables spécifiées par les projets faisant appel au components, permettant de généraliser les components et de les rendre agnostiques aux spécificités de chaque projet. Par exemple, `frontend-node` permet de définir les inputs suivants :

![[Pasted image 20250614130058.png]]

Ainsi, un même fichier de configuration de pipelines peut prendre en charge différentes versions de node, différents package managers, différents framework, etc.

Finalement, il suffit d'inclure le component dans le `.gitlab-ci.yml` du projet et de spécifier les inputs.

`.gitlab-ci.yml` de **HUI-API** :
```yaml
include:
  - component: $CI_SERVER_FQDN/taki-infra/gitlab-components/backend-gradle@1.1.10
    inputs:
      JAVA_LTS_VERSION: 21
      ARTIFACT_JAR_PATH: build/libs/hui-api.jar
      ARTIFACT_DIR_PATH: build
      TEST_RUNNER_SIZE: extra_large
      SONAR_PROJECT_KEY: "Hui-api"
```

`.gitlab-ci.yml` de **HUI-Front** :
```yaml
include:
  - component: $CI_SERVER_FQDN/taki-infra/gitlab-components/frontend-node@1.1.10
    inputs:
      NODE_LTS_VERSION: 22
      PACKAGE_MANAGER: yarn
      RUNNER_SIZE: large
      TEST_RUNNER_SIZE: extra_large
```

Vous aurez pu remarquer que l'on précise le tag `@1.1.10` derrière le nom du component utilisé. Ce tag permet de spécifier la version du component. En effet, les Gitlab Components permettent de versionner les fichiers de configurations, et ainsi de proposer des mises à jour de configurations rétro-compatibles pour les projets utilisant les pipelines.

L'annexe A montre le contenu du `.gitlab-ci.yml` de Hui-Front avant d'avoir implémenté les Gitlab Components.

#### **Optimisations des performances**

Une fois le code ré-factorisé, j'ai commencé à me pencher sur les problèmes de performances. Une mauvaise configuration des jobs de pipelines peut causer des baisses non-négligeables de performances, mais ce n'est pas évident de savoir quelles configurations causent ces lenteurs. J'ai donc commencé à investiguer les logs des différents jobs des pipelines afin de déterminer les goulots d'étranglements.

Je me suis rapidement rendu compte que les jobs ralentissaient significativement au moment de transférer et de télécharger le cache depuis un serveur cloud. Avant d'aller plus loin, il faut comprendre comment fonctionne le cache dans les pipelines.

Lorsque l'on compile une application, ses dépendances et librairies sont téléchargées. Plus un projet est gros, et plus son nombre de dépendances a des chances d'augmenter, et donc de prendre plus de temps à télécharger. Lors de l'exécution d'une pipeline, chaque job crée un nouvel environnement dans lequel effectuer ses tâches. Pour éviter d'avoir à re-télécharger les dépendances à chaque job, on met en place une stratégie de cache afin de stocker les dépendances téléchargées lors du premier job, et ainsi de pouvoir les réutiliser durant les autres jobs. Dans notre cas, le cache est stocké dans un serveur Amazon S3 (service de stockage managé dans le cloud). Avant d'être envoyé dans le S3, le cache est compressé par Gitlab, puis décompressé au moment de le récupérer. Cependant, ces opérations de compression et de décompression peuvent prendre un certain temps notamment quand les dépendances sont lourdes, et si le cache n'est pas correctement configuré, il peut facilement perdre tout son intérêt.

Prenons un exemple : Lorsque l'on construit une application front-end avec Node.js, on spécifie des dépendances dans le fichier `package.json`. La commande `npm install` permet d'installer toutes ces dépendances dans le dossier `node_modules/`. La pipeline effectue les jobs suivants :
-  **install dependencies** : installe les dépendances en exécutant la commande `npm install`
- **build** : compile l'application
- **tests** : effectue les tests unitaires et d'integration
- **sonarqube check** : effectue une analyse statique du code
- **package** : crée une image Docker de l'application et la stocke sur Gitlab
- **deploy** : déploie l'image Docker sur un environnement (dev, preprod ou prod)

Comme on peut le voir, les dépendances sont déjà téléchargées par le job `install dependencies`, et on ne veut pas avoir à les re-télécharger pendant au cours des jobs suivants. La solution qui avait été mise en place était donc d'ajouter du cache au niveau de chaque job afin de récupérer le contenu de `node_modules/` du cache et, s'il le cache est vide, d'installer les dépendances et de le stocker en cache. En spécifiant une clé correspondant à l'identifiant de la pipeline, les différents jobs d'une même pipeline peuvent donc se partager le cache :

```yaml
cache:
	key: IDENTIFIANT_DE_LA_PIPELINE
	paths:
		- node_modules/
	policy: pull-push
```

Sauf que cette façon de configurer le cache pose des problèmes :
- Tout d'abord, seuls les jobs de `build` et de `tests` ont besoin des dépendances. Ajouter le cache aux jobs suivants est inutile, ils perdront du temps à compresser et décompresser le cache pour rien.
- Ensuite, la stratégie de cache utilisée par défaut est celle de `pull-push`. Le job va récupérer le cache et le décompresse. S'il n'existe pas, alors il installe les dépendances. Puis, dans les deux cas, les dépendances sont compressées et renvoyées au cache, même si le cache existait déjà. Cela rajoute une étape de compression inutile pour `build`et `tests` puisqu'ils n'effectuent pas de modification sur les dépendances. Pour régler ça, il faut changer la stratégie de ces deux jobs en `pull` afin d'uniquement décompresser le cache. Seul le job d'`install dependencies` conserve la stratégie de `pull-push`.
- Enfin, en définissant la clé via l'identifiant de la pipeline, le cache est uniquement partagé au sein d'une même pipeline. Or, les dépendances restent souvent inchangées, et l'idéal serait que toutes les pipelines ayant les mêmes dépendances puissent réutiliser le cache. Puisque les dépendances sont définies dans le fichier `package.json`, on peut simplement hacher le contenu du fichier et utiliser ce hash en tant que clé.

![[Pasted image 20250614181803.png]]
Schéma de la gestion du cache non-optimisée : chaque job pull et push


![[Pasted image 20250614181843.png]]
Schéma de la gestion du cache optimisée : seuls les opérations nécessaires sont effectuées


Ainsi, on peut optimiser la gestion du cache ainsi :

```yaml
cache:
	key:
        files:
          - package.json
	paths:
		- node_modules/
	policy: pull-push (install dependencies) OU pull (build et tests)
```


De la même manière pour le projet **HUI-API** qui utilise le gestionnaire de dépendances **gradle**, les dépendances sont spécifiées dans le fichier `build.gradle.kts` et les dépendances sont téléchargées dans le dossier `gradle/caches/`, donc on peut définir le cache suivant :

```yaml
cache:
	key:
        files:
          - build.gradle.kts
	paths:
		- gradle/caches/
	policy: pull-push (install dependencies) OU pull (build et tests)
```


![[Pasted image 20250614182134.png]]
Meilleure gestion de la clé du cache avec le fichier de dépendances


J'ai également effectué quelques optimisations lors de la génération d'image Docker, en utilisant une image de base légère et minimale dite `alpine`. Cependant la simple optimisation du cache était déjà significativement efficace.

#### **Résultats et gains mesurés**

Les résultats obtenus par ces optimisations des pipelines ont  dépassé mes espérances. Bien que les résultats soient variables d'un jour à l'autre - en fonction de la charge du runner (le runner est le serveur sur lequel tournent les pipelines) puisque tous les projets internes de Takima utilisent les mêmes runners - j'ai pu calculer une moyenne des gains en performances pour l'API et le front-end de HUI.

Pour l'API, nous sommes passés d'une durée de pipeline de 20 minutes en moyenne à 12-13 minutes. Il s'agit d'une amélioration de 38%.
![[Pasted image 20250614190549.png]]
Moyenne des gains en performance sur les pipelines de l'API


Pour le front-end, nous sommes passés d'une durée de pipeline de 20 minutes en moyenne à 3 minutes environ. Il s'agit d'une amélioration de 85%. Cette amélioration est particulièrement impressionnante, et ça montre bien à quel point une simple configuration de quelques lignes peut faire toute la différence.
![[Pasted image 20250614190718.png]]
Moyenne des gains en performance sur les pipelines du front-end

Après avoir présenté ces résultats, j'ai été amené à généraliser les optimisations de pipelines sur tous les projets dans l'infrastructure de Takima. Grâce à la centralisation et ré-factorisation des Gitlab Components effectuées, généraliser les configurations des pipelines a été plutôt rapide. J'ai simplement eu à créer de nouveaux components publics pour prendre en charge les autres technologies utilisées dans les projets.

Une fois les components créés, j'ai accompagné les projets dans la migration de leur configuration `.gitlab-ci.yml` afin d'adopter les nouvelles pipelines.

#### **Rédaction de documentation**

Pour garantir la pérennité de mon travail et faciliter leur adoption pour les prochains projets, j'ai rédigé une documentation complète. Cette documentation a plusieurs objectifs :
- Détailler la structure du projet `gitlab-components`, l'utilité de mettre en place les components, comment versionner les pipelines, ainsi que le rôle respectif des components publics et privés
- Détailler individuellement la structure de chaque component public, quels inputs peuvent être spécifiés, quelles valeurs sont autorisées, et comment régler les problèmes récurrents que j'ai pu rencontrer.
- Fournir un guide de migration pour passer de sa configuration `.gitlab-ci.yml` vers l'utilisation des components.

Voici un exemple de la documentation détaillant la liste de components publics :
![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUcK2_Bs8TZIJmnnjp1j-SqxsUs7oKmZss7s4U-yPovF9cnZLPbtOcd2paXQdLDoqt9V6-n0SS0qaubJKv5tORyUJUcyEGq34I5vxhGVI70Lt2cKDONC6MQNk9AzFHNIeL80xtB1=s2048?key=2z088As1guQ-ZA8-niVywg)

Et voici un exemple de la documentation détaillant le fonctionnement du component `frontend-node` et de comment l'intégrer à son projet :
![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUdmxUYDuSL1inSwzglyuTg91X9RY1B6n_imt3ECyf4vVr0rM0EslyStBsrLjSKRWDI8pMtWdNE7nyb3CM5fStatnL_e1H2VfQD15FpODgHRMo81O35shBfqPXKYLppWP-1HbDAU9g=s2048?key=2z088As1guQ-ZA8-niVywg "Screenshot From 2025-05-09 22-11-58.png")

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

- Diagramme C4 des composants de Hui
 ![[Pasted image 20250614180736.png]]



`.gitlab-ci.yml` de **HUI-Front** avant Gitlab Components
```yaml
variables:
  RELEASE:
    value: minor
    description: 'major,minor,patch'
  TARGET_APP_NAME: front
  ALPINE_IMAGE: '${CI_DEPENDENCY_PROXY_DIRECT_GROUP_IMAGE_PREFIX}/alpine:3.21.3'
  IMAGE_NAME: '${CI_DEPENDENCY_PROXY_DIRECT_GROUP_IMAGE_PREFIX}/node:22'
  DOCKERFILE_CUSTOM_ARGS: '--build-arg NODE_LTS_VERSION=22'


stages:
  - "install dependencies \U0001F503"
  - "build \U0001F528"
  - "test \U0001F9EA"
  - sonarqube-check
  - "package \U0001F4E6"
  - release ⭐
  - "deploy \U0001F680"
 
 
install:
  interruptible: true
  stage: "install dependencies \U0001F503"
  image: $IMAGE_NAME
  cache:
    - key: '${CI_PROJECT_NAME}-node'
      paths:
        - node_modules/
  script:
    - yarn install
  artifacts:
    reports:
      dotenv:
        - vars.env
  tags:
    - compute
    - large
    
    
build:
  interruptible: true
  stage: "build \U0001F528"
  needs:
    - job: install
      artifacts: true
      optional: true
  image: $IMAGE_NAME
  cache:
    - key: '${CI_PROJECT_NAME}-node'
      paths:
        - node_modules/
  script:
    - yarn run build
  artifacts:
    expire_in: 1 hour
    paths:
      - build
  tags:
    - compute
    - large
    
    
test:
  interruptible: true
  stage: "test \U0001F9EA"
  needs:
    - job: install
      artifacts: true
      optional: true
    - job: build
      artifacts: true
  image: $IMAGE_NAME
  cache:
    - key: '${CI_PROJECT_NAME}-node'
      paths:
        - node_modules/
  script:
    - 'yarn run test:ci'
  tags:
    - compute
    - extra_large
    
    
sonarqube-check:
  interruptible: true
  stage: sonarqube-check
  image: >-
    ${CI_DEPENDENCY_PROXY_DIRECT_GROUP_IMAGE_PREFIX}/sonarsource/sonar-scanner-cli:11.2.1.1844_7.0.2
  variables:
    SIZE: large
  needs:
    - job: install
      artifacts: true
      optional: true
    - job: build
      artifacts: true
      optional: true
    - job: test
      artifacts: true
  dependencies:
    - build
    - test
  script:
    - sonar-scanner
  allow_failure: true
  tags:
    - compute
    - $SIZE
  
  
package:
  image: 'registry.takima.io/school/proxy/kaniko:1.23.2'
  cache:
    - key: '${CI_PROJECT_NAME}-node'
      paths:
        - node_modules/
  script: |
    /kaniko/executor \
          --context $CI_PROJECT_DIR \
          --dockerfile $CI_PROJECT_DIR/Dockerfile \
          --build-arg ARTIFACT_PATH="build" \
          --destination $CI_REGISTRY_IMAGE:$TAG \
          --destination $CI_REGISTRY_IMAGE:latest \
          --cache=true \
          $DOCKERFILE_CUSTOM_ARGS
  tags:
    - packaging
  interruptible: true
  stage: "package \U0001F4E6"
  needs:
    - job: install
      artifacts: true
      optional: true
    - job: build
      artifacts: true
    - job: test
      artifacts: false
    - job: sonarqube-check
      artifacts: false
      optional: true
  
  
'release:app':
  stage: release ⭐
  image: $IMAGE_NAME
  cache:
    - key: '${CI_PROJECT_NAME}-node'
      paths:
        - node_modules/
  script: >
    npm config set tag-version-prefix ''

    appver=( $( node -p
    "require('./package.json').version.replace('-SNAPSHOT','')" | tr . '\n' ) )


    case $RELEASE in 
      major) RELEASE_VERSION=$((appver[0]+1)).0.0 
             NEW_VERSION=$((appver[0]+1)).1.0-SNAPSHOT
      ;;
      minor) RELEASE_VERSION=$((appver[0])).$((appver[1])).$((appver[2])) 
             NEW_VERSION=$((appver[0])).$((appver[1]+1)).0-SNAPSHOT
      ;;
      patch) RELEASE_VERSION=$((appver[0])).$((appver[1])).$((appver[2])) 
             NEW_VERSION=$((appver[0])).$((appver[1])).$((appver[2]+1))-SNAPSHOT
      ;;
    esac


    npm version $RELEASE_VERSION --tag-version-prefix='v' --git-tag-version -m
    "[yarn-release-plugin] prepare release v%s"

    git push --tags


    npm version $NEW_VERSION --no-git-tag-version 

    git commit -am "[yarn-release-plugin] prepare for next development
    iteration"

    git push origin $CI_COMMIT_BRANCH
```