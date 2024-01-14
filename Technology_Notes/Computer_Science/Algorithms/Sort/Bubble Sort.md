# Bubble Sort (tri à bulle)

#computerscience #sort #algorithms 

Le plus simple des algorithmes de tri. Mais aussi le plus lent, donc peu utilisé.

Bouge les valeurs basses vers la gauche et les valeurs hautes vers la droite.

![](https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif)

- **Pseudocode**
    - **On passe sur chaque élément** du tableau et on le compare à son voisin de droite
    - **Si le voisin de droite est plus petit**, on **permute** les éléments
    - **Faire autant de passes** tant que le tableau n'est pas trié

**Big O notation : O(n²)**

**Oméga notation : Ω(n)**

Pire scénario : l'array est complétement mélangé et on doit bouger tous les éléments

Meilleur scénario : l'array est déjà trié et ne fait aucun swap au premier tour

- **Code**
    
    ```jsx
    const unsortedArray = [2, 1, 47, 32, 115, 98];
    
    const bubbleSort = array => {
    	const arrayLength = array.length
    	// isSwapped permet d'éviter de répéter l'algo 
    	// même si les chiffres sont déjà triés
    	let isSwapped;
    
    	do {
    		isSwapped = false;
    		
    		// on itère dans l'array
    		for (let i = 0; i < arrayLength; i++) {
    			if (array[i] > array[i + 1] {
    				// on met la valeur dans une variable temporaire
    				const tempLeftValue = array[i];
    
    				// on permute les deux chiffres
    				array[i] = array[i + 1];
    				array[i + 1] = tempLeftValue;
    				
    				isSwapped = true;
    			}
    		}
    	} while (isSwapped);
    	return array;
    }
    
    console.log(bubbleSort(unsortedArray);
    ```