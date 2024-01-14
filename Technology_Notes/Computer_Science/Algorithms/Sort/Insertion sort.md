# Insertion sort (tri par insertion)

#algorithms #computerscience #sort 

Assez lent et peu efficaces sur beaucoup de données.

Efficace sur peu de données = un des meilleurs.

On passe sur chaque élément à trier et on l'insère directement à la place où il devrait être. Pour faire cette insertion, on va simplement comparer l'élément courant avec chaque élément déjà trié sur la gauche.

![](https://upload.wikimedia.org/wikipedia/commons/9/9c/Insertion-sort-example.gif)

- **Pseudocode**
    - **On définit** le premier élément comme trié
    - **On répète**, jusqu'à ce que tous les éléments soient triés
        - **On regarde** le prochain élément non trié. **On l'insert** dans la partie triée en **bougeant** le nombre requis d'éléments.

Permet de bouger plusieurs éléments à la fois.

**Big O notation : O(n²)**

**Omega notation : Ω(n)**

Pire scénario : l'array est en ordre inversé, on doit donc bouger chaque élément à chaque fois 

Meilleur scénario : l'array est déjà trié, on doit juste regarder chaque élément une fois.

Quand on joue aux cartes, on trie sa main en en prenant chaque carte une à une et en les insérant sur la gauche = insertion sort.

- **Code**
    
    ```jsx
    const insertionSort = (array) => {
    	const arrayLength = array.length;
    	
    	// i débute à 1, on compare i au premier élément (i - 1);
    	for (let i = 1; i < arrayLength; i++) {
    		let j = i - 1;
    		let temp = array[i];
    
    		// on compare de droite à gauche
    		while (j >= 0 && array[j] > temp) {
    			array[j + 1] = array[j];
    			j--;
    		}
    		array[j + 1] = temp;
    	}
    	return array;
    }
    ```