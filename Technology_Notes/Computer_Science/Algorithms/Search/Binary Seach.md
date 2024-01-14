# Binary Seach

#computerscience #algorithms #search

Pour trouver un élément dans un array.

L'array doit être trié en ordre croissant.

Diviser en 2 le problème à chaque fois.

![](https://d18l82el6cdm1i.cloudfront.net/uploads/bePceUMnSG-binary_search_gif.gif)

- **Pseudocode**
    - Répéter jusqu'à ce que l'array soit de taille 0
        - Calculer le point du milieu de l'array
        - Si la cible est au milieu : stop
        - **Sinon, si la cible est plus petite que le milieu**, répéter, en changeant le point de fin directement à gauche du milieu. Chercher dans la moitié gauche.
        - **Sinon, si la cible est plus grande que le milieu**, répéter en changeant le point de début directement à droite du milieu. Chercher dans la moitié droite.

Il faut connaître :

- Élément cible
- Point de début
- Point de fin
- Milieu de l'array

Quand le point de début et de milieu se croisent : l'élément n'existe pas dans l'array (start : 8, end : 7)

**Big O notation : log n**

**Ω notation : 1**

Pire scénario / O(log n) : on doit diviser en 2 de façon répétée

- Soit car l'élément va être trouvé en dernier
- Soit car l'élément n'existe pas dans l'array

Meilleur scénario / Ω(1) :

- L'élément est au milieu de l'array
- **Approche récursive**
    
    ```jsx
    let recursiveFunction = function(arr, x, start, end) {
    	// base case
    	if (start > end) {
    		return false;
    	}
    	// find the middle index
    	let mid = Math.floor((start + end) / 2);
    
    	// compare mid with target
    	if (arr[mid] === x) {
    		return true;
    	}
    	// if target is lower than mid
    	if (x < arr[mid]) {
    		// call the same function, setting the end to be
    		// at the left of the mid
    		return recursiveFunction(arr, x, start, mid-1);
    	} else {
    		// if target is greater than mid
    		// call same function
    		// set start to be at righ of mid
    		return recursiveFunction(arr, x, mid+1, end);
    	}
    }
    // output code
    // not using let to avoid error
    arr = [1, 7, 12, 15, 29];
    x = 15;
    
    if (recursiveFunction(arr, x, 0, arr.length - 1)) {
    	console.log("Element found");
    } else {
    	console.log("Element not found");
    }
    
    	
    	
    ```
    
- **Approche itérative**
    
    ```jsx
    // declare here to avoid errors
    let start;
    let end;
    
    let iterativeFunction = function(arr, x, start, end) {
    	start = 0;
    	end = arr.length - 1;
    
    	//iterate while start and end don't cross
    	while (start <= end) {
    		// find mid
    		let mid = Math.floor((start + end) / 2);
    
    		// if target is mid
    		if (arr[mid] === x) return true;
    		
    		// else, look left or right, regarding
    		else if (arr[mid] < x) {
    			start = mid + 1;
    		} else {
    			end = mid - 1;
    		}
    	}
    	return false;
    }
    
    // output code
    let arr = [1, 7, 12, 15, 29];
    let x = 15;
    
    if (iterativeFunction(arr, x, 0, arr.length - 1)) {
    	console.log("Element found");
    } else {
    	console.log("Element not found");
    }
    	
    			
    
    ```