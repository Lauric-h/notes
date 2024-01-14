# REGEX

#javascript #regex

Special string qui représentent un schéma de recherche souhaité pour qu'on puisse trouver ce qu'on veut.

On utilise /expression/

La regex cherche littéralement l'expression, elle prend en compte la casse.

 **Ignorer la casse avec le flag i** (ignoreCase) : /expression/**i**

**Chercher une string avec plusieurs possibilités |** : /yes**|**no/

**Chercher ou extraire plus d'une seule fois avec le flag g** (global) : /expression/**g**


## Méthodes :

### .test()

Appliquée à une string. Retourne true ou false si la regex se trouve dedans.

regex.test(string)

### .match()

Extrait le mot cherché et retourne un array.

string.match(regex)

.exec()

Execute une recherche sur la string. Retourne un array ou null.

regex.exec(string)

.matchAll()

Retourne un itérateur contenant tous les matchs.

string.matchAll(regex)

.search()

### Retourne l'index du match.

string.search(regex)

### .replace()

Execute une recherche, et remplace le match avec ce qu'on veut.

const newStr = str.replace(regexp|substr, newSubstr|function)

### .replaceAll()

Execute une recherche, et remplace les matchs avec ce qu'on veut.

const newStr = str.replaceAll(regexp|substr, newSubstr|function)

### .split()

Utilise une regex pour séparer une string dans un array de substring

str.split([separator[, limit]])

## Lookahead

**Positive** : S'assurer que l'élément est là mais ne le match pas : (?=)

**Negative** : S'assurer que l'élément n'est pas là : (?!)

***On peut utiliser des regex viewer pour tester et débugguer les expressions.***