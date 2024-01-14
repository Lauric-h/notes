# GET et POST
#web #learnings #http

[https://developer.mozilla.org/fr/docs/Web/Guide/HTML/Formulaires/Envoyer_et_extraire_les_données_des_formulaires](https://developer.mozilla.org/fr/docs/Web/Guide/HTML/Formulaires/Envoyer_et_extraire_les_donn%C3%A9es_des_formulaires)

Dans un formulaire HTML, on choisit entre les méthodes GET et POST.

Dans une requête HTTP, on retrouve 2 parties : un header (en-tête) et le corps (body).

## Get

- Utilisée pour demander au serveur de renvoyer une certaine ressource
- "Hé le serveur, je veux cette ressource"
- Si un formulaire est envoyé avec cette méthode : les données envoyées sont ajoutées dans l'URL sous forme de paires nom/valeur

> [ww.foo.com/?say=Hi&to=Mom](http://ww.foo.com/?say=Hi&to=Mom)
> 

La requête HTTP ressemble à :

> GET /?say=Hi&to=Mom HTTP/1.1
> 

**La taille d'une URL est limitée, et les données sont visibles dans l'URL (= pas secure)**

---

## Post

- Demande au serveur une réponse prenant en compte ce qui est dans le corps de la requête
- « Hé serveur ! vois ces données et renvoie-moi le résultat approprié »
- Si un formulaire est envoyé avec cette méthode, les données sont ajoutées au corps de la requête HTTP.
- Aucune donnée n'est ajoutée à l'URL
- Elle n'a pas de taille limite

> POST / HTTP/1.1
Host: [foo.com](http://foo.com/)
Content-Type: application/x-www-form-urlencoded
Content-Length: 13
say=Hi&to=Mom
> 

**La méthode est recommandée pour modifier les données sur le serveur et pour les données sensibles**