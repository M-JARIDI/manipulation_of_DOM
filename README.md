# manipulation_of_DOM


### Pour la recherche des éléments :
	document.getElementById();
	document.getElementsByClassName();
	document.getElementsByTagName();
	document.querySelector(); //renvoie le premier element trouvé
	document.querySelectorAll(); //renvoie toutes les éléments trouvés
	element.children  : cette propriété nous retourne la liste des enfants de cet élément ;
	element.parentElement  : cette propriété nous retourne l'élément parent de celui-ci ;
	element.nextElementSibling  /  element.previousElementSibling  : ces propriétés nous permettent de naviguer vers l'élément suivant / précédent de même niveau que notre élément.


### Pour modifier le contenu d'un élément, on a les propriètés suivantes : 
	- innerHTML : demande à ce que vous entriez du texte représentant un contenu HTML. Par exemple :  "<p>Voici un exemple de contenu pour <strong>innerHTML</strong></p>"
	- textContent : demande un simple texte qui ne sera pas interprété comme étant du HTML.

### Pour modifier les classes (let elt = document.getElementById('main');) :
	elt.classList.add("nouvelleClasse");    // Ajoute la classe nouvelleClasse à l'élément
	elt.classList.remove("nouvelleClasse"); // Supprime la classe nouvelleClasse que l'on venait d'ajouter
	elt.classList.contains("nouvelleClasse");   // Retournera false car on vient de la supprimer
	elt.classList.replace("oldClass", "newClass"): // Remplacera oldClass par newClass si oldClass était présente sur l'élément

Changez les styles d'un élément :
	elt.style.color = "#fff";      // Change la couleur du texte de l'élément à blanche
	elt.style.backgroundColor = "#000"; // Change la couleur de fond de l'élément en noir
	elt.style.fontWeight = "bold"; // Met le texte de l'élément en gras

Modifiez les attributs (elt  faisant référence à un élément de type  input par exmp) :
	elt.setAttribute("type", "password");   // Change le type de l'input en un type password
	elt.setAttribute("name", "my-password");    // Change le nom de l'input en my-password
	elt.getAttribute("name");               // Retourne my-password
	//elt.removeAttribute(nom_attribute);
	//elt.hasAttribute(nom_attribute);

Créez de nouveaux éléments :
	const newElt = document.createElement("div");
	Remarque :
		Un élément créé avec cette fonction ne fait pas encore partie du document, vous ne le verrez donc pas sur votre page. Pour le voir, il va d'abord falloir l'ajouter en tant qu'enfant à un élément.


Ajoutez des enfants :
	const newElt = document.createElement("div");
	let elt = document.getElementById("main");
	elt.appendChild(newElt);

Supprimez et remplacez des éléments :
	const newElt = document.createElement("div");
	let elt = document.getElementById("main");
	elt.appendChild(newElt);

	elt.removeChild(newElt);    // Supprime l'élément newElt de l'élément elt
	elt.replaceChild(document.createElement("article"), newElt);    // Remplace l'élément newElt par un nouvel élément de type article


Réagissez lors d'un clic sur élément :
	la fonction addEventListener(<event>, <callback>)
	exemple :
		const elt = document.getElementById('mon-lien');    // On récupère l'élément sur lequel on veut détecter le clic
		elt.addEventListener('click', function() {          // On écoute l'événement click
  		elt.innerHTML = "C'est cliqué !";               // On change le contenu de notre élément pour afficher "C'est cliqué !"
		});

	preventDefault()
	exemple :
		const elt = document.getElementById('mon-lien');    // On récupère l'élément sur lequel on veut détecter le clic
		elt.addEventListener('click', function(event) {     // On écoute l'événement click, notre callback prend un paramètre que nous avons appelé event ici
    		event.preventDefault();                         // On utilise la fonction preventDefault de notre objet event pour empêcher le comportement par défaut de cet élément lors du clic de la souris
		});

	stopPropagation() , vous pouvez ainsi empêcher que d'autres éléments (les parents) reçoivent l'événement.
	exemple :
		elementInterieur.addEventListener('click', function(event) {
    		event.stopPropagation();
  		elementAvecMessage.innerHTML = "Message de l'élément intérieur";
		}); //l'élément parent ne recevra plus le clic
	
	
Détectez le mouvement de la souris :
	exemple :
		elt.addEventListener('mousemove', function(event) {
    		const x = event.offsetX; // Coordonnée X de la souris dans l'élément
  		const y = event.offsetY; // Coordonnée Y de la souris dans l'élément
		});
	
- /! \à ne pas oublier les deux événements 'onInput' et 'onChange' d'un champ de texte. 
	myInput.addEventListener('input', function(e) {} // en temps réel
	myInput.addEventListener('change', function(e) {} // après perdre le focus


- AJAX (Asynchronous JavaScript And Xml) :
	Il s'agit d'un ensemble d'objets et de fonctions mis à disposition par le langage JavaScript, afin d'exécuter des requêtes HTTP de manière asynchrone.

- Construitre et envoyer une première requête HTTP avec AJAX :
	var request = new XMLHttpRequest();
	request.open("GET", "http://url-service-web.com/api/users");
	request.send();

- Récupérez le résultat de la requête :
	var request = new XMLHttpRequest();
	request.onreadystatechange = function() {
    		if (this.readyState == XMLHttpRequest.DONE && this.status == 200) {
        		var response = JSON.parse(this.responseText);
        		console.log(response.current_condition.condition);
    		}
	};
	request.open("GET", "https://www.prevision-meteo.ch/services/json/paris");
	request.send();

- Validez les données saisies par vos utilisateurs :
	-> Never trust user input!
	-> Validez les données suite à des événements
		myInput.addEventListener('input', function(e) {
    		var value = e.target.value;
   		 if (value.startsWith('Hello ')) {
        			isValid = true;
    		} else {
       			 isValid = false;
    		          }
		});
	-> Faites une validation plus complexe avec les Regex : il s'agit d'un format spécial qui permet de matcher du texte, c'est-à-dire de vérifier qu'un texte corresponde à une description que l'on a définie.
		exemple : si l'on veut savoir si notre texte commence par la lettre  e  et est suivi d'au moins 3 chiffres, on écrira la regex suivante :  
			function isValid(value) {
   				 return /^e[0-9]{3,}$/.test(value);
			}

- Découvrez les contraintes HTML5 :
	-> L'attribut type pour les inputs : text, password; email, tel, URL, date ...
	-> Les  attributs de validation simples : min/max, required, step, minlength/maxlength ...
	-> L'attribut pattern : Il suffit de définir une Regex dans cet attribut, et vous obligez la valeur du champ correspondant à la respecter.
		<input type="text" pattern="[0-9]{,3}" />

- Envoyez des données avec une requête POST :
	exemple :
		var request = new XMLHttpRequest();
		request.open("POST", "http://url-service-web.com/api/users");
		request.setRequestHeader("Content-Type", "application/json");
		request.send(JSON.stringify(jsonBody));


JavaScript est synchrone et Mono-thread, donc comment fonctionne l'asynchrone en JS ?
	-> Réponse : par ce qu'on appelle "l'event Loop".
		En JavaScript, chaque ligne de code est exécutée de façon synchrone, mais il est possible de demander à exécuter du code de manière asynchrone. Et lorsque l'on demande à exécuter 		une fonction de façon asynchrone, la fonction en question est placée dans une sorte de file d'attente qui va exécuter toutes les fonctions qu'elle contient les unes après les autres. C'est ce 		qu'on appelle l'event loop.

comment demander à exécuter du code de manière asynchrone ?
	-> Réponse : - la fonction setTimeOut(nom_function, délai) // délai en millisecondes, avant d'exécuter cette fonction.
				À retarder l'exécution d'une fonction du temps indiqué
		    - la fonction setInterval(...) : elle exécute la fonction passée en paramètre en boucle à une fréquence déterminée par le temps en millisecondes passé en second paramètre.
Remarque :
	tout ce qui touche à l'I/O peut être exécuté de manière asynchrone (la lecture/écriture des fichiers, aux requêtes HTTP, etc.).


 comment on peut exécuter du code asynchrone et renvoyer le résultat que l'on souhaite à celui qui a lancé le code ?
	- les fonctions de CallBack : Les callbacks sont la base de l'asynchrone en JavaScript et sont très utilisées.
		Remarque : C'est bien beau de gérer du code asynchrone, mais rien ne vous garantit que tout se soit bien passé. Il nous faut donc un mécanisme pour savoir si une erreur est survenue
			  d'où le rôle de la gestion des erreurs.
			Exemple :
				fs.readFile(filePath, function(err, data) {
   					 if (err) {
        						throw err;
    					}
    					// Do something with data
					});
	- Les promises : (sont faciles à lire par rapport les CallBacks) : Cette promesse est en fait un objet Promise qui peut être  "resolve"  avec un résultat, ou  "reject"  avec une erreur.	
		exemple :
			functionThatReturnsAPromise()
   	 			.then(function(data) {
        					// Do somthing with data 
    				})
    				.catch(function(err) {
       					 // Do something with error
    			});
		Remarque : Le gros avantage est que l'on peut aussi chaîner les  Promises
		exmple :
			returnAPromiseWithNumber2()
    				.then(function(data) { // Data is 2
        					return data + 1;
    				})
    				.then(function(data) { // Data is 3
       				 	throw new Error('error');
    				})
    				.then(function(data) {
       					 // Not executed  
    				})
    				.catch(function(err) {
       		 			return 5;
    				})
    				.then(function(data) { // Data is 5
       					 // Do something
   				 });

	- Async/Await : permettent de gérer le code asynchrone de manière beaucoup plus intuitive, en bloquant l'exécution d'un code asynchrone jusqu'à ce qu'il retourne un résultat.
		exemple :
			async function fonctionAsynchrone1() {/* code asynchrone */}
			async function fonctionAsynchrone2() {/* code asynchrone */}

			async function fonctionAsynchrone3() {
 				const value1 = await fonctionAsynchrone1();
 				const value2 = await fonctionAsynchrone2();
 				return value1 + value2;
			}
		Remarque : utilisent les Promises en arrière-plan, il est donc possible d'utiliser les 2 en même temps.
		Gestion des erreurs : il suffit d'exécuter notre code asynchrone dans un bloc  try {} catch (e) {} , l'erreur étant envoyée dans le catch
		Remarque 2 : async  et  await  sont des mots clés du langage JavaScript, qui permettent de créer du code asynchrone qui utilisera les  Promise  en arrière-plan.


Parallélisez plusieurs requêtes HTTP : comment enchaîner les requêtes HTTP ?
	exemple : enchaîner les requêtes HTTP en exécutant 2 requêtes GET en même temps (en parallèle), puis 1 requête POST une fois que les 2 requêtes précédentes sont terminées (en séquence).
	-> Enchaînez des requêtes avec les callbacks
	-> Enchaînez des requêtes avec les Promises
	-> Enchaînez des requêtes avec async/await

- Optimisez votre code par Linter, minifier, bundler et transpiler :
	
	bundler (exp : webpack) : il va vous permettre de compiler votre code et de tout packager en un seul fichier


