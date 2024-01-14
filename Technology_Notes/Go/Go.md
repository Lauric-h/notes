# Go

#go #language 

[https://golang.org/doc/code](https://golang.org/doc/code)

[https://golang.org/doc/effective_go](https://golang.org/doc/effective_go)

## Code organization

Go programs are organized in **package**.

**Package** = a collection of source files in the same directory that are compiled together.

⇒ On a accès aux fonctions, variables etc.

---

**Repository** = contient un ou plusieurs **modules**

**Module** = a collection of related go packages that are released together

Un Repository contient un seule module situé à la racine. Un fichier go.mod déclare le module path (prefix_ pour tous les packages à l'intérieur du module. Le module contient tous les packages du dossier.

---

**Import path** = string utilisée pour importer un package.

Les packages de la librairie standard n'ont pas de préfixe

⇒ Le premier statement d'un fichier Go doit être le nom du package.

Une fonction avec une première lettre en majuscule est exportée et peut être utilisée dans d'autres packages.

## Formatting

⇒ gofmt s'occupe tout seul du formatage

- Utiliser tabs pour indentation
- Pas de limite de longueur de ligne\
- Privilégier les line comment // plutot que les blocks /*
- Il existe un program godoc qui extrait les commentaires /* avant les déclarations pour en faire de la doc
- Chaque package doit avoir un block de commentaire de package, qui commence par le nom due l'item qu'il décrit
- Les commentaires sont formattés automatiquement
- Chaque nom exporté (1e lettre majuscule) doit avoir un commentaire de doc
- La visibilié d'un nom en dehors d'un package est déterminée par sa 1e lettre : majuscule = visible, minuscule = non visible
- Les packages doivent avoir un nom court, concis et en minuscule
- Getters : pas besoin de mettre get dans le nom du getter : un getter pour un attribut owner devrait s'appeler Owner (majuscule = exporté)
- Setter : on utiliser SetOwner (majuscule = exporté)
- Les interfaces avec une seule méthodes utilisent le nom + -er suffixe : Reader, Writer, Formatter...

## Control structures

### If

- Pas de parenthèses
- Les  { } sont obligatoires
- On peut initialiser une variable dans le if

```kotlin
if err := file.Chmod(0664); err != nil {
	// do stuf
}
```

### For

```kotlin
// Like a C for
for init; condition; post { }

// Like a C while
for condition { }

// Like a C for(;;)
for { }
```

- Quand on itère sur un array, string, map etc. on utilise range

```kotlin
for key, value := range oldMap {
	// stuff
}
```

- Si on a besoin que du premier item d'un range on peut laisser tomber le 2e

```kotlin
for key := range m { }
```

- Par contre si on a besoin que du second, on doit utiliser le blank identifier (_) pour laisser tomber le premier :

```kotlin
for _, value := range array { }
```

### Switch

- On peut utiliser switch sans expression = switch(true) ⇒ On peut donc remplacer if-else-if-else par un switch
- Pas besoin de break, mais on peut les utiliser quand meme
- Si on a besoin de sortir d'une loop qui englobe un switch, on peut ajouter un label au break pour indiquer qu'on veut sortir de la loop et non du switch

```go
Loop:
	for n := 0; n < len(src); n += size {
		switch {
		case src[n] < sizeOne:
			if validateOnly {
				break
			}
			size = 1
			update(src[n])

		case src[n] < sizeTwo:
			if n+1 >= len(src) {
				err = errShortInput
				break Loop
			}
			if validateOnly {
				break
			}
			size = 2
			update(src[n] + src[n+1]<<shift)
		}
	}
```

## Functions

- On peut retourner plusieurs valeurs +> aide à gérer les erreurs

```go
func (file *File) Write(b []byte) (int,error)
```

- On peut nommer les paramètres de retour attendus  ⇒ les variables sont initialisées à leur valeur 0 au début de la fonction. Si la fonction se termine avec un return sans argument, alors la fonction retourne les valeurs courantes des variables

```go
func nextInt(b []byte, pos int) (value, nextPos int) {
```

### Defer

⇒ Le statement defer programme l'appel de la fonction deferée juste après que la fonction qui execute defer (celle qui l'englobe) retourne.

⇒ On l'utilise souvent pour close() ⇒ permet d'éviter d'oublier de fermer un fichier, et de faire apparaître le close() à côté de l'ouverture, ce qui rend la chose plus claire.

- Les arguments passés à la fonction déférée sont évalués quand defer execute et non quand le call de defer est executé.

## Data

⇒ 2 types de primitives pour allouer des données : new et make

### New

- Alloue de la mémoire mais n'initialise pas la mémoire ⇒ il la remplit de valeur 0

→ new(T) alloue de la place mémoire pour un nouvel item de type *T avec sa valeur 0, et retourne son adresse ⇒ débloque simplement de la mémoire pour un objet, prêt à être utilisé

→ On peut créer une nouvelle instance avec un **composite literal**

```go
func NewFile(fd int, name string) *File {
    if fd < 0 {
        return nil
    }
    f := File{fd, name, nil, 0}
    return &f
}
```

⇒ On peut même combiner les deux dernières lignes : ca alloue une nouvlle instance a chaque fois  que c'est évalué

```go
return &File{fd, name, nil, 0}
```

Si un composite literal ne contient pas de fields, ca crée des zero value pour le type

Les expression new(File) et &File{} sont équivalentes

### Make

⇒ Crée uniquement des slices, maps et channels et retourne une valeur de type T ( pas *T) **initialisée** et non de valeur 0.

Sous le capot, ces 3 types doivent être initialisés avant d'etre utilisés.

```go
var p *[]int = new([]int)       // allocates slice structure; *p == nil; rarely useful
var v  []int = make([]int, 100) // the slice v now refers to a new array of 100 ints

// Unnecessarily complex:
var p *[]int = new([]int)
*p = make([]int, 100, 100)

// Idiomatic:
v := make([]int, 100)
```

Make ne s'applique qu'aux maps, arrays, slices et ne retourne pas de pointer.

### Arrays

- Les arrays sont passés par valeur : assigner un array a un autre copie tous les éléments
- Si on passe un array à une fonction, elle recoit une **copie** de l'array et pas un pointer vers l'array
- La taille de l'array fait partie de son type : [10]int et [20]int sont distincts

⇒ Les arrays servent surtout de base aux Slices

### Slices

→ On utilise la plupart du temps des slices plutot que des arrays

→ Un slice contient une référence vers un array ⇒ Si on assigne un slice à un autre, les deux feront référence au même array ⇒ Si on passe un slice à une fonction, les changements seront faits faits sur l'array (comme si on passait un pointer)

- La length d'un slice (len) peut être modifiée tant que c'est dans les limites de l'array.
- La capacity (cap) d'un slice donne la taille maximale du slice>
- ⇒ Si la data est plus grande que la capacité, le slice est réalloué.
- On peut avoir des array/slice multidimensionnels en déclarant un array/slice d'array/slice
- 

```go
type Transform [3][3]float64  // A 3x3 array, really an array of arrays.
type LinesOfText [][]byte     // A slice of byte slices.
```

### Maps

⇒ Ensemble de clé/valeur 

→ Comme les slices, les maps font références à une autre data structure, donc si on passe une map en paramètre d'une fonction, les changements seront visibles.

```go
// Construction avec composite literal
var timeZone = map[string]int{
    "UTC":  0*60*60,
    "EST": -5*60*60,
    "CST": -6*60*60,
    "MST": -7*60*60,
    "PST": -8*60*60,
}
```

- Si on essaie d'accéder à une clé qui n'existe pas dans la map retourne zéro
    - Si on doit distinguer une valeur absente d'une valeur 0 on utilise le "**comma ok**" idiom
        - Si tz est présent: seconds sera assigné et ok sera true, sinon seconds sera 0 et ok sera false :
    
    ```go
    var seconds int
    var ok bool
    seconds, ok = timeZone[tz]
    
    // on peut écrire
    seconds, ok := timeZone[tz]
    
    // On peut tester la présence de valeur sans avoir à se préoccuper de la valeur en utilisant le blank identifier
    _, present := timeZone[tz]
    ```
    
- Pour supprimer une entrée de map on utilise delete(map, key)

```go
delete(timeZone, "tz")
```

### Printing

⇒ les fonctions font partie du package fmt

```go
fmt.Printf("Hello %d\n", 23)
fmt.Fprint(os.Stdout, "Hello ", 23, "\n")
fmt.Println("Hello", 23)
fmt.Println(fmt.Sprint("Hello ", 23))
```

→ Pour les structs, le format %v+ formate le field avec son nom et le format &#v formate en syntaxe Go

→ %T imprime le type d'une valeur

→ On peut controler le format par défaut de print d'un type en définissant une méthode String() (⇒ équivalent d'une méthode toString() @override en java)

```go
func (t *T) String() string {
    return fmt.Sprintf("%d/%g/%q", t.a, t.b, t.c)
}
fmt.Printf("%v\n", t)
```

### Append

→ On peut utiliser ...interface{} pour préciser qu'on accepte un nombre variable d'arguments

```go
func append(slice []T, elements ...T) []T
```

⇒ Append ajoute les éléments à la fin de la slice et retourne le résultat

→ On peut append un slice à un slice avec ...

```go
x := []int{1,2,3}
y := []int{4,5,6}
x = append(x, y...)
fmt.Println(x)
```

## Initialization

### Constants

→ Seulement numbers, char (runes), strings or booleans

→ Crées à la compilation

→ utilise le mot const, on peut aussi en déclarer plusieurs d'un coup

```go
const a = 50
const (
	name = "John"
  age = 50
  country = "Canada"
)
```

## Function literals

## Methods

### Pointers vs value

→ On peut définir des méthodes sur n'importe quel type nommé

```go
type ByteSlice []byte
func (slice ByteSlice) DoStuff() {}
```

On peut aussi modifier le type qui appelle

```go
func (slice *ByteSlice) DoStuff{}
```

⇒ Value methods can be invoked on pointers and values, but pointer methods can only be invoked on pointers

⇒ Pointer methods can modify the receiver, invoking them on a value would cause the method to receive a copy of the value, so any modifications would be discarded

## Interfaces

⇒ Spécifier le comportement d'un objet

- Un type peut implémenter plusieurs interfaces
- Un type n'a pas besoin de dire explicitement qu'il implémente une interface, il a simplement besoin d'implémenter la méthode de l'interface
- On peut convertir un type en un autre type en implémentant les méthodes du type

→ Regroupe les types avec leurs méthodes 

## Blank identifier

⇒ Peut être assigné ou déclaré avec n'importe quelle valeur de n'importe quel type. La valeur est écartée sans conséquences. ⇒ On l'utilise en placeholder, quand une variable est nécessaire mais la valeur importe peu.

### multiple assignment

⇒ Quand un assignment a besoin de plusieurs valeurs du côté gauche mais qu'une valeur ne sera pas utilisée, on utilise _

Exemple : on ignore la valeur pour garder que l'erreur 

```go
if _, err := os.Stat(path); os.IsNotExist(err) {
	fmt.Printf("%s does not exist\n", path)
}
```

→ On peut utiliser les blank identifier pour que le programme compile même avec des imports ou variables non utilisés (en phase de dev/debug, pas en prod)

→ On peut donner un nom blank à un package pour utiliser seulement son side effect et non l'utiliser explicitement

```go
import _ "net/http/pprof"
```

## Embedding

⇒ Permet de composer des types en désignant un struct ou interfaces comme field d'un struc ou interface

## Concurrency

→ Go encourage le partage de valeurs via les channels. Une seule Goroutine a accès à la valeur à un temps donné.

> Do not communicate by sharing memory; instead, share memory by communicating
> 

⇒ On utilise les channels pour controler l'accès.

### Goroutines

⇒ Function executing concurrently with other goroutines in the same address space.

→ Multiplexed onto multiple OS threads = if one block, others continue to run,

→ Utilisation : on prefixe une fonction ou méthode avec go. Quand l'appel est terminé, la goroutines se termine, silencieusement.

```go
go list.Sort()
```

On peut utiliser une function literal :

```go
func Announce(message string, delay time.Duration) {
    go func() {
        time.Sleep(delay)
        fmt.Println(message)
    }()  // Note the parentheses - must call the function.
}
```

### Channels

→ Les channels sont alloués avec make. On peut mettre un int en 2e paramètre, signalant une taille de buffer  (facultatif)

```go
ci := make(chan int)            // unbuffered channel of integers
cj := make(chan int, 0)         // unbuffered channel of integers
cs := make(chan *os.File, 100)  // buffered channel of pointers to Files
```

Un channel peut faire en sorte d'attendre que la goroutine ait terminé

```go
c := make(chan int)
// Start the sort in a goroutine; when it completes, signal on the channel.
go func() {
	list.Sort()
	c <- 1 // Send a signal; value does not matter.
}()
doSomethingForAWhile()
<-c // Wait for sort to finish; discard sent value.
```

→ Les receiver bloquent jusqu'à ce qu'ils aient recu la donnée. Si le channel est unbefferd, l'expéditeur bloque jusqu'à ce que le receiver ait recu la donnée. Si le channel a un buffer, l'expéditeur bloque seulement jusqu'à ce que la valeur ait été copiée dans le buffer. Si le buffer est full, il faut attendre qu'un autre receiver recoive la valeur.

- Un channel est une valeur de première classe et peut être alloué et passé comme n'importe quelle autre.

### Parallelization

→ Paralléliser une calculation à travers plusieurs cores CPU. Si la calculation peut être découpée en plusieurs pièces qui peuvent s'executer indépendemment, elle peut être parallélisée, avec un channel pour signaler quand les différentes pièces sont complètes.

Concurrency ≠ parallélisation

## Errors

→ Gestion explicite des erreurs

### Exepected errors

Valider un email, vérifier les accès d'un utilisateur etc.

⇒Doit toujours retourner une erreur : on choisit ce qu'on veut faire de l'erreur.

### Unexpected errors

⇒ Erreur qui mettent le système dans un état non récupérable : BDD non accessible, invalid state, divisé par zéro etc.

On ne teste pas ces erreurs, elles sont prises pour acquis.

→ On peut remplacer les return err par panic(err)

→ On peut extraire la gestion des erreurs dans une autre fonction pour rendre le code plus lisible

### Panic

→ Quand une erreur est unrecoverable, on peut utiliser panic qui crée une  run-time error et stop le programme avec un message qu'on lui passe.

### Recover

→ Quand panic est appelé, cela stop l'execution de la fonction et commence à remonter toute la stack. Une fois la stack remontée, le programme s'arrête.

→ Il existe un moyen de reprendre le controle de la fonction et continuer l'execution : recover

⇒ Un appel à recover stop la remontée de la stack et retourn l'argument passé à panic. Recover est seulement utile dans des fonction defer.

Une application de recover est de stopper une goroutine défectueuse dans un serveur sans tuer les autre goroutines

```go
func server(workChan <-chan *Work) {
    for work := range workChan {
        go safelyDo(work)
    }
}

func safelyDo(work *Work) {
    defer func() {
        if err := recover(); err != nil {
            log.Println("work failed:", err)
        }
    }()
    do(work)
}
```