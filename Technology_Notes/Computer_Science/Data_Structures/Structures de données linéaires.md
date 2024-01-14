# Structures de données linéaires

#algorithms #datastructures
## Définition

Structures de données = différentes façons d'organiser la donnée dans du code. Chaque structure va organiser la données de façon particulière.

On veut pouvoir accéder facilement et rapidement aux données : la connaissance des structures de données et leurs utilisations est un avantage.

Le structures de données sont comme des outils à notre disposition pour résoudre des problèmes. Il faut trouver le plus adapter.

## Les structures linéaires

### 1. Array (tableau)

Un array est une collection d'éléments auxquels ont peut accéder par un indice. Chaque array est stocké dans la mémoire de la machine. **Chaque élément est lié à un index qui fait le lien entre l'adresse mémoire et la valeur de l'élément.**

Pour obtenir la valeur d'un élément, on utilise son index pour y accéder. **L'index va chercher la valeur via l'adresse mémoire.**

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

### 2. Stack (pile)

Une stack est une liste d'éléments qui ne peut être manipulant qu'en ajoutant ou enlevant le sommet de la liste.

Fonctionnement **Last In First Out** (LIFO) : Les derniers éléments ajoutés seront les premiers enlevés.

**Quatre opérations principales :**

- Push : ajouter un nouvel élément au sommet de la stack
- Pop : enlever l'élément au sommet de la stack
- Top : retourner l'élément au sommet de la stack
- isEmpty : retourner *true* si la stack est vide

**Ces opérations sont exécutées en temps constant (O(1))** : on peut traiter des données extrêmement rapidement.

La stack est utilisée :

- Pour les fonctions, la dernière fonction appelée doit finir son exécution puis elle est retirée
- Quand on doit inverser un mot
- Pour l'opération "undo" dans les éditeurs, ou "back" dans les browsers

```jsx
myStack = []

// push operation
myStack.push(1991)
myStack.push(1992)
myStack.push(1993)

// top operation
console.log(myStack[myStack.length - 1])

// pop operation
myStack.pop()

// isEmpty operation
console.log(myStack.length)
```

- **Avantages**
    - Permet de gérer de la data en mode LIFO
    - Certaines opérations sont faites en temps constant O(1)
- **Inconvénients**
    - A cause du LIFO, on ne peut pas accéder directement à un élément au milieu de la stack en temps constant comme un array
    - Créer trop d'éléments dans une stack peut amener à un débordement mémoire = stack overflow

### 3. Queue (file)

Une queue est une **liste d'éléments qui ne peut être manipulée qu'en ajoutant un élément à l'arrière (rear) ou en enlevant un élément à l'avant (front)**. Comme un file d'attente.

**Fonctionnement First In First Out (FIFO).**

Toutes les opérations où les ressources sont partagées entre les utilisateurs et qui fonctionnent en premier arrivé premier servi.

Par exemple : CPU scheduling, Disk scheduling, données asynchrones etc.

**Quatre opérations :**

- Push (enqueue) : ajouter un élément à l'arrière de la queue
- Pop (dequeue) : enlever un élément à l'avant de la queue
- Front (peek) : retourner l'élément à l'avant de la queue
- isEmpty : retourne true si la queue est vide

Fonctionne en temps constant (O(1)). Les queues sont partout en informatique (imprimante par exemple).

```jsx
myQueue = []

// push operation
myQueue.push(1991)

// top operation
console.log(myQueue[0])

// pop operation
myQueue.shift()

// isEmpty operation
console.log(myQueue.length)
```

- **Avantages**
    - Permet de gérer de la data en FIFO
    - Certaines opérations en temps constant
- **Inconvénients**
    - On ne peut pas accéder directement à un élément au milieu de la queue (en temps constant) comme un array

### 4. Linked list (liste chaînée)

**Séquence de nœuds liés aux autres via un pointeur de façon unidirectionnelle**. Chaque élément est un objet.

Chaque séquence commence avec un noeud appelé ***Head*** qui signale le point d'entrée de la liste. Chaque noeud peut contenir la data que l'on souhaite et a une structure particulière composée de deux éléments

- **Value** : la valeur de la donnée contenue dans le noeud
- **Next** : la référence (pointeur) vers le noeud suivant

On ne peut pas accéder directement à un noeud comme dans un array. 

On peut accéder directement à un noeud avec une linked list ne peut se faire qu'en temps linéaire O(n).

Il existe aussi des linked lists bidirectionnelles et circulaires.

On utilise les linked list pour stocker des données quand on ne connait pas le nombre d'éléments (contrairement à un array qui a une taille fixe), on peut donc ajouter et supprimer facilement des nouvelles données.

**Opérations principales :**

- Insert : ajouter un nouveau noeud après un noeud existant
- Remove : supprimer un noeud après un noeud existant
- Front : retourner le premier noeud (*Head*)
- isEmpty : retourne *true* si la liste est vide

```jsx
class Node {
	constructor (value = null) {
		this.value = value
		this.next = null
	}
}

class LinkedList {
	constructor () {
		this.head = null
	}
	
	* nodes() {
		let node = this.head

		while (node != null) {
			yield node
			node = node.next
		}
	}

	insertAtBeginning(node) {
		node.next = this.head
		this.head = node
	}

	isEmpty() {
		if(!this.head) return 1

		return 0
	}

	removeNode(nodeToRemove) {
		if (this.head === nodeToRemove) {
		
		    this.head = this.head.next
		    return
		}

		let previous_node = this.head

		for (let node of this.nodes()) {
			if (node === nodeToRemove)
			    previous_node.next = node.next
			    return
			}
			previous_node = node
		}
	}
}

const myLinkedList = new LinkedList()

firstNode = new Node(1998)
secondeNode = new Node(2006)
badNode= new Node(2020)
thirdNode = new Node(2018)

secondeNode.next = badNode
badNode.next = thirdNode

myLinkedList.head = secondNode

// insert operation
myLinkedList.insertAtBeginning(firstNode)

// remove operation
myLinkedList.removeNode(badNode)

// front operation
console.log(myLinkedList.head.value)

// isEmpty operation
console.log(myLinkedList.isEmpty())

// show linked list
for (let node of myLinkedList.nodes()) {
	console.log(node.value)
}
```

- **Avantages**
    - La taille mémoire n'est pas fixe, c'est donc très flexible
    - Certaines opérations d'insertion et de suppression peuvent être faites en temps constant (O(1))
- **Inconvénients**
    - On ne peut pas accéder directement à un élément au milieu de la liste comme un array
    - De l'espace mémoire est utilisé, en plus de la valeur, pour chaque noeud pour les pointeurs
