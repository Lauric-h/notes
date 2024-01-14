# Structures de données non linéaires

#algorithms #datastructures

## Différences avec les structures linéaires

Dans les structures de données linéaires, la donnée est organisée de façon séquentielle : chaque élément du tableau vient l'un après l'autre. Facile à mettre en place et on peut consulter tous les éléments en une boucle.

Dans les structures non linéaires, la donnée n'est pas organisée de façon séquentielle : il va y avoir des liens hiérarchiques ou simplement des liens spéciaux qui relient et composent la structure. Il n'est pas possible de parcourir tous les éléments en une boucle.

## Les types de structures non linéaires

### Tree (arbres)

Ensemble de nœuds liés de façon hiérarchiques. Le noeud racine est au sommet, et est lié à ses nœuds enfants, qui peuvent eux-mêmes avoir d'autres nœuds enfants etc.

Chaque noeud ne peut avoir qu'un seul parent.

Taille = nombre de nœuds.

Hauteur = nombre de niveaux de profondeur.

Les arbres sont utilisés partout : organigramme hiérarchique, tournoi, arborescence de fichiers etc.

Il existe plusieurs types d'arbres :

- **General Tree :** pas de contrainte sur le type de hiérarchie, chaque noeud peut avoir un nombre infini d'enfants
- **Binary Tree (arbre binaire) :** chaque noeud peut avoir 2 enfants, l'enfant de droite et l'enfant de gauche. C'est le plus populaire des arbres.
- **Binary Search Tree :** type d'arbre binaire où l'enfant de gauche doit être inférieur ou égal à son parent et l'enfant de droite doit être supérieur à son parent.

```jsx
class Node {
    constructor (value = null) {
        this.value = value
        this.left = null
        this.right = null
    }
}

const Russia = new Node(2018)
const Germany = new Node(2006)
const France = new Node(1998)
const Mexico = new Node(1986)

Russia.left = Germany
Russia.right = France
France.left = Mexico

//    '2018'   
//     /   \   
//  '2006' '1998'
//          /
//       '1986'
	
```

**Avantages des arbres**

- Utilisés pour la hiérarchie
- Efficace pour la recherche et l'insertion
- Flexibles, les sous-arbres peuvent être bougés sans efforts
- Reflètent la structure de données

### Graphs (graphes)

Un graphe est un **ensemble de nœuds ou (sommets) finis reliés entre eux par des arêtes.** Chaque noeud porte une valeur, chaque arête fait le lien entre les nœuds. Les liens n'ont pas d'origine hiérarchique, juste relationnelle.

On peut comparer un graphe à une carte de stations de métro : les arrêts sont les nœuds qui portent une valeur (les noms de station). Elles sont reliées entre elles par les arêtes (les lignes). Il n'y a pas de relation hiérarchique, elles sont juste reliées entre elles.

Les graphes sont ce qui est le plus utilisé pour représenter des systèmes réels en informatique : réseaux informatiques, cartographie (Google Maps).

Pour représenter un graphe, on utilise une **matrice d'adjacence**. Si un chemin existe entre deux sommets on le représente avec un boolean true, sinon false.


```jsx
class Graph {
    constructor(vertices) {
        this.vertices = vertices
        this.adjacencyMatrix = []

        for (var i = 0; i < this.vertices; i++) { 
            this.adjacencyMatrix[i] = new Array(this.vertices).fill(0) 
        }
    }

    addEdge(i, j) {
        this.adjacencyMatrix[i][j] = 1
        this.adjacencyMatrix[j][i] = 1
    }

    display() {
        for(const row of this.adjacencyMatrix) {
            let displayRow = ''
            for(const value of row) {
                displayRow += value + ' '
            }
            console.log(displayRow)
        }
    }
}

myGraph = new Graph(4)

myGraph.addEdge(0, 2)
myGraph.addEdge(1, 3)
myGraph.addEdge(2, 3)

myGraph.display()
// 0 0 1 0
// 0 0 0 1
// 1 0 0 1
// 0 1 1 0
```