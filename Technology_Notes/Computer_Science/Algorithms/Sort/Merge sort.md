# Merge sort (tri fusion)

#computerscience #algorithms #sort 

Algorithme de tri de la famille "divide and conquer".

Plus complexe mais très efficaces, surtout sur de grandes séquences de données.

On divise le tableau en 2 éléments égaux et on recommence la même chose jusqu'à atteindre un élément par séparation. On fusionne les éléments en les triant à chaque niveau.

Comme des poupées russes, on décompose le tableau jusqu'à son élément le plus petit.

- **Pseudocode**
    - **Trier** la partie gauche du tableau (on suppose que n > 1)
    - **Trier** la partie droite du tableau (on suppose que n > 1)
    - **Fusionner** les deux moitiés

![](https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif?20151222172210)

**Big O notation : O(n log n)**

**Omega notation : Ω(n log n)**

Pire scénario : On doit diviser n éléments jusqu'à les refusionner 

Meilleur scénario : On doit quand même diviser et combiner les tableaux même si l'array est déjà trié

- **Code**
    
    ```jsx
    const mergeSort = array => {
          // divide array until there's only one element
          // the recursive stops condition
          if (array.length > 1) {
            // get the middle index of the current division
            const middleIndex = Math.floor(array.length / 2);
            // get left side of array 
            const leftSide = array.slice(0, middleIndex);
            // get right side of array
            const rightSide = array.slice(middleIndex);
    
            // call recursively for the left part of data
            mergeSort(leftSide);
            // call recursively for the right part of data
            mergeSort(rightSide);
    
            // default setup of indexes
            let leftIndex = 0; rightIndex = 0; globalIndex = 0;
    
            // loop until we reach the end of the left or right array
            // we can't compare if there is only one element
            while (leftIndex < leftSide.length && rightIndex < rightSide.length) {
    
              // actual sort comparison is here
              // if the left element is smaller, it should be first in the array
              // else the right element should be first
              // move indexes at each step
              if (leftSide[leftIndex] < rightSide[rightIndex]) {
                array[globalIndex] = leftSide[leftIndex];
                leftIndex++;
              } else {
                array[globalIndex] = rightSide[rightIndex];
                rightIndex++;
              } 
              globalIndex++;
            }
    
            // making sure that no element was left behind during process
            while (leftIndex < leftSide.length) {
              array[globalIndex] = leftSide[leftIndex];
              leftIndex++;
              globalIndex++;
            }
    
            while (rightIndex < rightSide.length) {
              array[globalIndex] = rightSide[rightIndex];
              rightIndex++;
              globalIndex++;
            }
    
          }
          return array;
        }
    
      console.log(mergeSort([2, 4, 1, 3, 8, 6]))
    ```