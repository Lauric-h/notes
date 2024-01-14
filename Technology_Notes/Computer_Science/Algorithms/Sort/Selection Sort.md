# Selection Sort (tri par sélection)

#algorithms #computerscience #sort 

Lire chaque chiffre de la liste, retenir le plus petit et le placer devant.

Simple algorithme de tri dans lequel la liste est divisée en deux : la partie triée à gauche et la partie non triée à droite. Initialement, la partie triée est vide et la partie non triée est la liste entière.

*Pas recommandé quand il y a beaucoup de données à trier.*


- **Pseudocode**
    - **Déclarer** min à 0
    - **Chercher** la partie non triée des données pour trouver la plus petite valeur
    - **Permuter** avec la ****valeur située à min
    - **Incrémenter** min pour être le prochain élément
    - **Répéter** jusqu'à ce que la liste soit triée

**Big O notation : O(n²)**

**Omega notation : Ω(n²)**

Pire scénario : regarder tous les éléments et les permuter un par un

Meilleur scénario : pareil, car on doit vérifier tous les éléments un par un pour être sûrs que c'est trié

- **Code**
    
    ```jsx
    const unsortedArray = ['Joe', 'Michel', 'Zoé', 'Alix', 'Cedric'];
    
    const selectionSort = (array) ⇒ {
    	const arrayLength = array.length;
    	
    	// on compare la première valeur au reste de l'array
    	for (let i = 0; i < arrayLength; i++) {
    		// on définit la première valeur comme plus petite valeur
    		let min = i;
    		for (let j = i + 1; j < arrayLength; j++) {
    			// si on trouve une valeur plus petite que la valeur min
    			if (array[j] < array[min]) {
    				// On remplace min par la nouvelle valeur
    				min = j;
    			}
    		}
    		// si min est différent de la première valeur
    		if (min ! = i) {
    			// on permute les deux, la plus petite devient la première valeur
    			let temp = array[i];
    			array[i] = array[min]
    			array[min] = temp;
    	}
    	return array;
    }
    ```