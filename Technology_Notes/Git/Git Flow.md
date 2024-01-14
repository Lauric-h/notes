# Git Flow

Created: January 13, 2021 2:32 PM
Tags: git, tools

[https://www.atlassian.com/fr/git/tutorials/comparing-workflows/gitflow-workflow](https://www.atlassian.com/fr/git/tutorials/comparing-workflows/gitflow-workflow)

## Définition

Framework pour la gestion de projets. Définit un cadre précis de création de branches.

Il dicte quel type de branches doit être configuré et comment les merger.

Également outil en CLI.

## Fonctionnement

### ⇒ 2 branches pour sauvegarder l'historique du projet :

- branche principale (master) : stock l'historique officiel des versions
- branche de développement (develop) : branche d'intégration pour les fonctionnalités

![https://wac-cdn.atlassian.com/dam/jcr:2bef0bef-22bc-4485-94b9-a9422f70f11c/02%20(2).svg?cdnVersion=1402](https://wac-cdn.atlassian.com/dam/jcr:2bef0bef-22bc-4485-94b9-a9422f70f11c/02%20(2).svg?cdnVersion=1402)

![Git%20Flow%200070c/02_(2).svg](Git%20Flow%200070c/02_(2).svg)

![Git%20Flow%200070c/02_(2)%201.svg](Git%20Flow%200070c/02_(2)%201.svg)

### ⇒ branches de fonctionnalités

- Une branche pour chaque fonctionnalité
- On les utilise à partir de la branche de développement et non de master
- Lorsqu'une fonctionnalité est terminée elle est à nouveau mergée dans develop
- Les fonctionnalités ne communiquent jamais avec la branche master

![https://wac-cdn.atlassian.com/dam/jcr:b5259cce-6245-49f2-b89b-9871f9ee3fa4/03%20(2).svg?cdnVersion=1402](https://wac-cdn.atlassian.com/dam/jcr:b5259cce-6245-49f2-b89b-9871f9ee3fa4/03%20(2).svg?cdnVersion=1402)

### ⇒ branches de livraison

Une fois que la branche develop possède assez de fonctionnalités, on fork une branche de version (release) à partir de develop.

*La création de cette branche marque le début du cycle de livraison suivant, aucune fonctionnalité supplémentaire ne pourra être ajoutée*

→ la branche sera dédiée à la correction de bugs, générations de documentation et autres tâches.

Une fois qu'elle est prête, on peut merge la branche release avec la branche master.

![https://wac-cdn.atlassian.com/dam/jcr:a9cea7b7-23c3-41a7-a4e0-affa053d9ea7/04%20(1).svg?cdnVersion=1402](https://wac-cdn.atlassian.com/dam/jcr:a9cea7b7-23c3-41a7-a4e0-affa053d9ea7/04%20(1).svg?cdnVersion=1402)

### ⇒ branches hotfix

Branches de maintenant servent à appliquer rapidement des patchs aux versions de production. Elles sont basées sur la branche principale.