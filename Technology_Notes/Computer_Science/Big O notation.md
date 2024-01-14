# Big O notation

#computerscience #learnings 

## Définition

Aussi appelée complexité algorithmique. **Manière standard de mesurer la performance d'un algorithme.**

Manière mathématique de juger l'efficacité du code. Permet de mesurer le taux de croissance de l'algorithme en fonction des données d'entrées.

**Décrit le pire cas possible de la performance du code.**

O = ordre de grandeur (order of)

On ne mesure pas directement la vitesse d'un algorithme en secondes, **on mesure le taux de croissance via le nombre d'opérations qu'il faut pour terminer.**

On regarde la tendance du nombre d'opérations nécessaires selon les paramètres d'entrées.

## Tendances

### Tendance linéaire O(n)

Quand l'ordre de grandeur est directement lié au nombre d'entrées : tendance linéaire O(n).

### Complexité constante O(1)

Si l'ordre de grandeur est fixe quel que soit le nombre d'entrées : tendance constante O(3). Le même nombre d'opérations est nécessaire dans tous les cas.

### Complexité logarithmique O(log (n))

La complexité logarithmique tend à diviser les performances de l'algorithme avec le temps.

Exemple : binary search (recherche dichotomique).

### Complexité linéarithmique O(n log (n))

Même approche que la complexité logarithmique : se divise à chaque fois, mais elle le fait sur chaque élément de l'input n.

Exemple : merge sort (tri fusion)

### Complexité quadratique O(n²)

Evolue au carré de l'input en entrée. Exemple de deux boucles imbriquées.

Exemple : quick sort, bubble sort, insertion sort

## Intérêt

Permet d'évaluer les limites des solutions implantées. A quel point la solution scale ? Peu importe si les volumes sont importants.

Permet d'optimiser son code et de repérer rapidement ce qui ne va pas dans un système lent.
