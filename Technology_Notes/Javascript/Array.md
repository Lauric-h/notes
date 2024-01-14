# Array

#javascript #computerscience 

# Définition

Un array est une collection d'éléments auxquels ont peut accéder par un indice. Chaque array est stocké dans la mémoire de la machine. **Chaque élément est lié à un index qui fait le lien entre l'adresse mémoire et la valeur de l'élément.**

Pour obtenir la valeur d'un élément, on utilise son index pour y accéder. **L'index va chercher la valeur via l'adresse mémoire.**

![Array%20661b8/jVmA2wP.jpg](Array%20661b8/jVmA2wP.jpg)

**Un array est une séquence finie d'éléments** = on alloue une certaine taille mémoire à un array et on ne peut plus changer.

**Un array ne permet de gérer qu'un seul type de données, on ne peut pas mélanger les types.** (En JavaScript on peut mélanger les types de données car les arrays sont en réalité des objets).

```jsx
let arr = [1, 2, 3, 12, 257];
```

- **Avantages**
    - On peut maintenir une grande quantité de données au même endroit
    - Chacun des éléments peut être accédé en temps constant (O(1)) via son index
    - Taille mémoire fixe : évite les problèmes de mémoire (overflow)
- **Inconvénients**
    - Taille fixe : impossible de le faire grossir sans créer un nouvel array
    - Un array ne peut contenir qu'un seul type de données
    
    # Méthodes
    
    ## .push & .pop : Ajouter et supprimer des éléments en fin de tableau
    
    .push() permet **d'ajouter des éléments à la fin de l'array.**
    
    .pop() **supprime le dernier élément** du tableau.
    
    .push() renvoie également la nouvelle taille du tableau.
    
    ```jsx
    const animals = ['pig', 'cows'];
    const count = animals.push('horse');
    console.log(count) // 3 = nouvelle taille du tableau
    console.log(animals) = ['pig', 'cows', 'horse'];
    
    let popped = animals.pop();
    console.log(animals) // ['pig', 'cows'];
    console.log(popped) // 'horse';
    ```
    
    ## .shift() & .unshift() : Ajouter et supprimer des éléments en début de tableau
    
    .unshift() permet **d'ajouter des éléments au début de l'array** et retourne la nouvelle taille du tableau.
    
    .shift() **enlève le premier élément** de l'array et retourne la valeur de l'élément retiré.
    
    ```jsx
    const animals = ['pig', 'cows'];
    const count = animals.unshift('horse');
    console.log(count) // 3 = nouvelle taille du tableau
    console.log(animals) = ['horse', 'pig', 'cows'];
    
    let shifted = animals.shift();
    console.log(animals) // ['pig', 'cows'];
    console.log(shifted) // 'horse';
    ```
    
    ## .splice() : Ajouter ou supprimer des éléments choisis dans un tableau
    
    .splice() permet **d'ajouter ou supprimer des éléments n'importe où dans l'array**.
    
    La méthode prend au moins 2 arguments : la position à partir de laquelle les éléments devront être ajoutés et combien d'éléments devront être enlevés.
    
    Après ces deux arguments, on peut ajouter autant d'arguments qu'on veut ajouter de valeurs.
    
    Si on veut juste supprimer une valeur sans insérer de nouveaux éléments il suffit de n'indiquer aucun élément.
    
    ```jsx
    array.splice(début, nbASupprimer, 'él1', 'él2')
    
    const months = ['Jan', 'Mar', 'Apr'];
    months.splice(1, 0, 'Feb'); // insère 'Feb' en position 1 et enlève 0 élément
    console.log(months) // ['Jan', 'Feb', 'Mar', 'Apr'];
    
    months.splice(2);
    console.log(months) // ['Jan', 'Feb'];
    ```
    
    ## .sort() : Classer les éléments d'un tableau
    
    .sort() permet de **trier les éléments d'un array** dans l'ordre croissant ou alphabétique.
    
    Attention à la casse : les majuscules seront classées avant les minuscules.
    
    Attention pour trier les nombres : sort() trie caractère par caractère ⇒ 25 sera classé après 100 car 2 est plus grand que 1.
    
    sort() convertit les éléments en chaînes de caractères.
    
    Le tri utilisé dépend de l'interpréteur JavaScript (cf algorithmes de tri), la complexité (Big O) ne peut pas être garantie car différente selon les navigateurs.
    
    ```jsx
    arr.sort()
    arr.sort(fonctionComparaison) // pour trier les nombres correctement
    
    const months = ['March', 'Jan', 'Feb', 'Dec'];
    months.sort();
    console.log(months);
    // expected output: Array ["Dec", "Feb", "Jan", "March"]
    
    const array1 = [1, 30, 4, 21, 100000];
    array1.sort();
    console.log(array1);
    // expected output: Array [1, 100000, 21, 30, 4]
    
    // fonctions de comparaison 
    function compare(a, b) {
      if (a est inférieur à b selon les critères de tri)
         return -1;
      if (a est supérieur à b selon les critères de tri)
         return 1;
      // a doit être égal à b
      return 0;
    }
    
    // Pour comparer des nombres plutôt que des chaînes, 
    // la fonction de comparaison peut simplement soustraire b à a
    function compareNombres(a, b) {
      return a - b;
    }
    
    // exemple avec des chiffres
    var nombres = [4, 2, 5, 1, 3];
    nombres.sort(function(a, b) {
      return a - b;
    });
    console.log(nombres);
    // [1, 2, 3, 4, 5]
    
    // syntaxe concise avec ES6
    let nombres = [4, 2, 5, 1, 3];
    nombres.sort((a, b) => a - b);
    console.log(nombres);
    ```
    
    ## .reverse() : inverser les éléments d'un tableau
    
    .reverse() permet d'inverser les éléments d'un tableau : combinée avec .sort(), on peut ainsi classer un tableau dans l'ordre inverse de l'ordre alphabétique ou décroissant.
    
    ```jsx
    let nombres = [4, 2, 5, 1, 3];
    nombres.sort((a, b) => a - b);
    console.log(nombres); // 1, 2, 3, 4, 5
    nombres.reverse()
    console.log(nombres); // 5, 4, 3, 2, 1
    ```
    
    ## .join()
    
    .join() permet de **retourner les différentes valeurs d'un tableau sous forme de chaînes de caractères** et permet de choisir le type de séparateur voulu entre les différentes valeurs (virgule, espace, trait etc.)
    
    La méthode ne modifie pas le tableau, elle renvoie une nouvelle chaîne de caractères avec le séparateur.
    
    ```jsx
    arr.join()
    arr.join(séparateur)
    
    const elements = ['Fire', 'Air', 'Water'];
    
    console.log(elements.join());
    // expected output: "Fire,Air,Water"
    
    console.log(elements.join(''));
    // expected output: "FireAirWater"
    
    console.log(elements.join('-'));
    // expected output: "Fire-Air-Water"
    ```
    
    ## .slice() : Créer un nouveau tableau
    
    .slice() permet de **créer un nouveau tableau en extrayant des éléments d'un tableau de base.**
    
    La méthode a besoin de 2 arguments : une position de départ et une position de fin.
    
    Si on ne précise qu'une position de départ, la méthode coupe jusqu'à la fin du tableau.
    
    Elle n'impacte pas le tableau de base, mais créé un nouveau tableau avec les valeurs extraites. (shallow copy)
    
    ```jsx
    arr.slice()
    arr.slice(début)
    arr.slice(début, fin)
    
    var fruits = ["Banane", "Orange", "Citron", "Pomme", "Mangue"];
    var agrumes = fruits.slice(1, 3);
    
    // fruits vaut --> ["Banane", "Orange", "Citron", "Pomme", "Mangue"]
    // agrumes vaut --> ["Orange", "Citron"]
    ```
    
    ## .concat() : créer un tableau à partir de plusieurs tableaux
    
    .concat() permet de fusionner plusieurs tableaux pour en créer un nouveau.
    
    La méthode prend en argument les tableaux que l'on souhaite fusionner.
    
    Les tableaux de base ne sont pas modifiés, un nouveau tableau est créé.
    
    On choisit le premier tableau arbitrairement.
    
    ```jsx
    let nouveau_tableau = ancien_tableau.concat(valeur1[, valeur2[, ...[, valeurN]]])
    
    let num1 = [1, 2, 3];
    let num2 = [4, 5, 6];
    let num3 = [7, 8, 9];
    
    let nums = num1.concat(num2, num3);
    
    console.log(nums);
    // [1, 2, 3, 4, 5, 6, 7, 8, 9]
    ```
    
    ## .every() : tester les éléments
    
    La méthode .every() permet de **tester si tous les éléments d'un tableau remplissent une condition donnée par une fonction en argument**. La fonction renvoie un booléen.
    
    La fonction sur laquelle on souhaite tester chaque élément du tableau, elle prend 3 arguments :
    
    - currentValue : la valeur de l'élément à traiter
    - index : l'indice de l'élément à traiter
    - array: le tableau sur lequel on a appelé la méthode every()
    
    La méthode every exécute la fonction callback fournie sur chacun des éléments contenus dans le tableau jusqu'à ce qu'un élément pour lequel la fonction callback renvoie une valeur fausse (falsy value) soit trouvé. Si un tel élément est trouvé, la méthode every renvoie directement false. Sinon, si la fonction callback a renvoyé une valeur vraie pour tous les éléments, la méthode every renverra true.
    
    every ne modifie pas le tableau sur lequel elle a été appelée.
    
    ```jsx
    arr.every(callback)
    
    function estAssezGrand(element, index, array) {
      return element >= 10;
    }
    [12, 5, 8, 130, 44].every(estAssezGrand);   // false
    [12, 54, 18, 130, 44].every(estAssezGrand); // true
    ```
    
    ## .some()
    
    La méthode some() **teste si au moins un élément du tableau passe le test implémenté par la fonction fournie**. Elle renvoie un booléen indiquant le résultat du test.
    
    Elle fonctionne comme la méthode every().
    
    La méthode some() exécute la fonction callback une seule fois pour chaque élément présent dans le tableau jusqu'à ce qu'elle en trouve un pour lequel callback renvoie une valeur équivalente à true dans un contexte booléen. Si un tel élément est trouvé, some() renvoie immédiatement true. Dans le cas contraire, some renvoie false.
    
    ```jsx
    arr.some(callback)
    
    function estAssezGrand(element, indice, array) {
      return (element >= 10);
    }
    var resultat = [2, 5, 8, 1, 4].some(estAssezGrand);
    // resultat vaut false
    passed = [12, 5, 8, 1, 4].some(estAssezGrand);
    // passed vaut true
    ```
    
    ## .find() & .findIndex() : la premier élément trouvé
    
    .find() **renvoie la valeur du premier élément trouvé qui respecte la condition** donnée par la fonction test en argument.
    
    .findIndex() **renvoie l'index du premier élément trouvé qui respecte la condition** donnée par la fonction test en argument.
    
    La méthode find exécute la fonction callback une fois pour chaque élément présent dans le tableau jusqu'à ce qu'elle retourne une valeur vraie (qui peut être convertie en true). Si un élément est trouvé, find retourne immédiatement la valeur de l'élément. Autrement, find retourne undefined.
    
    La méthode `findIndex` exécute la fonction `callback` une fois pour chaque élément présent dans le tableau (le tableau est parcouru entre les indices `0` et `length-1` compris) jusqu'à ce que `callback` renvoie une valeur vraie.
    
    S'il existe un tel élément, `findIndex` renverra immédiatement l'indice de l'élément concerné. Sinon, `findIndex` renverra -1.
    
    ```jsx
    const array1 = [5, 12, 8, 130, 44];
    
    const found = array1.find(element => element > 10);
    
    console.log(found);
    // expected output: 12
    
    const foundIndex = array1.findIndex(element => element > 10);
    console.log(foundIndex)
    // expected output : 1
    ```
    
    ## .filter()
    
    La méthode filter() crée et retourne un nouveau tableau contenant tous les éléments du tableau d'origine qui remplissent une condition déterminée par la fonction callback.
    
    ```jsx
    const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];
    
    const result = words.filter(word => word.length > 6);
    
    console.log(result);
    // expected output: Array ["exuberant", "destruction", "present"]
    ```
    
    ## .map()
    
    **La méthode map() crée un nouveau tableau avec les résultats de l'appel d'une fonction fournie sur chaque élément du tableau appelant.**
    
    Lorsqu'on utilise map, la fonction callback fournie en argument est exécutée une fois pour chacun des éléments du tableau, dans l'ordre du tableau. Chaque résultat de l'opération sur un élément sera un élément du nouveau tableau.
    
    **Attention !** map() construit un nouveau tableau. Si on utilise cette méthode sans utiliser le résultat, mieux vaudra utiliser forEach ou for...of. Pour mieux décider si map()est adéquat, regardez si vous utilisez la valeur de retour et/ou si vous renvoyez une valeur avec la fonction callback : si ce n'est pas le cas, il ne faut pas utiliser map().
    
    .map() ne modifie pas le tableau sur lequel elle est appelée (bien que la fonction callback, si elle est appelée, puisse modifier le tableau).
    
    ```jsx
    var nouveauTableau = arr.map(callback)
    
    // Fonctionnement de map avec une fonction à un argument
    var nombres = [1, 4, 9];
    var doubles = nombres.map(function(num) {
      return num * 2;
    });
    // doubles vaut désormais [2, 8, 18].
    // nombres vaut toujours [1, 4, 9]
    ```
    
    ## Array.from()
    
    La méthode Array.from() permet de créer une nouvelle instance d'Array (une copie superficielle) à partir d'un objet itérable ou semblable à un tableau
    
    `Array.from()` permet de créer des instances d'`Array` à partir :
    
    - d'objets semblables à des tableaux (qui disposent d'une propriété `length` et d'éléments indexés) ou
    - [d'objets itérables](https://developer.mozilla.org/fr/docs/Web/JavaScript/Guide/iterable) (des objets dont on peut avoir les éléments comme `[Map](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Map)` et `[Set](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Set)`).
    
    `Array.from()` possède un paramètre optionnel `fonctionMap`, qui permet d'exécuter une fonction `[map](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/map)` sur chacun des éléments du tableau (ou de l'instance de la classe fille) qui est créé. Autrement dit `Array.from(obj, mapFn, thisArg)` correspond exactement à `Array.from(obj).map(mapFn, thisArg)`, sauf qu'il n'y a pas de tableau intermédiaire de créé. Cet aspect est
    notamment important pour certaines classes filles, comme les [tableaux typés](https://developer.mozilla.org/fr/docs/JavaScript/Tableaux_typ%C3%A9s) (en effet, un tableau intermédiaire aurait eu ses valeurs tronquées pour qu'elles soient du type approprié).
    
    ```jsx
    console.log(Array.from('foo'));
    // expected output: Array ["f", "o", "o"]
    
    console.log(Array.from([1, 2, 3], x => x + x));
    // expected output: Array [2, 4, 6]
    ```
    
    ## .toString()
    
    La méthode toString() renvoie une chaine de caractères représentant le tableau spécifié et ses éléments.
    
    Pour les objets Array, la méthode toString() concatène les éléments du tableau et renvoie une chaîne contenant chacun des éléments, séparés par des virgules.
    
    ```jsx
    const array1 = [1, 2, 'a', '1a'];
    
    console.log(array1.toString());
    // expected output: "1,2,a,1a"
    ```
    
    ## .apply()
    
    La méthode apply() appelle une fonction en lui passant une valeur this et des arguments sous forme d'un tableau (ou d'un objet semblable à un tableau).
    
    Il est possible d'utiliser un objet this différent lors de l'appel à une fonction existante. this fait référence à l'objet courant, l'objet appelant. Avec apply, on peut écrire une méthode une seule fois et en hériter dans un autre objet, sans avoir à la réécrire dans le nouvel objet.
    
    On peut aussi passer arguments en tant que paramètre argsArray. arguments étant une variable locale à la fonction. Celle-ci peut également être utilisée pour tous les arguments non spécifiés de l'objet appelé. Ainsi, il n'est pas nécessaire de connaître les arguments de l'objet appelé lors d'un appel à la méthode apply. arguments peut être utilisé pour passer tous les arguments à l'objet appelé. L'objet appelé gèrera alors la manipulation des arguments.
    
    ```jsx
    //syntaxe
    function.apply(thisArgs, [argsArray])
    
    const numbers = [5, 6, 2, 3, 7];
    
    const max = Math.max.apply(null, numbers);
    
    console.log(max);
    // expected output: 7
    
    const min = Math.min.apply(null, numbers);
    
    console.log(min);
    // expected output: 2
    ```
    
    ## .reduce()
    
    La méthode reduce() applique une fonction qui est un « accumulateur » et qui traite chaque valeur d'une liste (de la gauche vers la droite) afin de la réduire à une seule valeur.
    
    `reduce()` exécute la fonction `callback` une fois pour chaque élément présent dans le tableau et ignore les éléments vides du tableau. La fonction `callback` utilise quatre arguments :
    
    1. L'accumulateur (la valeur retournée par le précédent appel de la fonction `callback`), ou la valeur initiale s'il sagit du premier appel ;
    2. la valeur de l'élément courant ;
    3. l'index de l'élément courant ;
    4. le tableau parcouru par la méthode.
    
    La première fois que la fonction `callback` est appelée, `valeurInitiale` et `valeurCourante` peuvent correspondre à un ou deux éléments. Si `valeurInitiale` est fournie dans l'appel de `reduce()`, alors `accumulateur` sera égale à `valeurInitiale` et `valeurCourante` sera égale à la première valeur de la liste. Si `valeurInitiale` n'est pas fournie, alors `accumulateur` sera égale à la première valeur de la liste, et `valeurCourante` sera alors égale à la seconde.
    
    Autrement dit, si `valeurInitiale` n'est pas fournie, `reduce` exécutera la fonction de rappel à partir de l'indice 1 et la première valeur du tableau (d'indice 0) sera utilisée pour `valeurInitiale`.
    
    [Copy of Untitled](https://www.notion.so/323579819add405d9c36abc9b244f6ed)
    
    ```jsx
    // syntaxe
    arr.reduce(callback)
    arr.reduce(callback, valeurInitiale)
    
    const array1 = [1, 2, 3, 4];
    const reducer = (accumulator, currentValue) => accumulator + currentValue;
    
    // 1 + 2 + 3 + 4
    console.log(array1.reduce(reducer));
    // expected output: 10
    
    // 5 + 1 + 2 + 3 + 4
    console.log(array1.reduce(reducer, 5));
    // expected output: 15
    ```