# Object Oriented Programing

#concept #computerscience #javascript 

**Programmation Orientée Objet est un design pattern qui vise à regrouper son code en objets.**

## Object constructor

Quand on a besoin de dupliquer un objet, on utilise une **fonction constructor** qui nous sert à créer des instances de l'objet avec le mot new.

On a accès au constructor avec newobj.constructor.

Plusieurs règles

- Sont définies avec une majuscule
- Utilisent this pour déifnir les propriétés
- Définissent des propriétés et méthodes au lieu de retourner une valeur

On peut vérifier si un objet a été créé avec une constructor avec instance of obj

```jsx
function Player(name, score) {
	this.name = name,
	this.score = score
}
const player1 = new Player('Olrik', 2)
```

## Object Prototype

Tous les objets ont un prototype = un objet dont l'objet original hérite. Il a accès à toutes les propriétés et méthodes.

Quand on créé la fonction constructor, un prototype se crée. Le prototype a une propriété constructor qui est une référence à la fonction.

Quand on créé une instance de l'objet avec new, une propriété prototype est ajoutée : c'est une référence au prototype du constructor. 

Chaque instance du constructor a accès au prototype du constructor.

Toutes les fonctions ont une propriété prototype (vide par défaut). Utilisée principalement pour l'héritage.

**Prototype Attribute** : Cette caractéristique donne le parent de l'objet. Chaque objet hérite de ses propriétés par un autre objet.

Tous les objets créés avec Object literal ( = {} ) object constructor héritent de l'objet Object.prototype.

La méthode recommandée pour définir le prototype d'un objet est Object.create.

monObjet.prototype = Object.create(unObjet.prototype)

Quand on définit le prototype manuellement, ça efface la propriété constructor, il faut la redéfinir manuellement.

## Héritage

L'héritage est un paradigme. **Les objets peuvent hériter entre eux des propriétés et méthodes.**

Permet de respecter le principe **DRY (Don't Repeat Yourself).**

Pour utiliser au mieux l'héritage il faut créer une instance avec Object.create(obj).

**La prototype chain** : JS remonte la chaîne pour trouver la propriété à laquelle on veut accéder. D'abord localement puis elle remonte via la propriété prototype jusqu'à Object.prototype.

C'est grâce à cela que les propriétés du super objet Object.prototype sont accessibles par tous.

Au lieu de créer une nouvelle fonction sur chaque instance de l'objet (utilisant de la mémoire) on créé la fonction sur le prototype, et elle sera accessible par toutes les instances de l'objet.

- Les références d'un prototype ne peuvent pas être circulaires : renvoi ERROR
- La valeur de la propriété prototype ne peut être que null ou un objet, les autres valeurs sont ignorées.

## La valeur de this

this n'est pas affecté par le prototype : **peu importe où la méthode est trouvée, dans l'appel d'une méthode, this est toujours l'objet avant le point.**

admin.fullName : utilise admin pour this car avant le point.

Quand l'objet héritier run la méthode héritée, elle ne modifie que son propre état, pas celui de l'objet parent = **les méthodes sont partagées, pas les états.**

## For...in loop

Cette loop itère sur toutes les propriétés d'un objet.

```jsx
for (let keys in object) {
	// do stuf
}
```

On peut itérer sur des propriétés héritées. 

On peut aussi exclure les propriétés héritées avec obj.hasOwnProperty(key) : retourne true si l'objet a sa propre propriété non héritée.

Toutes les méthodes de Object.prototype sont non énumérables et n'apparaissent pas quand on loop dans un objet.

## Mixins

On peut créer des mixins pour partager des méthodes entre des objets qui n'ont rien à voir.

Par exemple : avion et oiseau volent tous les deux mais n'ont rien à voir.

```jsx
let flyMixin = function(obj) {
	obj.fly = function() {
		// do stuff
	}
}
```

flyMixin(obj) prend n'importe quel objet en argument et lui donne la méthode fly.

## Les classes

ES6 introduit les classes qui permettent une syntaxe plus simple. Tout fonctionne pareil qu'avec un constructor. On utilise le mot class.

Une class a une fonction constructor, mais les propriétés qu'on veut ajouter au prototype sont définies sur la classe elle-même.

```jsx
class Dog {
	constructor(name, breed) {
		this.name = name,
		this.breed = breed
		}
	bark() {
		return 'woof'
	]
]
```

Avec les class, on peut étendre d'autres classes avec le mot extend et super

```jsx
class chihuahua extends Dog {
	constructor(name)
	super(name)
	}
	smallBark() {
		return 'woofy'
	}
}
```

Dans la classe étendue on peut accéder au constructor de la class parent avec super.

On peut définir une instance avec new chihuahua(nom) qui aura accès aux prototypes de Chihuahua **et** Dog.

L'héritage et la chain fonctionnent pareil avec les class.

## Closure

La propriété d'un objet est publique : on peut y accéder et la modifier en dehors de la définition de l'objet. Peu poser des problèmes de sécurité.

Pour rendre la propriété privée, on la créé dans la fonction constructor, limitant ainsi son scope à la fonction. Elle ne sera donc pas accessible globalement

La méthode a accès à la variable privée car elles sont définies dans le même contexte.

**En JS, une fonction a toujours accès au contexte dans lequel elle est créée = closure.**

```jsx
function Bird() {
	let eggs = 10 // variable pribvée
	this.getEggs = function() {
		// do stuff
	}
}
```

## IIFE : Immediately Invoked Function Expression

Un pattern commun est d'exécuter une fonction dès sa déclaration. On ajoute des **parenthèses ()** à la fin de la fonction, ce qui signifie que l'on veut l'exécuter tout de suite.

Une IIFE est souvent utilisée pour regrouper des fonctionnalités reliées dans un seul objet ou module.

```jsx
let motionModule = (function () {
	return {
		glideMixin: function(obj) {
			obj.glide = function() {
				// do stuff
			};
		},
		flyMixin: function(obj) {
			obj.fly = function() {
				// do stuff
			};
		}
	}
}
// accéder aux fonctions
motionModule.glideMixin(duck)
// ou
duck.glide()
```

On peut regrouper 2 mixins :

Une IIFE qui retourne un objet motionModule qui contient tous les comportements regroupés en un seul objet, qui peut être utilisé par d'autres parties du code.