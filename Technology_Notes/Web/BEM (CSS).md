
#web #css #learnings 

[https://www.alsacreations.com/article/lire/1641-bonnes-pratiques-en-css-bem-et-oocss.html](https://www.alsacreations.com/article/lire/1641-bonnes-pratiques-en-css-bem-et-oocss.html)

[https://getbem.com/introduction/](https://getbem.com/introduction/)

BEM est utile pour organiser son code CSS.

## BEM = Block Element Modifier

![](https://www.alsacreations.com/xmedia/doc/original/bem-blocks-540.jpg)

Les éléments sont classés en 3 catégories :

- **Le Block :** entité indépendante, il ne dépend pas du contexte d'autres blocks ou éléments.
- **Les éléments** : composent un block, et agissent dans le contexte de celui-ci.
- **Les modifiers** : ils modifient les blocks ou les éléments.

L'organisation BEM dicte 3 règles :

1. Les blocks et éléments doivent chacun avoir un nom unique (on n'utilise pas d'ID non plus)
2. Les sélecteurs ne doivent pas utiliser les noms d'éléments HTML
3. Les cascades doivent être évitées

```css
.block-name
.block-name__element_name
.block-name--modifier
.block-name__element_name--modifier

```

⇒ BEM permet de mieux organiser et structurer son code, d'améliorer le rendu des pages en évitant les styles en cascade. Les noms explicites permettent aussi d'identifier rapidement quels éléments dépendent de quel block et les fonctions des classses
