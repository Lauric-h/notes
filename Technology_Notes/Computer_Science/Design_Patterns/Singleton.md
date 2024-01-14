# Singleton

#computerscience #designpatterns 

⇒ Permet d'avoir une seule instance d'accès á la base de données.

→ Le client n'est censé utiliser que la fonction getInstance.

- On vérifie si l'instance existe déjà
- Si oui : on retourne l'existante
- Si non : on la créer via la fonction interne

![https://i.imgur.com/cpQEHr5.png](https://i.imgur.com/cpQEHr5.png)

## Principes

- On rend privé les constructeurs
- On construit un pseudo constructor :
    - On déclare une méthode staique qui retournera un objet correspondant au type de la classe : on peut controler la valeur qu'on veut retourner → le fait qu'elle soit statique permet de pouvoir l'appeler sans instancier la classe : par convention on l'appelle getInstance
- Créer un attribut statique qu iva permettre de stocker l'unique instance de la classe
- Dans le pseudo constructeur (getInstance) on test l'attribut : si null on crée une instance, sinon c'est que l'attribut possède déjà une instance
- On retourne la valeur de l'attribut possédant l'unique instance de la classe,

![https://refactoring.guru/images/patterns/diagrams/singleton/structure-en-indexed.png](https://refactoring.guru/images/patterns/diagrams/singleton/structure-en-indexed.png)

```php
class Singleton
{
/**
     * The Singleton's instance is stored in a static field. This field is an
     * array, because we'll allow our Singleton to have subclasses. Each item in
     * this array will be an instance of a specific Singleton's subclass. You'll
     * see how this works in a moment.
     */
	private static $instance = [];

	protected function __construct() {}
/**
     * This is the static method that controls the access to the singleton
     * instance. On the first run, it creates a singleton object and places it
     * into the static field. On subsequent runs, it returns the client existing
     * object stored in the static field.
     *
     * This implementation lets you subclass the Singleton class while keeping
     * just one instance of each subclass around.
     */

	public static function getInstance() {
		$cls = static::class;
		if (!isset(self::$instance[$cls] {
			self::$instance[$cls] = new static ();
		}
		return self::$instance[$cls];
	}

// client code

function clientCdode() {
	$s1 = Singleton::getInstance();
}
```

## Inconvénients

Anti pattern :

- Pas adapté au multi threading (plusieurs instances)
- Viole le principe SOLID : résoud 2 problèmes en même temps
- Utilise des variables globales