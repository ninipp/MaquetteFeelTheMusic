# MaquetteFeelTheMusic
Le fond de la page: #2F3038
Le fond du formulaire: #202027
Le fond des inputs: #2F3038
Le fond du footer: #202027
La couleur d'accent: #BC3A80
La couleur du bouton du formulaire: #1867A7

Tu peux retrouver les images et logos nécessaires à la réalisation de cet exercice par ici:

https://github.com/sirius-school/WebDev/tree/main/HTML_CSS/1-html-css-debutant/assets/feelthemusic

Changer le style du menu
Si vous souhaitez changer le style du lien dans le menu en fonction de la page sur laquelle vous êtes, il va falloir de nouveau "hacker" le système un tout petit peu.

On va de nouveau utiliser un peu de JQuery pour parvenir à nos fins.

Créez une nouvelle page nav.jset copiez le code suivant:

$('nav a').each(function() {
  if ($(this).attr('href') == location.href.split("/").slice(-1)){ $(this).addClass('isActive'); }
});
Ce code va sélectionner toutes nos balises <a> contenue dans notre balise <nav>. Donc ayez une navigation dans votre header qui fonctionne avec ce principe, ou alors changer la partie du script pour qu'elle corresponde à ce que vous avez vous. Ensuite le script va comparer le nom du fichier dans l'attribut hrefet le comparer au nom du fichier dans l'adresse du navigateur (sans le .html), si il y a une correspondance il va ajouter une classe 'isActive` à ce lien.

<nav>
  <a href="discover.html">Discover</a>
  <a href="comments.html">Comments</a>
</nav>
Il reste à créer une classe CSS isActive avec les propriétés voulue et le tour est joué.

.isActive{
  background-color: red;
}
❗ N'oubliez pas de lier votre nouvelle page nav.js dans votre header.html!

Variante bonus
Si vous voulez une propriété différente pour chacun de vos liens, vous pouvez employez ce code Jquery.

let fileName = location.href.replace(/\.[^/.]+$/, "").split("/").slice(-1);
$('nav a').each(function() {
  if ($(this).attr('href') == location.href.split("/").slice(-1)){ $(this).addClass(fileName); }
});
Ensuite il faudra un sélecteur CSS pour chacun des noms de fichier que vous avez.

.fileName{
  font-size: 2em;
}
La différence ici c'est qu'il va ajouter une classe avec le même nom que le fichier. Du coup vous pouvez séparer vos styles pour chacun des liens du menu.

Iframes (LEGACY) ⚠️
❗update: ceci n'est vraiment pas une bonne méthode, c'était pour ne pas utiliser de Jquerry ou de framework. Préférez vraiment utiliser la solution plus haut. Je laisse le bout de code à titre informatif.

Alors, ceci est une méthode un peu laborieuse pour arriver à créer une page avec votre header/footer tout seul et pour ensuite le répéter sur toutes vos pages. Cela vous permettra de ne pas avoir à modifier toutes vos pages si vous avez besoin d'éffectuer un changement dans votre header/footer.

Nous allons utiliser une iframe. C'est une sorte de fenêtre sur votre page qui affiche une autre page.

Créez votre page index.html
Créez votre page header.html/footer.html
Créez votre feuille de style style.css
Créez votre feuille de style header.css/footer.css(optionnel)
Placez le code suivant dans votre page index.html là où vous voulez que votre header/footer apparaisse: <iframe src="header.html" seamless></iframe>
Placez le code suivant dans votre style.css: iframe[seamless]{border: 0; width: 100%;}
Tadaamm! Vous avez votre header qui s'affiche.
Petite précision
Cette méthode est plus un hack qu'une bonne pratique. On n'a pas encore vu les outils nécessaire quant à la réalisation de composant réutilisable. Du coup, il faut un petit peu trafiquer le code pour arriver à nos fins.

Le style de header/footer
Même si votre header/footer s'affiche sur votre page index sur laquelle vous avez lié votre feuille de style, elle est tout de même considérer comme une autre page. N'oubliez donc pas de lier votre feuille de style dans header/footer aussi. Pour ce faire, vous pouvez utiliser la fonction @importde CSS pour importer votre feuille de style dans la feuille de style de header/footer.

@import "style.css";
Le background-color de body
Il est également possible que votre header/footer s'affiche en prenant en compte le background-color définit dans votre feuille de style principale et du coup vous aurez un gros bloc de cette couleur qui se place par dessus certains éléments sur votre page. Pour ce faire précisez dans la feuille de style de header/footer que le background-color doit être transparent. body{background-color: transparent;}

Les liens
Si vous avez des liens dans votre header/footer, ceux-ci vont s'ouvrir dans votre iframe par défaut. Pour changer cela il faut ajouter un attribut target:_top à vos liens.

Exemple d'utilisation
index.html

<head>
  <title>Soundwave</title>
  <link rel="stylesheet" href="./css/style.css">
</head>
<body>
  <iframe src="header.html" seamless></iframe>
  <main>
    <img src="./assets/Girl.png" alt="girl" class="girl">
  </main>
</body>
header.html

<link rel="stylesheet" href="./css/header.css">
<header>
  <div class="title">
    <a href="index.html" target="_top">
      <img src="./assets/Logo.png" alt="logo">
      <span>Soundwave</span>
    </a>
  </div>
  <nav>
    <a class="nav" href="discover.html" target="_top">Discover</a>
    <a class="nav" href="comments.html" target="_top">Comments</a>
  </nav>
</header>
header.css

@import "style.css";

body{
  background-color: transparent;
}