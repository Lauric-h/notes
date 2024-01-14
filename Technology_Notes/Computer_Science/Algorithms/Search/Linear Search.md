# Linear Search

#algorithms #computerscience #search

Un array pourrait être comparé à un ensemble de casiers fermés, les uns à côté des autres.

Pour vérifier si un chiffre donné se trouve dans l'array, il faut ouvrir un par un les casiers et comparer notre chiffre avec celui qui se trouve dans le casier.

![](https://slaystudy.com/wp-content/uploads/2020/05/linearsearchitr.gif)

**Si le chiffre se trouve dans le casier**, on s'arrête et on retourne l'index du casier. 

**Si le chiffre ne se trouve dans aucun casier**, on retourne que l'élément ne s'y trouve pas.

- **Pseudocode :**
    - Répéter, en commençant au premier élément,
        - Si le 1er élément est ce qu'on cherche, arrêter
        - Sinon, passer à l'élément suivant

Pire scénario : on doit regarder tous les éléments de l'array un par un 

- Si l'élément cherché est en dernier
- Si l'élément cherché n'est pas dans l'array

Meilleur scénario : l'élément cherché est le premier dans l'array.

**Big O notation : O(n)**

**Omega notaion : Ω(1)**

Les données n'ont pas besoin d'être triées pour effectuer une linear search. 

Linear Search n'est pas très utilisée car pas très rapide. Si on sait que certaines valeurs vont être utilisées fréquemment on peut les placer en début d'array.

- **Code**
    
    ```jsx
    function findIndexValue(values, target) {
    	for(let i = 0; i < values.length; ++i) {
    		if(values[i] == target) { return i; }
    	}
    	return "not found";
    }
    			
    ```