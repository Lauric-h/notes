# Quick sort (tri rapide)

#computerscience #algorithms #sort 

Aussi appelé tri pivot. 

Fait partie de la famille "divide and conquer". Utilise la récursion, et est complexe.

Très utilisé par les langages modernes

Fonctionnement centré autour du concept de **pivot** : on choisit un élément du tableau et on décrète que c'est le pivot. Une fois le pivot choisit, on crée un sous tableau : toutes les valeurs plus basses vont à gauche, toutes les valeurs plus hautes à droite. Ensuite on appelle de façon récursive le même algo sur le sous-tableau.

Il existe la fonction sort() en JavaScript qui permet de trier un array sans implémenter d'algorithme.

**/!\ sort() est utilisée différemment selon les navigateurs** : MergeSort sur Firexox, QuickSort sur Chrome

![](https://upload.wikimedia.org/wikipedia/commons/9/9c/Quicksort-example.gif)

- **Pseudocode**
    - **Définir** le pivot
    - **Créer un sous tableau** avec le pivot au milieu
        - **Comparer** les valeurs du tableau au pivot
            - Si valeur supérieure au pivot, **placer la valeur à droite du pivot**
            - Si valeur inférieure au pivot, **placer la valeur à gauche du pivot**
            - **Répéter**


**Big O notation : O(n²)** (mais les chances d'avoir cette durée sont infimes, on peut donc considérer que O(n log n))

**Omega notation : Ω(n log n)**

- **Code**
    
    ```jsx
    // on définit le pivot
        const pivot = (arr, start = 0, end = arr.length + 1) => {
          // swap réassigne les index 
          const swap = (list, a, b) => [list[a], list[b]] = [list[b], list[a]];
    
          // pointer est un placeholder pour le pivot
          // A chaque fois qu'un tour de boucle est fait, chaque élément est comparé au pivot
            // si l'élément est plus petit, il est swap avec le pointer.
          // On fait cela pour s'assurer que le pointer est toujours 
          // après les éléments plus petits que le pivot 
          // et avant les éléments plus grands
          let pivot = arr[start];
          let pointer = start;
    
          for (let i = start; i < arr.length; i++) {
            if (arr[i] < pivot) {
              pointer++;
              swap(arr, pointer, i)
            }
          };
          swap(arr, start, pointer);
    
          return pointer;
        }
    
        const quickSort = (arr, start = 0, end = arr.length) => {
          let pivotIndex = pivot(arr, start, end);
    
          // base case
          if (start >= end) return arr;
          // récursion
          // On trie la première partie de l'array
          quickSort(arr, start, pivotIndex);
          // on trie la deuxième partie de l'array
          quickSort(arr, pivotIndex + 1, end);
    
          return arr;
        };
    
        const unsortedArray = [20500, 33, 25000, 1200, 3]
    
        console.log(quickSort(unsortedArray));
    ```