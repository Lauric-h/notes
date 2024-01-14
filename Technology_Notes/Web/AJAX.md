#web #learnings
# AJAX

**A**synchronous **Ja**vaScript and **X**ML > permet d"update une page dynamiquement.

⇒ refresh certaines sections d"une page mais pas toute la page. 

⇒ Par exemple : maj du score sur une page de sport, page de notre inbox quand on reçoit un email.

Il faut créer un nouvel objet JS appelé **XMLHttpRequest**

```jsx
var xhttp = new XMLHttpRequest()
```

Une fois l'objet défini, il faut définir son comportement onreadystatechange.

⇒ fonction (anonyme) qui sera appelée quand la requete asynchrone HTTP sera complète, et défini ce qui est censé changer sur le site.

La requete XMLHttpRequest a 2 autres propriétés qui servent à détecter quand la page a fini de load :

- La propriété readyState change de 0 (request not initialized) à 1, 2 ,3 et 4 (request finished, response ready)
- La propriété status sera 200 OK

Ensuite il faut open() pour définir la requete et send() pour l'envoyer.

```jsx
function ajax_request(argument) {
	var aj = new XMLHttpRequest();
	aj.onreadystatechange = function() {
		if (aj.readyState === 4 && aj.status === 200) {
			// do something
		}
	}
	aj.open("GET", /* url */, true);
	aj.send();
}
```