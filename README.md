# Chapitre 1 : Conception d\'un site web {#ref-chapitre1}

Ce premier chapitre a pour but d\'introduire l\'histoire du web, le
fonctionnement du HTML et le framework python Flask.

Le \"`ref-chapitre2`{.interpreted-text role="ref"}\" contient un
tutoriel Flask qui sera l\'objet de la première séance de travaux
pratique.

::: toctree
00_web/01_web.rst 00_web/02_html.rst 00_web/03_flask.rst
00_web/04_mvc.rst
:::


# Le world wide web (www) {#ref-web}

Inventé durant les années 1990s par les physiciens du [Centre Européen
de Recherche Nucléaire (CERN)](https://www.cern.ch) à Genève, le [world
wide web (www)](https://cds.cern.ch/record/245440/files/p69.pdf) est
petit à petit devenu une des composante fondamentale de la société de
l\'information que nous connaissons aujourd\'hui. A l\'origine, le
[www]{.title-ref} a été conçu de façon à faciliter le partage de
documents scientifiques. Dans un document scientifique, il est très
courant de citer d\'autres documents que ce soit via des notes de bas de
pages ou des citations dans une bibliographie reprise à la fin du
document. Les inventeurs du web ont voulu faciliter l\'accès à ces
documents en les structurant comme des
[hypertextes](https://fr.wikipedia.org/wiki/Hypertexte).

L\'idée d\'un document hypertexte est plus ancienne puisqu\'elle remonte
aux années soixante avec le projet
[Xanadu](https://fr.wikipedia.org/wiki/Projet_Xanadu). Un document
hypertexte est un document qui contient des références vers un autre
document. Dans un hypertexte, ces références sont telles que le lecteur
peut aisément passer d\'un document à sa référence par un simple clic de
souris. Les premiers hypertextes étaient stockés sur un ordinateur isolé
et nécessitaient l\'utilisation de logiciels spécifiques pour les
visualiser. Avant l\'invention du web, le logiciel
[Hypercard](https://fr.wikipedia.org/wiki/HyperCard) disponible sur les
premiers Mac de chez Apple était un des rares hypertextes à être connus
du grand public. L\'invention du web a permis de construire des
documents hypertextes qui sont stockés sur des ordinateurs différents et
même des documents qui combinent des parties de documents stockées sur
différents ordinateurs.

Les détails du fonctionnement du [www]{.title-ref} sortent du cadre de
ce cours et seront abordés dans le cours de [réseaux
informatiques](https://www.computer-networking.info) en troisième année
de bachelier. Dans le cadre de ce projet, nous nous limiterons au base
de fonctionnement du web. Le web repose sur trois éléments principaux:

> -   un langage (HTML) permettant de décrire des pages d\'hypertextes
> -   un protocole (HTTP) permettant à un navigateur web de charger un
>     document HTML depuis un ou plusieurs serveurs web
> -   un mécanisme (URL) permettant d\'identifier de façon non-ambiguë
>     un document web

Ces trois éléments sont supportés par les
[navigateurs](https://fr.wikipedia.org/wiki/Navigateur_web) et [serveurs
web](https://fr.wikipedia.org/wiki/Serveur_web). Ceux-ci jouent un rôle
important dans l\'évolution du web et le web n\'aurait pas eu le succès
qu\'il a aujourd\'hui sans l\'existence de navigateurs et de serveurs
efficaces. Le CERN a développé le premier navigateur textuel et le
premier serveur. Ces deux logiciels étant open-source, ils ont servis de
base au développement des autres navigateurs et serveurs web. Le
navigateur [Mosaic](https://fr.wikipedia.org/wiki/NCSA_Mosaic),
développé par le National Center for Supercomputing Applications (NCSA)
a été le premier navigateur graphique capable d\'intégrer des images
dans les documents.
[Netscape](https://fr.wikipedia.org/wiki/Netscape_Communications), créé
par l\'équipe qui avait lancé Mosaic, a été le premier navigateur
commercial. C\'est Netscape qui a été la première société à proposer des
solutions pour sécuriser le commerce électronique. Quelques uns des
principaux navigateurs web actuels sont Firefox de Mozilla, Safari chez
Apple et Chrome développé par Google. Chromium, le coeur de Chrome est
open-source et Microsoft a récemment lancé Edge, un nouveau navigateur
basé sur Chromium. Chromium est utilisé par d\'autres navigateurs tels
que Brave. Côté serveurs, le premier serveur développé par le CERN a été
petit à petit amélioré par de nombreux développeurs qui diffusaient
leurs modifications sous forme de [patches]{.title-ref}. Après quelques
temps, un groupe de développeurs a décidé de regrouper les patches les
plus populaires dans un nouveau projet baptisé
[Apache](http://httpd.apache.org/), dont le nom reste fort proche du mot
[patches]{.title-ref}. Il reste aujourd\'hui un serveur web très
populaire avec d\'autres dont [nginx](https://nginx.org/) par exemple.

Sur le réseau Internet, un serveur est identifié par un nom et une
adresse IP. Le nom est important pour l\'utilisateur car c\'est celui
qu\'il utilise dans son navigateur web pour contacter un serveur.
L\'adresse IP est utilisée par les ordinateurs pour s\'échanger de
l\'information. Il existe un service (le Domain Name System - DNS) qui
permet d\'obtenir l\'adresse IP qui correspond à un nom de machine, mais
nous n\'entrerons pas dans ces détails dans le cadre de ce projet.

Il y a aujourd\'hui deux types d\'adresses sur Internet:

> -   les adresses IP version 4 sur 32 bits. Celles-ci sont généralement
>     représentées sous la forme de quatre entiers séparés par le
>     caractère `.` Ainsi `193.191.245.244` est l\'adresse IP version 4
>     qui correspond au nom `www.belgium.be`
> -   les adresses IP version 6 sur 128 bits. Celles-ci sont
>     généralement représentées sous la forme d\'une suite de nombres en
>     notations hexadécimale séparés par le caractère `:` Ainsi,
>     `2a01:690:35:100::f5:f4` est l\'adresse IP version 6 qui
>     correspond au nom `www.belgium.be`

Au niveau des noms de machine, les informaticiens ont l\'habitude de
donner des noms qui sont liés au service rendu par un service donné.
Ainsi, dans une petite entreprise, il sera fréquent d\'utiliser le nom
`print` pour le serveur d\'impressions et `www` pour le serveur web de
l\'entreprise. De nombreuses entreprises ont choisi d\'adopter ces
conventions. Si leurs réseaux sont isolés, le PC de l\'entreprise A ne
pourra rejoindre qu\'un seul serveur baptisé `www`. Si par contre toutes
ces entreprises sont connectées à l\'Internet, il faut absolument que
l\'on évite d\'associer le même nom à plusieurs serveurs.

La façon standard de s\'assurer de l\'unicité des noms de machine sur
Internet est de construire ces noms de machine de façon hiérarchique. En
simplifiant, un nom de machine sur Internet est composé de deux parties:

> -   le nom de la machine qui n\'est pas nécessairement unique
> -   le nom du domaine dans lequel la machine se trouve qui lui est
>     unique

Le nom complet d\'une machine est la concaténation entre le nom de la
machine et le domaine dans lequel la machine se trouve. Les noms de
domaine sont attribués de façon hiérarchique. Chaque pays dispose d\'un
nom de domaine en deux lettres (`be` pour la Belgique, `fr` pour la
France, \...). Quand une entreprise belge veut obtenir un nom de
domaine, elle contacte le secrétariat qui gère le domaine `.be`.
Celui-ci vérifie si le nom demandé par l\'entreprise est déjà utilisé et
si non, il est réservé pour l\'entreprise qui peut l\'utiliser comme nom
de domaine.

Les noms de domaine jouent un rôle clé dans la définition des Uniform
Ressource Locators (URL). Une URL est une sorte d\'adresse pour un
document accessible sur un serveur web. Tout document accessible via un
serveur web est identifié par son URL. Une URL est une chaîne de
caractères qui est composée de différentes parties:

> -   un identifiant de protocole permettant de télécharger le document
>     suivi de `://`
> -   un nom de domaine suivi du caractère `/`
> -   un nom de fichier

Le web supporte différents identifiants de protocoles. Les plus utilisés
sont `http` et `https`. Dans le cadre de ce projet, nous utiliserons
`http`. La plupart des serveurs Internet utilisent `https` qui est la
version sécurisée de `http`. La distinction entre ces deux protocoles
sort du cadre de ce projet.

Prenons quelques exemples pour comprendre d\'utilisation des URLs. Nous
verrons qu\'ils jouent un rôle important dans le langage HTML également.
Commençons par le site web de l\'UCLouvain. Celui-ci est accessible en
français et en anglais. La version française utilise l\'URL
`https://uclouvain.be/fr/index.html` tandis que la version anglaise est
accessible via `https://uclouvain.be/en/index.html`. L\'URL de la page
en français indique que celle-ci peut être chargée en contactant le
serveur `uclouvain.be` en utilisant le protocole `https`. Sur ce
serveur, le document demandé est `/fr/index.html`. Ce document
correspond au fichier dénommé `index.html` dans le répertoire `fr`. Sur
le même site, l\'URL `https://uclouvain.be/fr/etudier/bacheliers.html`
correspond à la page consacrée aux études de bachelier. Celle-ci est
dans le fichier `bachelier.html` qui se trouve dans le sous-répertoire
`etudier` du répertoire `fr`.

La structuration d\'un site web en répertoires et sous-répertoires est
très fréquente. Nous verrons qu\'elle sera utile lors de la création de
pages en format HTML et aussi lorsque vous utiliserez Flask pour créer
votre site web interactif.

Continuez votre lecture avec le document `ref-html`{.interpreted-text
role="ref"}.


# Le langage HTML {#ref-html}

L\'HyperText Markup Language (HTML) est un langage de description de
documents qui s\'appuie sur un ensemble de balises
([markups]{.title-ref} en anglais). Il s\'agit du langage de référence
pour décrire les pages web consultables via un navigateur. Il existe de
nombreux livres et sites web qui fournissent de très nombreux détails
sur HTML. Les sites
[https://www.w3schools.com/](https://www.w3schools.com/../html/) et
<https://developer.mozilla.org/en-US/docs/Web/HTML> proposent de
nombreuses ressources concernant HTML et les technologies web.

Dans le cadre de ce projet, nous nous concentrerons sur un sous-ensemble
de la version 5 du langage HTML (HTML5). Libre à vous d\'explorer le web
et les bibliothèques pour utiliser d\'autres fonctionnalités de ce
langage. Il est très important pour un informaticien de pouvoir
apprendre de façon autonome en s\'aidant des multiples ressources
disponibles[^1].

Un document HTML est composé de deux parties : l\'entête
([head]{.title-ref} en anglais) et le corps ([body]{.title-ref} en
anglais). L\'entête contient des informations telles que le titre de la
page qui sera affiché en haut de la fenêtre du navigateur, mais aussi le
type de codage des caractères utilisé (typiquement UTF-8), \... Le corps
de la page contient lui le document en hypertexte.

Tout document HTML commence par la chaîne de caractères
`<!DOCTYPE html>`. Cette chaîne est suivie par la première balise
(ouvrante) : [\<html\>]{.title-ref}. Dans l\'exemple ci-dessous, tout le
texte se trouvant entre la balise ouvrante, [\<html\>]{.title-ref}, et
la balise fermante, [\</html\>]{.title-ref} est du HTML. Si un document
HTML contient la balise ouvrante [\<xyz\>]{.title-ref} il doit y avoir
une balise fermante [\</xyz\>]{.title-ref} plus loin qui délimite la
zone de texte couverte par cette balise. C\'est un peu comme des
parenthèses dans une expression mathématique. Il y a toujours une
parenthèse fermante qui correspond à une parenthèse ouvrante.

L\'entête du document HTML ci-dessous est la zone du fichier se trouvant
entre les balises [\<head\>]{.title-ref} et [\</head\>]{.title-ref}.
Celle-ci ne contient que le titre de la page que l\'on reconnaît grâce à
l\'utilisation de la balise [\<title\>]{.title-ref} et une indication
sur le codage des caractères utilisé dans le document.

::: {.literalinclude language="html"}
/figures/html/html-simple.html
:::

<figure>
<img src="/figures/html/html-simple.png"
alt="/figures/html/html-simple.png" />
<figcaption>Une page HTML simple</figcaption>
</figure>

Le corps du document HTML ci-dessus est le texte se trouvant entre les
balises [\<body\>]{.title-ref} et [\</body\>]{.title-ref}. Ce texte
comprend deux sous-sections contenant chacune un paragraphe. La balise
[\<h1\>]{.title-ref} correspond à un titre de section de premier niveau
([\<h2\>]{.title-ref} pour une sous-section, c\'est-à-dire un titre de
deuxième niveau, \...). La balise [\<p\>]{.title-ref} sert à identifier
un paragraphe.

HTML5 définit de nombreuses balises qui ne peuvent pas toutes être
détaillées dans le cadre de cette brève introduction. Outre les balises
telles que [\<h1\>]{.title-ref} qui définissent des niveaux de titre, il
existe des balises qui permettent de modifier le style utilisé pour
présenter certains mots à l\'écran, dont :

> -   [\<b\>]{.title-ref} qui est utilisé pour indiquer que du texte
>     doit être écrit en gras. [\<strong\>]{.title-ref} est un synonyme
>     sur de nombreux navigateurs.
> -   [\<i\>]{.title-ref} qui est utilisé pour indiquer que du texte
>     doit être écrit en italique. [\<em\>]{.title-ref} est un synonyme
>     sur de nombreux navigateurs.
> -   [\<sub\>]{.title-ref} qui indique que du texte doit être mis en
>     indice
> -   [\<sup\>]{.title-ref} qui indique que du texte doit être mis en
>     exposant
> -   [\<mark\>]{.title-ref} qui indique que du texte doit être surligné

Certaines balises sont liées à la présentation des paragraphes. Comme
indiqué précédemment, un paragraphe débute toujours par
[\<p\>]{.title-ref} et se termine par [\</p\>]{.title-ref}. Celui-ci
peut contenir de nombreuses lignes de textes. Le navigateur se chargera
de mettre en forme le paragraphe correctement entre les balises
[\<p\>]{.title-ref} et [\</p\>]{.title-ref}. Parfois, l\'auteur d\'une
page HTML peut souhaiter forcer un retour à la ligne à un endroit
particulier d\'un paragraphe. Cela peut se faire en utilisant la balise
ouvrante [\<br\>]{.title-ref}. Cette balise force le navigateur à aller
directement à la ligne. C\'est une des rares balises HTML à ne pas avoir
de balise fermante.

Dans certains cas, notamment pour présenter du code dans un langage de
programmation à l\'intérieur d\'une page HTML, il est préférable que le
navigateur présente le texte tel qu\'il a été écrit dans le fichier et
sans rajouter d\'espaces ou de retours à la ligne. Cela se fait en
utilisant les balises [\<pre\>]{.title-ref} et [\</pre\>]{.title-ref}.
Le texte se trouvant entre ces deux balises sera alors affiché tel quel
en utilisant une police avec espacement fixe entre les caractères alors
que la police standard est généralement avec espacement proportionnel.

Lorsque l\'on écrit des pages HTML dans un éditeur de textes, il est
parfois utile d\'ajouter des commentaires. Par convention, dans un
document HTML, un commentaire s\'écrit à l\'intérieur d\'une balise
[\<!\-- \... \--\>]{.title-ref}. Il faut noter que la fin du commentaire
ne comprend pas de caractère [/]{.title-ref} contrairement aux balises
fermantes habituelles. Un commentaire peut être placé sur une ligne ou
couvrir plusieurs lignes, comme les commentaires dans les langages de
programmation.

::: {.literalinclude language="html"}
/figures/html/html-comment.html
:::

<figure>
<img src="/figures/html/html-comment.png"
alt="/figures/html/html-comment.png" />
<figcaption>Une page HTML simple avec des commentaires</figcaption>
</figure>

Comme le langage HTML utilise les caractères [\<]{.title-ref} et
[\>]{.title-ref} dans la définition des balises, comment peut-on
afficher ces caractères dans un document HTML ? Il n\'est pas possible
de simplement utiliser ces caractères puisqu\'ils sont interprétés par
HTML comme des débuts de balises. Pour résoudre ce problème, HTML
définit les entités caractères suivantes:

> -   [&lt;]{.title-ref} pour représenter le caractère [\<]{.title-ref}
>     dans du texte
> -   [&gt;]{.title-ref} pour représenter le caractère [\>]{.title-ref}
>     dans du texte
> -   [&amp;]{.title-ref} pour représenter le caractère [&]{.title-ref}
>     dans du texte
> -   [&nbsp;]{.title-ref} pour indiquer un espace insécable
> -   [&quot;]{.title-ref} pour le caractère correspondant aux
>     guillemets ([\"]{.title-ref})
> -   [&apos;]{.title-ref} pour le caractère correspondant à
>     l\'apostrophe ([\']{.title-ref})

Ainsi, dans une page HTML, il est possible d\'expliquer en HTML le
format d\'un commentaire en HTML.

::: {.literalinclude language="html"}
/figures/html/html-comment2.html
:::

<figure>
<img src="/figures/html/html-comment2.png"
alt="/figures/html/html-comment2.png" />
<figcaption>Une page HTML montrant comment écrire un commentaire en
HTML</figcaption>
</figure>

De nombreuses balises HTML supportent des attributs qui permettent de
préciser certains paramètres de chacune d\'entre elles. Il est
impossible de les lister toutes dans ce document. En voici quelques-uns
qui pourraient être utiles dans le cadre de ce projet.

La balise [\<html\>]{.title-ref} supporte l\'attribut [lang]{.title-ref}
qui permet d\'indiquer la langue dans laquelle la page a été écrite.
Ainsi [\<html lang=\"fr\"\>]{.title-ref} est la balise ouvrante d\'un
document écrit en français tandis que [\<html lang=\"en\"\>]{.title-ref}
est celle d\'un document en anglais.

La balise [\<meta\>]{.title-ref} que l\'on retrouve dans l\'entête d\'un
document HTML supporte différents attributs. Le plus important est le
type de code de caractères utilisé pour écrire le document.
Aujourd\'hui, le codage le plus répandu est
l\'[UTF-8](https://fr.wikipedia.org/wiki/UTF-8) qui fait partie du
standard [Unicode](https://fr.wikipedia.org/wiki/Unicode). Parmi les
autres attributs, on peut citer :

> -   l\'attribut [description]{.title-ref} qui fournit une information
>     sur le contenu de la page
> -   l\'attribut [keywords]{.title-ref} qui indique les mots-clés et
>     est lu par certains moteurs de recherche
> -   l\'attribut [author]{.title-ref} qui indique l\'auteur de la page

``` html
<head>
  <meta charset="UTF-8">
  <meta name="description" content="Une première page web">
  <meta name="keywords" content="HTML,exemple">
  <meta name="author" content="Jean Tartempion">
</head>
```

Les attributs des balises HTML nous permettent d\'aborder deux éléments
clés des pages HTML :

> -   les liens hypertextes
> -   les images

En HTML, un lien hypertexte s\'écrit en utilisant la balise
[\<a\>\...\</a\>]{.title-ref} pour ancre ([anchor]{.title-ref} en
anglais) et en utilisant l\'attribut [href]{.title-ref} pour indiquer
l\'URL du lien hypertexte. Ainsi dans un document HTML, un lien qui
pointe vers le site web de l\'UCLouvain s\'écrit comme suit :

::: {.literalinclude language="html"}
/figures/html/html-a.html
:::

<figure>
<img src="/figures/html/html-a.png" alt="/figures/html/html-a.png" />
<figcaption>Une autre page HTML contenant un lien
hypertexte</figcaption>
</figure>

Grâce à la balise [\<img\>]{.title-ref}, il est possible d\'inclure une
image à n\'importe quel endroit d\'une page HTML. Cette balise supporte
plusieurs attributs :

> -   [src]{.title-ref} : permet d\'indiquer l\'URL du fichier contenant
>     l\'image à inclure. Celui-ci peut être absolu ou relatif. La
>     plupart des navigateurs supportent les fichiers aux formats
>     [png]{.title-ref}, [jpg]{.title-ref} ou [svg]{.title-ref}.
> -   [alt]{.title-ref} : (optionnel) permet d\'indiquer une description
>     textuelle de l\'image pour les navigateurs non-graphiques. Ce
>     texte est en général rajouté par souci d\'inclusivité, car il être
>     automatiquement lu à voix haute par les navigateurs utilisés par
>     les malvoyants.
> -   [width]{.title-ref} : (optionnel) permet d\'indiquer la largeur de
>     l\'image en pixels. Par défaut le navigateur prendra la largeur de
>     l\'image d\'origine
> -   [height]{.title-ref} : (optionnel) permet d\'indiquer la hauteur
>     de l\'image en pixels. Par défaut le navigateur prendra la hauteur
>     de l\'image d\'origine

Dans le document HTML, l\'attribut [src]{.title-ref} d\'une image peut
correspondre à un fichier se trouvant dans le même répertoire que le
document HTML, un fichier présent dans un autre répertoire du même
serveur ou sur un autre serveur. En pratique, les designers de sites web
regroupent souvent leurs images dans un ou quelques répertoires ou
utilisent des serveurs dédiés pour les sites utilisant de très
nombreuses images. Pour un petit site, le plus simple est de regrouper
toutes les images du site dans un répertoire nommé par exemple
[/images]{.title-ref}.

::: {.literalinclude language="html"}
/figures/html/html-img.html
:::

<figure>
<img src="/figures/html/html-img.png"
alt="/figures/html/html-img.png" />
<figcaption>Une page HTML contenant des images</figcaption>
</figure>

Dans un article scientifique, les figures sont généralement accompagnées
d\'une légende. C\'est aussi possible en HTML avec les balises
[\<figure\>]{.title-ref} et [\<figcaption\>]{.title-ref}.

``` html
<figure>
 <img src="/images/mesures.jpg" alt="Mesures récentes" width="500" height="600">
 <figcaption>Les mesures collectées ce matin</figcaption>
</figure>
```

HTML permet également d\'afficher des listes ordonnées ou non. Les
listes ordonnées utilisent la balise [\<ol\>]{.title-ref} tandis les
non-ordonnées utilisent la balise [\<ul\>]{.title-ref}. Ces deux balises
supportent différents attributs. Pour la liste non ordonnée, l\'attribut
[list-style-type]{.title-ref} indique le type de marqueur d\'élément.
Par défaut c\'est un point, mais il est possible d\'utiliser un cercle
(attribut [circle]{.title-ref}), un carré (attribut
[square]{.title-ref}), \...

::: {.literalinclude language="html"}
/figures/html/html-li.html
:::

<figure>
<img src="/figures/html/html-li.png" alt="/figures/html/html-li.png" />
<figcaption>Une page HTML contenant une liste non numérotée</figcaption>
</figure>

Les listes ordonnées supportent elles l\'attribut [type]{.title-ref} qui
permet de spécifier le type de numérotation des éléments. Par défaut
c\'est la numérotation entière qui est utilisée, mais HTML supporte
aussi l\'utilisation de lettres majuscules (attribut
[type=\"A\"]{.title-ref}), minuscules (attribut
[type=\"a\"]{.title-ref}) ou en chiffres romains (attribut
[type=\"I\"]{.title-ref}).

::: {.literalinclude language="html"}
/figures/html/html-ol.html
:::

<figure>
<img src="/figures/html/html-ol.png" alt="/figures/html/html-ol.png" />
<figcaption>Une page HTML contenant une liste ordonnée</figcaption>
</figure>

Outre les listes, il est aussi possible de présenter des informations
sous la forme de tables. Les tables utilisent quatre types de balises.
La balise [\<table\>]{.title-ref} marque le début d\'une table. À
l\'intérieur d\'une table, la balise [\<tr\>]{.title-ref} est utilisée
pour représenter une ligne ([table row]{.title-ref} en anglais). La
balise [\<th\>]{.title-ref} est utilisée pour un nom ou une entête de
colonne ([table header]{.title-ref} en anglais) et enfin la balise
[\<td\>]{.title-ref} entoure une donnée dans une cellule de la table.

::: {.literalinclude language="html"}
/figures/html/html-table.html
:::

<figure>
<img src="/figures/html/html-table.png"
alt="/figures/html/html-table.png" />
<figcaption>Une page HTML contenant une table</figcaption>
</figure>

Il est possible en utilisant les attributs de ces balises de contrôler
finement la façon dont les données sont présentées dans une table. Vous
trouverez plus d\'informations à ce sujet dans les références
mentionnées au début du chapitre.

Il existe de très nombreux autres attributs en HTML5. L\'attribut
[style]{.title-ref} permet contrôler la couleur, la police utilisée pour
afficher du texte et sa taille ou l\'alignement du texte. Voici un
exemple simple.

``` html
<h1 style="font-family:courrier;">Une entête en police courrier</h1>
<p style="color:blue;text-align:center;">Ce paragraphe est écrit en couleur bleue et centré.</p>
```

Il est aussi possible de contrôler la couleur du fond
([background-color]{.title-ref}) et la taille de la police
([font-size]{.title-ref}). HTML5 supporte de très nombreuses couleurs.
Les plus courantes sont identifiées par un nom. Voir
<https://www.w3schools.com/colors/colors_names.asp> pour plus de
détails. Il est aussi possible de préciser la couleur demandée sur base
de ses composantes rouge, verte et bleue. Cela permet à HTML de
supporter toutes les couleurs imaginables.

Même si HTML est principalement utilisé pour présenter de
l\'information, il est parfois nécessaire sur un site web de demander à
l\'utilisateur d\'envoyer de l\'information. En HTML, cela se fait en
utilisant un formulaire qui est délimité par les balises
[\<form\>]{.title-ref} et [\</form\>]{.title-ref}. Un formulaire est
composé de plusieurs éléments. Le plus important est l\'élément
[\<input\>]{.title-ref}. Cet élément supporte différents attributs de
type. Par exemple, un élément [\<input type=\"text\"\>]{.title-ref}
permettra de définir une zone d\'une ligne de texte dans un formulaire.
un élément [\<input type=\"button\"\>]{.title-ref} permettra de
spécifier un bouton, un élément [\<input type=\"date\"\>]{.title-ref}
sera utilisé pour demander une date, \... Enfin, l\'élément [\<input
type=\"submit\"\>]{.title-ref} sera utilisé pour envoyer toutes les
informations d\'un formulaire au serveur.

L\'intérêt d\'un formulaire est de permettre à l\'utilisateur de saisir
dans la page HTML courante de l\'information qui sera ensuite envoyée au
serveur. Grâce aux éléments du formulaire, il est possible de déterminer
différents types de champ qui peuvent être remplis par l\'utilisateur.
Chacun de ces champs est identifié par un nom ([name]{.title-ref} en
anglais) et celui-ci est envoyé au serveur avec la valeur encodée par
l\'utilisateur lorsque celui-ci clique sur [Submit]{.title-ref}. Les
noms de ces champs doivent être uniques dans un formulaire pour
permettre au serveur de déterminer à quel champ correspond chaque valeur
reçue.

::: {.literalinclude language="html"}
/figures/html/html-form.html
:::

<figure>
<img src="/figures/html/html-form.png"
alt="/figures/html/html-form.png" />
<figcaption>Une page HTML contenant un formulaire</figcaption>
</figure>

Le formulaire ci-dessous demande à l\'utilisateur de saisir son nom et
son prénom. Ces deux informations sont saisies dans une zone
[text]{.title-ref}. Chacune de ces zones de texte est associée à un nom
([name]{.title-ref}) et un identifiant ([id]{.title-ref}). L\'attribut
[name]{.title-ref} est transmis avec la donnée saisie au serveur web.
L\'identifiant lui peut être utilisé par du Javascript qui serait
associé à ce formulaire. Cette utilisation sort du cadre de ce projet,
mais sachez que vous devez spécifier ces noms et identifiants. Les
étiquettes (balises [\<label\>]{.title-ref} utilisent l\'attribut
[for]{.title-ref} pour spécifier à quelle zone de l\'élément
[input]{.title-ref} elles sont associées. Enfin, l\'attribut
[method=post]{.title-ref} associé à l\'élément [\<form\>]{.title-ref}
indique que le contenu du formulaire sera envoyé au serveur en utilisant
une requête POST. Si cet attribut n\'est pas spécifié, c\'est une
requête GET qui est utilisée.

## Les feuilles de style

Lorsque l\'on développe quelques pages HTML manuellement, il est
possible d\'indiquer les attributs tels que la couleur des caractères ou
la police à utiliser directement dans chaque page HTML. Malheureusement,
c\'est assez fastidieux et il est difficile de garder une cohérence
entre la présentation des différentes pages d\'un même site web.
Lorsqu\'un site web est géré par un logiciel et est susceptible
d\'afficher de nombreuses pages HTML, il est préférable d\'utiliser des
feuilles de style ou Cascading Style Sheets (CSS). Une feuille de style
est un ensemble cohérent de règles que le navigateur va appliquer à la
mise en page d\'un document HTML. Elle peut être incluse directement
dans l\'entête de chaque page HTML ou référencée dans cette entête. La
seconde solution est préférable. Cela permet à avoir une même feuille de
style, chargée une seule fois par le navigateur, pour toutes les pages
d\'un site web. C\'est la solution que nous vous encourageons à adopter
et donc la seule que nous décrivons dans ces notes.

Une feuille de style indique comment la page sera présentée globalement
(police de caractères, couleur de fond d\'écran, \...) mais surtout les
particularités de chaque élément de la page seront présentées. Dans une
feuille de style CSS, il est possible de modifier la présentation des
entêtes d\'un niveau particulier, des paragraphes, des tables, \... Une
feuille style CSS permet d\'appliquer une série d\'attributs à des
éléments d\'un type particulier. La syntaxe générale d\'une feuille de
style CSS est :

``` css
/* commentaire sur une ligne */      
selecteur1 {
  proprieteA: valeurA;
  proprieteB: valeurB;
  /* ... */
}
/*
 * Commentaire
 * sur plusieurs lignes
 */
selecteur2 {
  proprieteX: valeurX;
  proprieteY: valeurY;
  /* ... */
}
```

Dans une telle feuille de style, le sélecteur correspond à un type
d\'élément se trouvant dans le document HTML. L\'élément
[body]{.title-ref} correspond à l\'ensemble du corps de la page HTML.
L\'élément [p]{.title-ref} correspond à un paragraphe tandis que
l\'élément [h1]{.title-ref} à un titre de premier niveau. Dans une
feuille CSS, la balise [/\*]{.title-ref} marque le début d\'un
commentaire. La balise [\*/]{.title-ref} marque la fin d\'un
commentaire.

::: {.literalinclude language="html"}
/figures/html/html-simple-css.html
:::

::: {.literalinclude language="html"}
/figures/html//simple.css
:::

<figure>
<img src="/figures/html/html-simple-css.png"
alt="/figures/html/html-simple-css.png" />
<figcaption>Une page HTML utilisant une feuille de style
simple</figcaption>
</figure>

La puissance de CSS dans HTML5 vient du fait qu\'il est possible
d\'appliquer ces attributs à des parties de texte qui ont étés
préalablement marqués par l\'auteur du document. Prenons comme exemple
une application web qui doit afficher une liste de lieux et une liste de
mesures de températures minimales et maximales. Supposons que le nom du
lieu doive s\'afficher en bleu et les températures en vert. Sans les
styles, une telle page en HTML pourrait s\'écrire comme suit :

::: {.literalinclude language="html"}
/figures/html/html-simple-nocss.html
:::

<figure>
<img src="/figures/html/html-simple-nocss.png"
alt="/figures/html/html-simple-nocss.png" />
<figcaption>Une page HTML sans feuille de style mais avec des
couleurs</figcaption>
</figure>

Avec une feuille de style, il est plus simple d\'identifier d\'abord
chaque type d\'élément. Cela peut se faire en utilisant l\'attribut
[class]{.title-ref} qui permet d\'identifier des sous-types d\'un même
type.

::: {.literalinclude language="html"}
/figures/html/html-simple-css2.html
:::

L\'attribut [class]{.title-ref} de chaque élément [\<li\>]{.title-ref}
n\'est pas directement affiché par le navigateur, mais il est utilisé
par le CSS ci-dessous.

::: {.literalinclude language="html"}
/figures/html//simple2.css
:::

Et le résultat apparaît comme prévu.

<figure>
<img src="/figures/html/html-simple-css2.png"
alt="/figures/html/html-simple-css2.png" />
<figcaption>Une page HTML utilisant une feuille de style</figcaption>
</figure>

L\'avantage de cette approche est que si on veut remplacer la couleur
verte par de l\'orange pour les températures, il suffira de modifier une
seule ligne dans le fichier CSS et toutes les pages du site web seront
automatiquement adaptées.

Grâce à l\'attribut [class]{.title-ref} des éléments HTML5, il est
possible d\'identifier différents types de paragraphes, de listes ou de
tables qui auront une mise en page différente en fonction de leur
contenu. Lorsque ces éléments sont générés par des programmes, il est
facile de leur associer la bonne classe directement. Il est possible
d\'aller plus loin en utilisant les balises [\<div\>]{.title-ref} et
[\<span\>]{.title-ref}. Ces deux balises sont génériques. Elles
permettent de regrouper des zones d\'un document HTML5. La balise
[\<div\>]{.title-ref} s\'utilise pour regrouper une zone qui contient
d\'autres éléments HTML5. La balise [\<span\>]{.title-ref} s\'utilise
plutôt autour d\'une petite zone de texte. Ces deux balises peuvent
contenir un attribut [class]{.title-ref}.

Notre premier exemple utilise la balise [\<div\>]{.title-ref} pour
entourer un article concernant une ville qui est composé d\'une entête
de section et d\'un paragraphe.

::: {.literalinclude language="html"}
/figures/html/html-simple-css-div.html
:::

La feuille de style associée.

::: {.literalinclude language="css"}
/figures/html//simple-div.css
:::

Et le résultat apparaît comme prévu.

<figure>
<img src="/figures/html/html-simple-css-div.png"
alt="/figures/html/html-simple-css-div.png" />
<figcaption>Une page HTML utilisant une feuille de style et la balise
<span class="title-ref">&lt;div&gt;</span></figcaption>
</figure>

Notre second exemple utilise la balise [\<span\>]{.title-ref} pour
afficher avec une couleur différente les températures minimale et
maximale mesurées dans une ville.

::: {.literalinclude language="html"}
/figures/html/html-simple-css-span.html
:::

La feuille de style associée.

::: {.literalinclude language="css"}
/figures/html//simple-span.css
:::

Et le résultat apparaît comme prévu.

![](/figures/html/html-simple-css-span.png)

L\'attribut [class]{.title-ref} et les balises [\<div\>]{.title-ref} et
[\<span\>]{.title-ref} sont très utiles lorsque l\'on veut produire avec
un programme des pages HTML qui auront la même mise en page. Pensez à
les utiliser à bon escient dans le cadre de votre projet.

Continuez votre lecture avec le document `ref-flask`{.interpreted-text
role="ref"}.

[^1]: En cas de doute, la spécification officielle et complète de HTML5
    est accessible en ligne via
    <https:/html.spec.whatwg.org/multipage/>. Ce n\'est pas un document
    conçu pour aider les débutants.
    
    
# Le framework flask {#ref-flask}

Il existe de nombreuses librairies qui permettent de faciliter
l\'écriture de sites web interactifs en Python:
[Django](https://www.djangoproject.com/), [Webpy](https://webpy.org/) ou
[flask](https://palletsprojects.com/p/flask/). Dans le cadre de ce
projet, nous avons choisi [flask](https://palletsprojects.com/p/flask/)
qui a l\'avantage d\'être simple à apprendre tout en pouvant profiter de
la puissance de python, un langage qui vous est déjà familier.

## Les sites statiques

Les premiers sites web étaient composés de pages HTML stockées dans des
fichiers se trouvant dans un même répertoire. Le serveur web était alors
simplement configuré pour servir tous les fichiers de ce répertoire.
C\'est ce que l\'on appelle communément un site web statique,
c\'est-à-dire un site web composé de pages HTML qui ne changent pas. Ces
sites web statiques sont intéressants pour du contenu tel que ce
syllabus qui ne change que rarement. La plupart des sites web actuels
sont dynamiques. Un programme reçoit les requêtes des utilisateurs et y
répond en générant si nécessaire les pages HTML correspondantes à la
volée. Flask permet de construire un tel site web assez facilement en
python.

Avant de se lancer dans l\'écriture d\'un site web dynamique en Flask,
il faut se rappeler que sur le web, toute page est identifiée par son
Uniform Resource Locator (URL). Quand un utilisateur interagit avec un
site web à travers son navigateur, celui-ci charge différentes pages en
utilisant l\'HyperText Transport Protocol (HTTP). Le fonctionnement
détaillé de HTTP sort du cadre de ce cours, mais vous devez savoir
qu\'un navigateur peut utiliser HTTP de deux façons différentes.

La première est d\'envoyer une requête GET HTTP pour un URL particulier.
Le serveur web répond à cette requête en renvoyant au navigateur la page
HTML correspondant à l\'URL demandée. L\'immense majorité des requêtes
qu\'un navigateur fait à un serveur web sont des GET HTTP.

À côté de ces requêtes GET HTTP, un navigateur peut aussi utiliser des
requêtes POST HTTP. Une telle requête n\'est utilisée que lorsque le
navigateur veut envoyer de l\'information autre qu\'un URL au serveur.
C\'est par exemple le cas lorsque l\'utilisateur remplit un formulaire
sur une page web.

Dans un site web purement statique, le serveur web supporte uniquement
les requêtes GET HTTP. Pour chaque URL demandée, il analyse la partie
fichier de cette URL et si le fichier existe retourne son contenu et
sinon une erreur. Pour illustrer cela, considérons que le serveur web
est configuré pour servir le répertoire ci-dessous. Celui-ci contient
deux fichiers et deux sous-répertoires.

``` console
index.html
page.html
css
images
```

Le répertoire `css` contient le fichier `style.css` qui est référencé
par les deux pages HTML. Le répertoire `images` contient le fichier
`logo.png`.

Le fichier [index.html]{.title-ref} contient la page reprise ci-dessous.

::: {.literalinclude language="html"}
/figures/html/exemple.html
:::

Le site web a été configuré pour servir le document
[index.html]{.title-ref} lorsqu\'un navigateur demande la racine du site
web ([/]{.title-ref}). Le navigateur reçoit donc ce fichier en réponse à
sa requête GET HTTP. Il lit le contenu du document HTML et doit
directement :

> -   faire une requête GET HTTP pour charger la feuille de style
>     ([style.css]{.title-ref})
> -   faire une requête GET HTTP pour charger l\'image
>     [/images/logo.png]{.title-ref}

Si l\'utilisateur clique sur le lien vers [page.html]{.title-ref}, le
navigateur fera une nouvelle requête GET HTTP pour charger cette page
depuis le serveur et afficher son contenu. L\'interaction entre un
navigateur web et un serveur est donc une succession de requêtes HTTP.

## Flask

Flask s\'inspire de ce mode de fonctionnement et vous permet d\'écrire
un programme en python qui répond aux requêtes HTTP faites par le
navigateur.

::: {.literalinclude language="python"}
/flask/simple-flask.py
:::

Flask utilise des décorateurs python pour indiquer l\'URL qui doit être
associée à une fonction python. Lorsque le serveur reçoit une requête
GET HTTP qui demande le fichier [/]{.title-ref}, il exécute la fonction
[index()]{.title-ref} qui retourne le contenu correspondant au fichier
[index.html]{.title-ref}. Il en va de même pour la fonction
[page()]{.title-ref} qui est appelée automatiquement par le serveur web
dès que celui-ci reçoit une requête pour [page.html]{.title-ref}.

## Lancer l\'application

L\'exemple ci-dessus est suffisant pour créer un petit site simple. Si
le code python a été enregistré dans [flask.py]{.title-ref}, alors la
commande suivante suffit à lancer un serveur local:

``` console
flask --app flask.py run
* Serving Flask app 'app.py'
* Debug mode: off
WARNING: This is a development server. Do not use it in a production deployment.[...]
* Running on http://127.0.0.1:5000
Press CTRL+C to quit
```

Vous pouvez maintenant naviguer vers <http://127.0.0.1:5000> pour
visiter votre site web.

:::: note
::: title
Note
:::

Pour développer, il convient d\'héberger votre site web en local. Dans
un second temps, nous vous expliquerons comment utiliser Coolify pour
héberger votre site web.
::::

::: only
html

Continuez votre lecture avec le document `ref-mvc`{.interpreted-text
role="ref"}.
:::

> l\'HyperText l\'URL l\'Internet tutoriel


# Le modèle MVC {#ref-mvc}

Bien qu\'il soit possible de contenir tout le site dans un seul fichier
python, cela n\'est pas recommandable. Le fichier deviendra vite très
gros, et il sera difficile de modifier une partie de l\'application.

Le site suivant est fonctionnel, mais tout est mélangé. La gestion du
HTML dans une seule chaîne de caractère est particulièrement sujette à
l\'introduction d\'erreurs.

::: {.literalinclude language="python"}
/flask/simple-flask-html.py
:::

Nous allons voir un premier moyen de ségrégation entre deux rôles :

> -   la logique de l\'application, le code python qui va dans un
>     fichier [.py]{.title-ref}
> -   le rendu en HTML, qui va dans une série de fichiers HTML.

Dans le modèle MVC, ou Modèle-Vue-contrôleur, ces deux éléments sont
appelés respectivement le contrôleur et la vue. Très vite, vous allez
devoir utiliser le troisième rôle : les modèles. Les modèles gèrent les
données dynamiques, comme un utilisateur sur lequel le contrôleur va
travailler, afin de finalement afficher les données dans la vue. Nous y
reviendrons plus tard.

## Vue

Dans le modèle MVC abstrait, la vue gère ce qui concerne la structure de
la page, entendons ici le HTML. On utilise en général le terme
« template » pour désigner les fichiers HTML utilisés pour la vue. Nous
avons ici un problème lié au Français, en anglais [Template]{.title-ref}
se traduit en [Modèle]{.title-ref}, qui est un autre rôle du MVC. Nous
utiliserons donc plutôt le mot anglais [Template]{.title-ref}.

Déplaçons le code HTML de l\'index dans un fichier propre, dans
\`template/index.html\`:

::: {.literalinclude language="html"}
/flask/templates/index.html
:::

Nous allons utiliser la fonction [render_template()]{.title-ref} pour
aller chercher le contenu du fichier index.html et l\'afficher:

::: {.literalinclude language="python"}
/flask/simple-flask-template.py
:::

## Contrôleur

Le contrôleur est la logique de l\'application. Dans l\'exemple utilisé
ci-dessus, les deux pages sont des contrôlleurs. Il est possible de les
séparer dans des fichiers distincts, ce qui est souhaitable en utilisant
un blueprint. Les détails du blueprint seront vu au premier TP.

Le fichier suivant montre un contrôleur qui serait responsable de
[/page.html]{.title-ref}, mais dans un fichier séparé \`page.py\`:

::: {.literalinclude language="python"}
/flask/page.py
:::

Les blueprints permettent de déléguer des contrôleurs.

## Modèle

Ce sont les données, par exemple "User" qui contient "firstName",
"lastName", etc. On parle aussi parfois d\'objets pour des raisons que
vous verrez plus tard, dans les cours de programmation orientée objet.

En général, ils sont stockés et retournés dans/depuis une base de
données, nous verrons cela au `ref-chap-sql`{.interpreted-text
role="ref"}.

Le fichier suivant est créé dans un dossier [models]{.title-ref}, c\'est
une convention pour les modèles. Par exemple
[models/user.py]{.title-ref}.

::: {.literalinclude language="python"}
/flask/models/user.py
:::

À ce stade, la classe [User]{.title-ref} est très simple et ne contient
pas vraiment de logique si ce n\'est get_complete_name(). Dans le TP 3,
vous verrez que cela se complexifie rapidement.

## Interaction

En fonction d'une entrée (comme la requête [GET]{.title-ref} vers
[/page]{.title-ref}), Flask va choisir un contrôleur. Le contrôleur va
éventuellement utiliser une série de Modèles pour remplir les vues et
les renvoyer à l'utilisateur.

Ce concept sera mis en pratique dans le TP1, qui est accessible ici:
`ref-chapitre2`{.interpreted-text role="ref"}.

# Chapitre 2 : Travaux Pratiques #1 : Un site Flask sans base de données[]{#ref-tp-flask-static} {#ref-chapitre2}

Ce deuxième chapitre est votre première séance de travaux pratiques qui
sera suivie en S1. Vous créerez votre première application Flask
pas-à-pas.

::: {.toctree caption="Contenu du chapitre:"}
tuto_flask_without_sql/intro.rst tuto_flask_without_sql/installation.rst
tuto_flask_without_sql/tutorial/tutoriel.rst
tuto_flask_without_sql/tutorial/layout.rst
tuto_flask_without_sql/tutorial/factory.rst
tuto_flask_without_sql/tutorial/view_new.rst
tuto_flask_without_sql/tutorial/static.rst
tuto_flask_without_sql/tutorial/menu.rst
tuto_flask_without_sql/tutorial/next.rst
:::

# Les bases de données SQL {#ref-sql}

Quand on doit traiter de petits volumes de données, on peut se contenter
de les stocker dans des fichiers et d\'y accéder directement depuis des
programmes écrits en Python. Cette approche est simple et peut donner de
bons résultats pour de petits volumes de données ou des données sur
lesquelles on doit faire des opérations simples et qu\'il ne faut pas
souvent modifier. Dans tous les autres cas, il est préférable de faire
appel à des gestionnaires de bases de données qui ont été optimisés au
fil des années pour stocker et manipuler efficacement de grandes
quantités de données.

Aujourd\'hui, les bases de données les plus populaires sont les bases de
données qui sont dites relationnelles. Une telle base de données est
composée d\'une ou plusieurs *tables* qui contiennent de l\'information.
Chaque table est composée d\'un ensemble de lignes qu\'on appelle
souvent des records. L\'information dans une table est aussi divisée en
colonnes, chacune de ces colonnes correspondant à un champ ou attribut
qui est présent dans chaque record. Une telle base de données est dite
relationnelle car il est possible de lier entre eux les lignes qui se
trouvent dans des tables différents.

> Structured Query Language Android Windows iOS iTunes Binary OBject
> tutoriels

Dans ce document, nous nous focaliserons sur les bases de données
utilisant le Structured Query Language (SQL), un langage standardisé
supporté par défaut vendeurs de base de données. Pour le projet, nous
utiliserons [SQLite](https://sqlite.org) qui est une implémentation
efficace de SQL qui supporte de petites bases de données. SQLite a
l\'avantage d\'être très bien supporté par le langage Python. SQLite est
intégré dans les logiciels suivants : Android, iOS, MacOS, Windows10,
Firefox, Chrome, Safari, iTunes, Dropbox, \...

# Une table

Les tables constituent le coeur d\'une base de données. Chaque table
d\'une base de données est composée de colonnes et chaque colonne
contient de l\'information d\'un type particulier, comme un nombre, un
caractère, une data, une chaîne de caractères, \... Une ligne de la
table contient une valeur pour chaque colonne.

SQL permet de stocker différents types d\'information dans une table.
SQLite supporte les types suivants:

> -   `INTEGER` : un nombre entier
> -   `REAL` : un nombre réel
> -   `TEXT` : une chaîne de caractères
> -   `BLOB`: un séquence de bytes (Binary Large OBject)
> -   `NULL` : indique l\'absence d\'une valeur

SQLite peut aussi stocker des dates et des heures en les représentant
sous la forme d\'un `TEXT`, un `REAL` ou un `INTEGER`. Des fonctions
spécifiques permettent de manipuler ces dates et heures.

La base de données ci-dessous est composée de quatre colonnes. La
première contient des nombres entiers tandis que les trois autres
contiennent des chaînes de caractères. Lorsque l\'on crée une telle
table dans une base de données, il est souvent nécessaire de spécifier
la taille de chacun des champs qui est stocké. Ici, on aura par exemple
réservé 30 caractères pour le nom et le prénom et 50 pour l\'adresse
email. La colonne matricule ne peut contenir que des nombres entiers.

  ------------ ------------ ----------- --------------------------
  matricule    nom          prénom      email

  17           Durand       Jules       <jules.durand@gmail.com>

  42           Tartempion   Emilie      <et@hotmail.com>

  95           Durant       Antoine     <durant@hotmail.com>
  ------------ ------------ ----------- --------------------------

> Durand Tartempion Durant Jules Emilie Antoine

Lorsque l\'on conçoit une base de données, on en définit son schéma,
c\'est-à-dire la structure de chacune des tables et les liens qui
existent entre ces tables. Pour pouvoir faire des liens entre des
tables, il est important de pouvoir identifier une ligne d\'une table de
façon unique. Dans la table des étudiants présentée ci-dessous, cela
peut se faire en utilisant le matricule ou l\'adresse email de
l\'étudiant. Cet identifiant unique est appelé une *clé primaire*
([primary key]{.title-ref} en anglais). Cette clé peut être une colonne
de la table ou dans certains cas un groupe de colonnes de la table. Dans
la table ci-dessus, les noms et prénoms des étudiants ne sont pas de
bonnes clés primaires puisque rien ne garantir leur unicité.

Cette clé primaire peut servir de lien vers une autre table. Considérons
une table qui reprend les inscriptions à un programme universitaire.
Celle-ci pourrait être structurée comme suit:

  ------------ ------------ -----------
  programme    étudiant     année

  SINF1BA      17           2

  SINF11       33           1

  SINF1BA      42           3
  ------------ ------------ -----------

Dans ce cas, le matricule de la première table sert de clé externe
([foreign key]{.title-ref} en anglais) dans la seconde table. Des
relations plus complexes peuvent être créées entre les différentes
tables d\'une base de données. Le principe de base lors de la création
d\'un schéma de base de données est d\'encoder une information à un seul
endroit dans la base de données et d\'utiliser des clés externes pour
faire référence à la table contenant l\'information mère. Les règles de
création d\'un base de données sortent du cadre de ce projet et seront
abordées dans le cadre du cours de bases de données.

> tutoriel téléchargée

# Utilisation de SQL depuis Python

SQL est un langage standardisé qui est supporté par de nombreuses bases
de données et de nombreux langages de programmation. Il y a de
nombreuses façons d\'accéder à une base de données en SQL. Dans le cadre
de ce tutoriel, nous utiliserons la base de données d\'exemple baptisée
Chinook qui est notamment utilisée par le site
<https://sqlitetutorial.net>.

Cette base de données peut être téléchargée depuis :
<https://github.com/lerocha/chinook-database/raw/master/ChinookDatabase/DataSources/Chinook_Sqlite.sqlite>

Une première façon d\'explorer son contenu est d\'utiliser un logiciel
disposant d\'une interface graphique tel que
[sqlitebrowser](https://sqlitebrowser.org/).

<figure>
<img src="/figures/sqlitebrowser.png"
alt="/figures/sqlitebrowser.png" />
<figcaption>Utilisation de sqlitebrowser sur la base de données
Chinook</figcaption>
</figure>

Un outil tel que [sqlitebrowser](https://sqlitebrowser.org/) est
intéressant pour sa balader dans une nouvelle base de données ou
modifier son contenu, mais c\'est nettement moins flexible que d\'écrire
un programme pour l\'interroger.

Il est aussi possible d\'accéder à la base de données depuis
l\'interface en ligne de commande de sqlite.

<figure>
<img src="/figures/sqlite-cli.png" alt="/figures/sqlite-cli.png" />
<figcaption>Utilisation de sqlite en ligne de commande</figcaption>
</figure>

La commande `.tables` permet de lister les tables se trouvant dans la
base de données. La base de données Chinook contient notamment de
l\'information relative à des albums musicaux. Celle-ci est structurée
dans plusieurs tables. La commande `.schema` permet de voir les
commandes qui ont été utilisées pour créer cette table de la base de
données. Nous reviendrons sur les principales commandes de SQL en nous
concentrant sur celles qui permettent d\'extraire des données.

> package sqlite

## Connexion à une base de données SQL

SQLite est directement inclus dans la distribution de Python. Vous
pouvez donc l\'utiliser en important simplement le package `sqlite3`
dans vos programmes Python. La première étape pour utiliser une base de
données est de s\'y connecter. Dans une entreprise, cela peut nécessiter
de connaître le nom du serveur sur laquelle elle tourne et d\'obtenir
des informations telles qu\'un nom d\'utilisateur ou un mot de passe.
Comme SQLite utilise un fichier unique sur l\'ordinateur pour stocker la
base de données, il suffit de spécifier le nom de ce fichier pour y
accéder via la fonction `sqlite3.connect`. Cette fonction retourne un
objet `Connection` qui permet d\'interagir avec la base de données.
L\'envoi de commandes SQL se fait en utilisant un objet `Cursor` qui est
obtenu grâce à la méthode `cursor()`. C\'est via cet objet que toutes
les interactions avec la base de données se feront depuis le programme
Python. Lorsque le programme a fini d\'utiliser la base de données, il
doit fermer la connexion avec la méthode `close()`. Si celle-ci a été
modifiée, il faut penser à faire appel à `commit()` pour forcer
l\'écriture des modifications.

::: {.literalinclude language="python"}
/sql/db.py
:::

## Création d\'une base de données SQL

La première étape est de créer une base de données. Commençons par une
base de données comprenant une seule table. Notre base de données va
stocker les élèves d\'une classe. Elle contient les informations
suivantes:

> -   Nom de l\'élève (chaîne de caractères)
> -   Prénom de l\'élève (chaîne de caractères)
> -   Année de naissance (nombre entier)
> -   Moyenne des points (nombre réel)
> -   Matricule (entier)

La clé primaire de cette table est le matricule qui est unique pour
chaque élève. La table peut être créée par la commande suivante :

::: {.literalinclude language="python" start-after="#start" end-before="#end"}
/sql/db-create.py
:::

Dans ce schéma, on indique que les champs `MATRICULE`, `NOM`, `PRENOM`,
et `AGE` sont obligatoires en spécifiant qu\'ils ne peuvent pas avoir la
valeur `NULL`. Le moteur de base de données vérifiera que cette
contrainte est respectée lors de toute modification de la base de
données.

Dans l\'exemple ci-dessus, nous pouvons observer que la clé primaire est
`MATRICULE`. Grace à cet attribut, nous pouvons identifier de manière
unique chaque ligne de cette table. Dans un monde où chaque étudiant
pourrait être identifié par la composition de son `NOM` et `PRENOM`,
nous pourrions définir une clé primaire composée, comme indiqué dans
l\'exemple ci-dessous:

::: {.literalinclude language="python" start-after="#start" end-before="#end"}
/sql/db-create-composite-key.py
:::

Cependant cette solution de clé composée n\'est pas optimale, car comme
annoncé plus haut, nous pourrions rencontrer des étudiants portant les
mêmes noms et prénoms. Et nous ne pourrions plus les identifier de
manière unique.

## Ajout d\'information dans une base de données SQL

La table étant créée, nous pouvons maintenant y ajouter de
l\'information. Cela se fait en utilisant la commande SQL `INSERT INTO`
qui prend comme arguments un nom de table, une liste d\'identifiants de
colonnes, et une liste de valeurs précédée du mot-clé `VALUES`.

La première façon d\'insérer des données dans une table SQL est de
fournir la commande avec toutes les données à insérer comme dans
l\'exemple ci-dessous.

::: {.literalinclude language="python" start-after="#s1" end-before="#e1"}
/sql/db-insert2.py
:::

Lorsque l\'on doit insérer plusieurs données dans la table, par exemple
le contenu d\'une liste Python ou d\'un dictionnaire, il est plus facile
d\'utiliser des espaces réservés qui sont identifiés dans la commande
par le caractère `?`. La librairie [sqlite3]{.title-ref} remplace ces
espaces réservés par les valeurs se trouvant dans la liste passée en
argument.

::: {.literalinclude language="python" start-after="#s2" end-before="#e2"}
/sql/db-insert2.py
:::

On peut faire de même avec un dictionnaire et indiquer dans la chaîne de
caractères qui contient la commande SQL des noms de clés et passer en
second argument un dictionnaire définissant un valeur pour chacune de
ces clés. Dans la commande SQL, chaque clé est précédée du caractère
[:]{.title-ref}. Cette forme peut être utile lorsqu\'il faut insérer le
contenu d\'un dictionnaire dans une table SQL.

::: {.literalinclude language="python" start-after="#s3" end-before="#e3"}
/sql/db-insert2.py
:::

Lorsque [sqlite3]{.title-ref} traite une commande d\'insertion, la
librairie vérifie que les contraintes spécifiées à la création de la
table sont respectées. Ces contraintes peuvent porter sur la présence de
valeurs nulles, la taille des chaînes de caractères, etc. L\'exemple
ci-dessous montre une insertion d\'un record qui ne contient pas de
valeur pour le champ `POINTS`. Cette insertion est acceptée puisqu\'elle
est conforme à la définition de la table `CLASSE`.

::: {.literalinclude language="python" start-after="#s4" end-before="#e4"}
/sql/db-insert2.py
:::

Par contre, il n\'est pas possible d\'insérer dans la base de données un
record qui ne contient pas de valeur pour le champ `AGE`.

::: {.literalinclude language="python" start-after="#s5" end-before="#e5"}
/sql/db-insert2.py
:::

## Recherche d\'information dans une base de données SQL

Dans le cadre de ce projet, vous vous concentrerez sur l\'extraction
d\'information se trouvant dans une base de données existante, mais vous
ne la modifierez normalement pas. En SQL, l\'extraction d\'information
se fait en utilisant la requête `SELECT`. La forme générique d\'une
requête `SELECT` est
`SELECT <liste de colonnes> FROM <table> WHERE <conditions>` où
`<liste de colonnes>` est une liste d\'identifiant de colonnes,
`<table>` le nom d\'une table et `<conditions>` une série de conditions
qui permettent de sélectionner les données à extraire.

La forme la plus simple de la requête est de ne pas écrire de condition.

::: {.literalinclude language="python" start-after="#start" end-before="#end"}
/sql/db-select1.py
:::

Ce code affiche sur sa sortie standard les étudiants de la classe.

``` console
Prénom    Nom
Emilie    Durant
Joséphine     Durand
Jean      Tartempion
Jules     Dupont
```

Plutôt que de spécifier les colonnes qui sont demandées, il est aussi
possible d\'obtenir une copie du contenu de toute la table en utilisant
`*` comme identifiant de colonnes.

::: {.literalinclude language="python" start-after="#s1" end-before="#e1"}
/sql/db-select1.py
:::

Ce code retourne la liste des attributs contenus dans la table `CLASSE`.

``` console
(1, 'Durant', 'Emilie', 8, 73.5)
(2, 'Durand', 'Joséphine', 7, 88.65)
(4, 'Tartempion', 'Jean', 9, 68.65)
(12, 'Dupont', 'Jules', 9, None)
```

En utilisant les conditions de la requête `SELECT`, il est possible de
filtrer les données avant de les extraire. SQL supporte de nombreux
filtres. Il est tout d\'abord possible de comparer la valeur d\'un champ
de la base de données. Les comparaisons suivantes sont supportées :

> -   `=` : égal
> -   `<>` : différent
> -   `>` : plus grand que (ainsi que `>=`)
> -   `<` : plus petit que (ainsi que `<=`)

A titre d\'exemple, le code ci-dessous permet d\'extraire les étudiants
qui ont une moyenne supérieure à 70.

::: {.literalinclude language="python" start-after="#s2" end-before="#e2"}
/sql/db-select1.py
:::

Plusieurs conditions peuvent être combinées sous la forme d\'une
expression booléenne en utilisant les opérateurs `AND`, `OR` et `NOT`
habituels.

Parfois, une requête SQL retourne de nombreux résultats identiques.
Supposons que l\'on cherche à savoir les différents âges des étudiants
de la classe sans avoir besoin de connaître le nombre d\'étudiants ayant
chaque âge.

::: {.literalinclude language="python" start-after="#s3" end-before="#e3"}
/sql/db-select1.py
:::

Cette requête extrait tous les âges (différents de NULL) de notre table.
Dans une grande base de données, cette liste peut être fort longue.

``` console
(8,)
(7,)
(9,)
(9,)
```

Une meilleure approche est d\'indiquer dans la requête SQL que l\'on
souhaite juste obtenir les valeurs distinctes.

::: {.literalinclude language="python" start-after="#s4" end-before="#e4"}
/sql/db-select1.py
:::

SQL supporte des conditions plus complexes. Il est notamment possible de
rechercher si un champ est `NULL`. La requête ci-dessous va extraire de
notre table le record dont le champ `POINTS` est NULL et afficher
`('Dupont', 12)`.

::: {.literalinclude language="python" start-after="#s5" end-before="#e5"}
/sql/db-select1.py
:::

Les conditions d\'une requête SQL peuvent aussi porter sur le contenu
des chaînes de caractères. L\'approche est assez simple comparée aux
expressions régulières que l\'on retrouve dans Python, mais elle permet
déjà de faire une pré-traitement de certaines données. Dans la chaîne de
caractères d\'une condition, le caractère spécial `_` correspond à
n\'importe quel caractère tandis que le caractère `%` peut remplacer
n\'importe quelle suite de caractères. Les requêtes ci-dessous
permettent d\'extraire de la base de données les élèves dont le nom de
famille contient certains caractères.

::: {.literalinclude language="python" start-after="#s6" end-before="#e6"}
/sql/db-select1.py
:::

Résultat affiché par ce code.

``` console
Requête : Du%
('Durant', 'Emilie')
('Durand', 'Joséphine')
('Dupont', 'Jules')
Requête : Du%t
('Durant', 'Emilie')
('Dupont', 'Jules')
Requête : D_____t
('Durant', 'Emilie')
('Dupont', 'Jules')
```

Le langage SQL contient de nombreuses fonctions que l\'on peut utiliser
dans une requête SQL. Tout d\'abord, il est possible appliquer les
opérations arithmétiques classiques (`+`, `-`, `*` et `/`) aux valeurs
ou variables numériques.

::: {.literalinclude language="python" start-after="#s7" end-before="#e7"}
/sql/db-select1.py
:::

Cette requête affiche la sortie suivante :

``` console
('Durant', 83.5)
('Durand', 98.65)
('Tartempion', 78.65)
('Dupont', None)
```

SQL supporte également des
[fonctions](https://sqlite.org/lang_corefunc.html) qui permettent de
manipuler les chaînes de caractères comme dans n\'importe quel autre
langage de programmation. Par exemple :

> -   `length(X)` qui retourne la longueur de la chaîne de caractères
>     `X`
> -   `instr(X,Y)` qui retourne la première occurrence de la chaîne `Y`
>     dans `X`
> -   `lower(X)` qui transforme `X` en minuscules (voir aussi
>     `upper(X)`)
> -   `substr(X,Y,Z)` qui retourne la sous-chaîne de caractères de `X`
>     qui démarre au caractère `Y` et es longue de `Z` caractères
> -   `trim(X,Y)` qui retire du début et de la fin de la chaîne `X` tous
>     les caractères qui se trouvent dans la chaîne `Y`

Les autres fonctions sont décrites dans le manuel de SQLite:
<https://sqlite.org/lang.html>

SQLite support également des fonctions spécifiques à la manipulation des
dates. Celles-ci sont décrites dans le manuel de SQLIte:
<https://sqlite.org/lang_datefunc.html>

Parmi les fonctions supportées par SQLite, les [fonctions
d\'agrégation](https://sqlite.org/lang_aggfunc.html) sont particulières
car elles permettent de réaliser des calculs sur les résultats d\'une
requête. Voici quelques exemples qui illustrent leur utilisation. Elles
sont décrites dans le manuel de SQLite:
<https://sqlite.org/lang_aggfunc.html>.

::: {.literalinclude language="python" start-after="#s8" end-before="#e8"}
/sql/db-select1.py
:::

Lorsque l\'on manipule une base de données, il est parfois nécessaire de
connaître le nombre de fois qu\'une valeur distincte est présente dans
la base de données, sans nécessairement devoir charger toutes ces
valeurs. Cela peut se faire en utilisant le modifier `DISTINCT`.
L\'exemple ci-dessous affiche `(4, )` ce qui indique qu\'il y a quatre
noms distincts dans notre table d\'exemple.

::: {.literalinclude language="python" start-after="#s9" end-before="#e9"}
/sql/db-select1.py
:::

Jusqu\'à présent, nous avons manipulé une base de données minuscule
contenant une seule table. Pour aborder des utilisations plus avancées
de SQL, nous allons maintenant travailler sur la base de données Chinook
qui a été présentée plus tôt. Cette base de données comprend plusieurs
tables.

``` console
sqlite> .tables
Album          Employee       InvoiceLine    PlaylistTrack
Artist         Genre          MediaType      Track        
Customer       Invoice        Playlist     
```

Dans la suite de ce document, nous allons utiliser les tables `Album`,
`Artist` et `Track`.

La table `Artist` est très simple, elle contient une liste d\'artistes
et associe à chacun d\'entre eux un identifiant.

``` console
sqlite> .schema Artist
CREATE TABLE [Artist]
(
  [ArtistId] INTEGER  NOT NULL,
  [Name] NVARCHAR(120),
  CONSTRAINT [PK_Artist] PRIMARY KEY  ([ArtistId])
);
CREATE UNIQUE INDEX [IPK_Artist] ON [Artist]([ArtistId]);
```

La requête ci-dessous permet de visualiser un sous-ensemble de cette
table qui contient 275 artistes.

::: {.literalinclude language="python" start-after="#s1" end-before="#e1"}
/sql/db-chinook.py
:::

``` console
Table Artist
(1, 'AC/DC')
(2, 'Accept')
(3, 'Aerosmith')
(4, 'Alanis Morissette')
(5, 'Alice In Chains')
(6, 'Antônio Carlos Jobim')
(7, 'Apocalyptica')
(8, 'Audioslave')
(9, 'BackBeat')
(10, 'Billy Cobham')
Nombre total de lignes:  275
```

Il est intéressant de noter que si l\'on cherche à extraire uniquement
quelques lignes de la base de données, il suffit d\'utiliser le
paramètre `LIMIT` comme dans l\'exemple ci-dessous.

::: {.literalinclude language="python" start-after="#s1b" end-before="#e1b"}
/sql/db-chinook.py
:::

La table `Album` contient une liste d\'albums de musique avec des
références vers la table `Artist`. Afin de définir cette contrainte sur
votre schéma de base de données, vous devez ajouter une ligne
`FOREIGN KEY (ArtistId) REFERENCES Artist (ArtistId)` lors de la
création de votre table, comme indiqué dans la console ci-dessous.
Chaque album est associé à un identifiant unique.

``` console
sqlite> .schema Album
CREATE TABLE [Album]
(
 [AlbumId] INTEGER  NOT NULL,
 [Title] NVARCHAR(160)  NOT NULL,
 [ArtistId] INTEGER  NOT NULL,
 CONSTRAINT [PK_Album] PRIMARY KEY  ([AlbumId]),
 FOREIGN KEY ([ArtistId]) REFERENCES [Artist] ([ArtistId]) 
     ON DELETE NO ACTION ON UPDATE NO ACTION
);
CREATE UNIQUE INDEX [IPK_Album] ON [Album]([AlbumId]);
CREATE INDEX [IFK_AlbumArtistId] ON [Album] ([ArtistId]);
```

Cette table contient 347 lignes.

::: {.literalinclude language="python" start-after="#s2" end-before="#e2"}
/sql/db-chinook.py
:::

``` console
Table Album
(1, 'For Those About To Rock We Salute You', 1)
(2, 'Balls to the Wall', 2)
(3, 'Restless and Wild', 2)
(4, 'Let There Be Rock', 1)
(5, 'Big Ones', 3)
(6, 'Jagged Little Pill', 4)
(7, 'Facelift', 5)
(8, 'Warner 25 Anos', 6)
(9, 'Plays Metallica By Four Cellos', 7)
(10, 'Audioslave', 8)
Nombre total de lignes:  347
```

La table `Track` est la plus complexe. Elle contient les informations
relatives aux chansons qui se trouvent sur les différents albums de
musique.

``` console
sqlite> .schema Track
CREATE TABLE [Track]
(
 [TrackId] INTEGER  NOT NULL,
 [Name] NVARCHAR(200)  NOT NULL,
 [AlbumId] INTEGER,
 [MediaTypeId] INTEGER  NOT NULL,
 [GenreId] INTEGER,
 [Composer] NVARCHAR(220),
 [Milliseconds] INTEGER  NOT NULL,
 [Bytes] INTEGER,
 [UnitPrice] NUMERIC(10,2)  NOT NULL,
 CONSTRAINT [PK_Track] PRIMARY KEY  ([TrackId]),
 FOREIGN KEY ([AlbumId]) REFERENCES [Album] ([AlbumId]) 
     ON DELETE NO ACTION ON UPDATE NO ACTION,
 FOREIGN KEY ([GenreId]) REFERENCES [Genre] ([GenreId]) 
     ON DELETE NO ACTION ON UPDATE NO ACTION,
 FOREIGN KEY ([MediaTypeId]) REFERENCES [MediaType] ([MediaTypeId]) 
     ON DELETE NO ACTION ON UPDATE NO ACTION
);
CREATE UNIQUE INDEX [IPK_Track] ON [Track]([TrackId]);
CREATE INDEX [IFK_TrackAlbumId] ON [Track] ([AlbumId]);
CREATE INDEX [IFK_TrackGenreId] ON [Track] ([GenreId]);
CREATE INDEX [IFK_TrackMediaTypeId] ON [Track] ([MediaTypeId]);
```

Cette table contient 3503 morceaux de musique.

::: {.literalinclude language="python" start-after="#s3" end-before="#e3"}
/sql/db-chinook.py
:::

``` console
Table Track
(1, 'For Those About To Rock (We Salute You)', 1, 1, 1, 'Angus Young, Malcolm Young, Brian Johnson', 343719, 11170334, 0.99)
(2, 'Balls to the Wall', 2, 2, 1, None, 342562, 5510424, 0.99)
(3, 'Fast As a Shark', 3, 2, 1, 'F. Baltes, S. Kaufman, U. Dirkscneider & W. Hoffman', 230619, 3990994, 0.99)
(4, 'Restless and Wild', 3, 2, 1, 'F. Baltes, R.A. Smith-Diesel, S. Kaufman, U. Dirkscneider & W. Hoffman', 252051, 4331779, 0.99)
(5, 'Princess of the Dawn', 3, 2, 1, 'Deaffy & R.A. Smith-Diesel', 375418, 6290521, 0.99)
(6, 'Put The Finger On You', 1, 1, 1, 'Angus Young, Malcolm Young, Brian Johnson', 205662, 6713451, 0.99)
(7, "Let's Get It Up", 1, 1, 1, 'Angus Young, Malcolm Young, Brian Johnson', 233926, 7636561, 0.99)
(8, 'Inject The Venom', 1, 1, 1, 'Angus Young, Malcolm Young, Brian Johnson', 210834, 6852860, 0.99)
(9, 'Snowballed', 1, 1, 1, 'Angus Young, Malcolm Young, Brian Johnson', 203102, 6599424, 0.99)
(10, 'Evil Walks', 1, 1, 1, 'Angus Young, Malcolm Young, Brian Johnson', 263497, 8611245, 0.99)
Nombre total de lignes:  3503
```

Avec ce trois tables, il est possible d\'explorer des requêtes SQL plus
complexes.

Commençons par essayer d\'extraire de la base de données les albums
d\'un artiste donné. Pour cela, il faut d\'abord extraire l\'identifiant
de cet artiste de la table `Artist` puis faire une requête dans la table
`Album` comme la suivante:

::: {.literalinclude language="python" start-after="#s4" end-before="#e4"}
/sql/db-chinook.py
:::

Cette requête affiche:

``` console
Albums d'AC/DC
('For Those About To Rock We Salute You',)
('Let There Be Rock',)
Nombre total de lignes:  2
```

Ce n\'est pas très efficace au niveau de l\'utilisation de la base de
données. Il faut en effet d\'abord consulter la base de données pour
connaître l\'identifiant de l\'artiste et ensuite rechercher celui-ci
dans la table `Album`. Si l\'on veut rechercher les albums de plusieurs
artistes, la clause WHERE peut prendre comme argument une liste
d\'identifiants comme dans l\'exemple ci-dessous.

::: {.literalinclude language="python" start-after="#s5" end-before="#e5"}
/sql/db-chinook.py
:::

``` console
Albums d'AC/DC ou Aerosmith
('For Those About To Rock We Salute You',)
('Let There Be Rock',)
('Big Ones',)
Nombre total de lignes:  3
```

Cette approche peut être étendue pour par exemple extraire de la base de
données tous les albums d\'un artiste dont le nom commence par `A`.

::: {.literalinclude language="python" start-after="#s6" end-before="#e6"}
/sql/db-chinook.py
:::

Même si ce code affiche le résultat demandé, ce n\'est pas la bonne
approche.

``` console
Ids des artistes dont le nom débute par A
[1, 2, 3, 4, 5, 6, 7, 8, 26, 43, 159, 161, 166, 197, 202, 206, 209, 214, 215, 222, 230, 239, 243, 252, 257, 260]
Albums d'artistes dont le nom débute par A
('For Those About To Rock We Salute You',)
('Let There Be Rock',)
('Balls to the Wall',)
('Restless and Wild',)
('Big Ones',)
('Jagged Little Pill',)
('Facelift',)
('Warner 25 Anos',)
('Chill: Brazil (Disc 2)',)
('Plays Metallica By Four Cellos',)
Nombre total de lignes:  27
```

La bonne approche est d\'utiliser SQL pour générer aussi la liste des
artistes dans une seule requête. Il est en effet possible de mettre dans
la clause `WHERE` d\'une requête une autre requête SQL qui elle aussi
produit une liste.

::: {.literalinclude language="python" start-after="#s7" end-before="#e7"}
/sql/db-chinook.py
:::

Cette requête fournit le résultat attendu.

``` console
Albums d'artistes dont le nom débute par A
('For Those About To Rock We Salute You',)
('Let There Be Rock',)
('Balls to the Wall',)
('Restless and Wild',)
('Big Ones',)
('Jagged Little Pill',)
('Facelift',)
('Warner 25 Anos',)
('Chill: Brazil (Disc 2)',)
('Plays Metallica By Four Cellos',)
Nombre total de lignes:  27
```

Il est évidemment possible d\'utiliser une requête SQL dans la clause
`WHERE` de la seconde requête et ainsi de suite.

SQL permet aussi de contrôler l\'ordre dans lequel les données sont
retournée. Par défaut, celles-ci sont retournées dans un ordre non
spécifié, mais on peut forcer un ordonnancement sur base de certaines
colonnes en utilisant le paramètre `ORDER BY` après la liste des tables
(ou après la clause `WHERE` si celle-ci est présente).

::: {.literalinclude language="python" start-after="#s10" end-before="#e10"}
/sql/db-chinook.py
:::

Cette requête affiche les noms d\'albums dans l\'ordre alphabétique.

``` console
(156, '...And Justice For All')
(257, '20th Century Masters - The Millennium Collection: The Best of Scorpions')
(296, 'A Copland Celebration, Vol. I')
(94, 'A Matter of Life and Death')
(95, 'A Real Dead One')
```

Il est aussi possible de spécifier un ordre sur une première colonne et
une seconde en croissant ou décroissant.

::: {.literalinclude language="python" start-after="#s11" end-before="#e11"}
/sql/db-chinook.py
:::

Cette requête affiche les noms des cinq plus longs morceaux de la base
de données.

``` python
(2820, 'Occupation / Precipice', 5286953)
(3224, 'Through a Looking Glass', 5088838)
(3244, 'Greetings from Earth, Pt. 1', 2960293)
(3242, 'The Man With Nine Lives', 2956998)
(3227, 'Battlestar Galactica, Pt. 2', 2956081)
```

SQL permet aussi de combiner des informations qui sont stockées dans
plusieurs tables différentes. Celle-ci s\'appelle généralement une
jointure dans la terminologie SQL. Une telle jointure est illustrée dans
l\'exemple ci-dessous.

::: {.literalinclude language="python" start-after="#s8" end-before="#e8"}
/sql/db-chinook.py
:::

Cette requête retourne le résultat attendu.

``` console
Albums et artistes 
('For Those About To Rock We Salute You', 'AC/DC')
('Balls to the Wall', 'Accept')
('Restless and Wild', 'Accept')
('Let There Be Rock', 'AC/DC')
('Big Ones', 'Aerosmith')
('Jagged Little Pill', 'Alanis Morissette')
('Facelift', 'Alice In Chains')
('Warner 25 Anos', 'Antônio Carlos Jobim')
('Plays Metallica By Four Cellos', 'Apocalyptica')
('Audioslave', 'Audioslave')
Nombre total de lignes:  347
```

Soyez cependant attentif au fonctionnement d\'un jointure en SQL.
Conceptuellement, il faut imagine qu\'une jointure se déroule comme
suit:

> 1.  La base de données extrait les lignes des deux tables
>     sélectionnées et construit toutes les paires de lignes contenant
>     une ligne de la première et une ligne de la seconde
> 2.  La base de données filtre les lignes intéressantes sur base des
>     clauses `WHERE`
> 3.  La base de données retourne les colonnes indiquées dans le
>     `SELECT`

Il faut garder ce mode de fonctionnement en mémoire lorsque l\'on
utilise une jointure SQL. La requête ci-dessous est un bon
contre-exemple de ce qu\'il ne faut pas faire.

::: {.literalinclude language="python" start-after="#s9" end-before="#e9"}
/sql/db-chinook.py
:::

``` console
('For Those About To Rock We Salute You', 'AC/DC')
('For Those About To Rock We Salute You', 'Accept')
('For Those About To Rock We Salute You', 'Aerosmith')
('For Those About To Rock We Salute You', 'Alanis Morissette')
('For Those About To Rock We Salute You', 'Alice In Chains')
('For Those About To Rock We Salute You', 'Antônio Carlos Jobim')
('For Those About To Rock We Salute You', 'Apocalyptica')
('For Those About To Rock We Salute You', 'Audioslave')
('For Those About To Rock We Salute You', 'BackBeat')
('For Those About To Rock We Salute You', 'Billy Cobham')
Nombre total de lignes:  95425
```

Cette requête retourne le produit-cartésien entre les deux tables. Si la
première contient [N]{.title-ref} lignes et la secondes [M]{.title-ref}
lignes, le résultat en contient [N\*M]{.title-ref} ce qui peut être
énorme pour de grosses bases de données.

SQLite supporte trois types de jointures: `INNER JOIN`, `LEFT JOIN` et
`CROSS JOIN`. Il est intéressant de voir sur quelques exemples comment
ces jointures se comportent.

Notre première requête permet d\'afficher les artistes avec leurs albums
en joignant la table `Album` avec la table `Artist`.

::: {.literalinclude language="python" start-after="#s12" end-before="#e12"}
/sql/db-chinook.py
:::

Dans cette requête, le champ `Name` provient de la table `Artist` tandis
que le champ `Title` de la table `Album`. Seules les lignes pour
lesquelles le champ `ArtistId` provenant de la table `Artist` est
identique à celui provenant de la table `Album` sont affichées.

``` console
('AC/DC', 'For Those About To Rock We Salute You')
('AC/DC', 'Let There Be Rock')
('Aaron Copland & London Symphony Orchestra', 'A Copland Celebration, Vol. I')
('Aaron Goldberg', 'Worlds')
('Academy of St. Martin in the Fields & Sir Neville Marriner', 'The World of Classical Favourites')
```

Des exemples complémentaires sont disponibles dans le tutoriel SQLite:
<https://www.sqlitetutorial.net/sqlite-inner-join/>

Cette jointure permet de combiner l\'information de deux tables.
Cependant, elle ne permet pas de lister les artistes qui n\'ont pas
d\'album dans la base de données, car pour ceux-ci, la condition
`Artist.ArtistId = Album.ArtistId` est toujours fausse puisque la table
`Album` ne contient aucune ligne avec l\'identifiant de cet artiste. Si
l\'on veut obtenir cette information avec SQLite, il est possible
d\'utiliser un `LEFT JOIN`. Cette jointure fonctionne conceptuellement
en extrayant toutes les lignes de la première table (celle dite à
gauche) et les lignes qui correspondent à la condition pour la seconde
table (celle dite à droite). Le `LEFT JOIN` retourne ensuite toutes les
lignes qui correspondent à la condition. Si une ligne de la première
table n\'a pas de ligne correspondante dans la seconde, SQLite retourne
les champs de la première table et `NULL` pour ceux qui correspondent à
la seconde.

::: {.literalinclude language="python" start-after="#s13" end-before="#e13"}
/sql/db-chinook.py
:::

Cette requête est particulièrement utile pour rechercher des lignes qui
existent dans la première table, mais pas dans la seconde. Elle
retourne:

``` console
('A Cor Do Som', None)
('Academy of St. Martin in the Fields, Sir Neville Marriner & William Bennett', None)
("Aerosmith & Sierra Leone's Refugee Allstars", None)
('Avril Lavigne', None)
('Azymuth', None)
```

D\'autres exemples sont présentés dans le tutoriel SQLite:
<https://www.sqlitetutorial.net/sqlite-left-join/>

La dernière jointure supportée par SQLite est appelée `CROSS JOIN`. Elle
retourne le produit cartésien entre les deux tables et doit être
utilisée avec prudence vu la taille du résultat qu\'elle peut retourner.

Avant de terminer ce survol rapide des fonctionnalités de SQL, il est
utile de revenir sur les fonctions qui permettent d\'agréger de
l\'information extraite d\'une base de données SQL. SQLite supporte
plusieurs de ces fonctions dont `avg()` pour calculer une moyenne,
`min()` et `max` ou encore `count()`. Il est aussi possible de
concaténer des chaînes de caractères avec `group_concat()`. Lorsque
l\'on utilise ces fonctions, il est parfois important de spécifier les
champs sur lesquels elles s\'appliquent et comment les résultats doivent
être retournés. Pour cela, la clause optionnelle `GROUP BY` d\'une
requête `SELECT` peut s\'avérer utile.

Supposons que l\'on cherche à compter le nombre de morceaux présents
dans chaque album de la table `Album`. Cette table contient de nombreux
albums comme l\'indique la requête ci-dessous.

::: {.literalinclude language="python" start-after="#s17" end-before="#e17"}
/sql/db-chinook.py
:::

``` console
(1, 'For Those About To Rock (We Salute You)', 1)
(1, 'Put The Finger On You', 6)
(1, "Let's Get It Up", 7)
(1, 'Inject The Venom', 8)
(1, 'Snowballed', 9)
(1, 'Evil Walks', 10)
(1, 'C.O.D.', 11)
(1, 'Breaking The Rules', 12)
(1, 'Night Of The Long Knives', 13)
(1, 'Spellbound', 14)
(2, 'Balls to the Wall', 2)
(3, 'Fast As a Shark', 3)
(3, 'Restless and Wild', 4)
(3, 'Princess of the Dawn', 5)
(4, 'Go Down', 15)
```

Une approche naïve pour compter les morceaux de chaque album serait
d\'écrire la requête suivante.

::: {.literalinclude language="python" start-after="#s16" end-before="#e16"}
/sql/db-chinook.py
:::

Malheureusement celle-ci ne produit pas le résultat attendu.

``` console
(1, 3503)
```

Elle compte les différentes valeurs de TrackId, mais non les morceaux
associés à chaque album. Pour obtenir un résultat correct, il faut
demander dans la requête SQL de grouper ensemble les valeurs qui ont le
même TrackId. Cela peut se faire avec le clause `GROUP BY` comme dans
l\'exemple ci-dessous.

::: {.literalinclude language="python" start-after="#s15" end-before="#e15"}
/sql/db-chinook.py
:::

Cette requête produit le résultat attendu.

``` console
(1, 10)
(2, 1)
(3, 3)
(4, 8)
(5, 15)
```

De la même façon, on peut rechercher tous les albums d\'un artiste
donné.

::: {.literalinclude language="python" start-after="#s18" end-before="#e18"}
/sql/db-chinook.py
:::

Cette requête produit le résultat attendu.

``` console
(1, 'For Those About To Rock We Salute You !! Let There Be Rock')
(2, 'Balls to the Wall !! Restless and Wild')
(3, 'Big Ones')
(4, 'Jagged Little Pill')
(5, 'Facelift')
```

Il est évidemment possible de combiner une jointure avec la clause
`GROUP BY`. La requête ci-dessous extrait les cinq albums qui
contiennent le plus de morceaux différents.

::: {.literalinclude language="python" start-after="#s14" end-before="#e14"}
/sql/db-chinook.py
:::

Cette requête produit le résultat attendu.

``` console
('Greatest Hits', 57)
('Minha Historia', 34)
('Unplugged', 30)
('Lost, Season 3', 26)
('Lost, Season 1', 25)
```

D\'autres exemples sont repris dans la section consacrée à `GROUP BY` du
site [SQLiteTutorial.net](https://www.sqlitetutorial.net/) :
<https://www.sqlitetutorial.net/sqlite-group-by/>

De nombreux livres et sites web proposés des cours et tutoriels sur
l\'utilisation des bases de données et de SQL en particulier. En voici
quelques-uns :

> -   J.-L. Hainaut, [Bases de données et modèles de calcul : Outils et
>     méthodes pour
>     l\'utilisateur](https://projects.info.unamur.be/~dbm/mediawiki/index.php?title=LIBD:Ouvrages),
>     Dunod, 2004
> -   SQLiteTutorial : <https://www.sqlitetutorial.net/>
> -   [sqlite3 - DB API 2.0 Interface for SQLite
>     databases](https://docs.python.org/3/library/sqlite3.html)
> -   [SQL As Understood BY SQLite](https://sqlite.org/lang.html)
> -   [SQLite documentation](https://sqlite.org/docs.html)
> -   [w3schools.com\'s SQL Tutorial](https://www.w3schools.com/../sql/)

:::: note
::: title
Note
:::

Méfiez-vous des injections SQL

Avant de terminer, nous devons malheureusement attirer votre attention
sur le problème des attaques par [Injection
SQL](https://realpython.com/prevent-python-sql-injection/). Lorsque
l\'on développe un serveur web qui utilise une base de données SQL, il
faut y être très attentif. Une telle attaque peut se produire lorsqu\'un
client qui maîtrise parfaitement SQL interagit avec un serveur développé
par un programmeur débutant qui n\'a pas pris toutes les protections
nécessaires.

Dans nos exemples avec `SELECT`, nous avons utilisé les formes
recommandées par les auteurs de `sqlite3`. Celles-ci permettent de
passer des valeurs de variables à la requête `SELECT` sans risquer
d\'attaque par injection SQL. Une discussion détaillée de ces attaques
sort du cadre de ce cours, vous pouvez consulter un document tel que
[Preventing SQL Injection
Attacks](https://realpython.com/prevent-python-sql-injection/) si vous
souhaitez en savoir plus.
::::

> Hainaut Dunod schools com Tutorial d\'identifiant d\'identifiants


::: {#ref-projet1}
:::

> crashé anonymisée d\'INGINIOUS téléchargeable tutoriel l\'UCLouvain
> l\'Internet l\'URL l\'HyperText grading frontend

Ce chapitre présente le projet dans sa globalité avant de se focaliser
sur la phase 1. Il se basera sur l\'architecture git et coolify de la
phase 0, bien que vous puissiez tout remplacer, et sera constitué de 3
phases au total.

# Une application d\'étude de la mobilité en Wallonie et à Bruxelles

Dans ce projet vous utiliserez les données des capteurs Telraam. Le
Telraam utilise une caméra collée à une fenêtre qui donne sur la rue et
un algorithme de vision par ordinateur pour compter le nombre de
voitures, piétons, cyclistes et poids lourds. Toutes les heures, le
capteur renvoie le nombre d\'objets détectés et leurs vitesses agrégées
à [Telraam.net](telraam.net).

Telraam offre une API pour questionner ces bases de données et extraire
ces informations. Vous n\'utiliserez cependant pas l\'API, nous avons
extrait pour vous les données (voir ci-dessous).

Vous allez créer un site web qui permettra de visualiser ces données, à
la manière de telraam.net, et implémenter une série de fonctionnalités.

# Organisation du projet

La réalisation du projet nécessite l\'apprentissage d\'un petit ensemble
de concepts qui seront introduits en cours et en TP. Cependant ce cours
reste un cours de projet, vous devrez aller plus loin par vous-même en
utilisant la documentation.

Nous verrons notamment :

> -   les bases du fonctionnement du world-wide web, voir
>     `ref-web`{.interpreted-text role="ref"}
> -   les bases de l\'HyperText Markup Langage (HTML) qui est utilisé
>     pour écrire les pages disponibles sur un serveur web, voir
>     `ref-html`{.interpreted-text role="ref"}
> -   les bases de SQL et la façon dont on peut interagir avec une base
>     de données SQL en python, voir `ref-chap-sql`{.interpreted-text
>     role="ref"}
> -   les bases pour utiliser la librairie `chart.js` pour produire
>     facilement de belles visualisations.
> -   le framework Flask qui permet d\'implémenter facilement des sites
>     web interactifs en python, voir `ref-flask`{.interpreted-text
>     role="ref"}

Le projet se fera en 3 phases :

> -   Phase 1, celle-ci. Intégration et affichage de la base de données.
> -   Phase 2, utilisation de tests unitaires.
> -   Phase 3, visualisations et site complet.

# Phase 1 : Intégration et affichage de la base de données

Nous avons extrait pour vous les données de Telraam. Les données sont
présentes dans un gros fichier CSV.

Voici la liste des colonnes du fichier CSV

> -   **nom_de_ville** : il s\'agit du nom de la ville
>
> -   **code_postal** : le code postal correspondant à la ville
>
> -   **nom_de_rue** : nom de la rue où l\'observation a été effectuée
>
> -   **rue_id** : id de la rue
>
> -   **date** : la date et l\'heure du début de l\'observation, les
>     observations durent 1h
>
> -   **lourd** : le nombre de véhicules \"lourds\" qu\'une voiture qui
>     a été observée en une heure. \"Lourd\" désigne tous les véhicules
>     plus grands qu\'une voiture.
>
> -   **voiture** : le nombre de voitures
>
> -   **velo** : nombre de vélos observés
>
> -   **pieton** : nombre de piétons observés
>
> -   
>
>     **histogramme_0_a_70plus** : un tableau de taille 8, chaque entrée décrit la proportion d\'usagers de la route se déplaçant à une vitesse donnée. Les vitesses sont regroupées par tranche de 10km/h :
>
>     :   | array\[0\] = 0-10km/h
>         | array\[1\] = 10-20km/h
>         | \...
>         | array\[7\] = 70km/h+
>
> -   **histogramme_0_a_120plus** : même idée, mais avec des tranches
>     plus précises de 5 km/h
>
> -   **v85** : il s\'agit d\'une estimation de la limite de vitesse qui
>     est respectée par 85% des usagers de la route (15% des usagers
>     dépassent cette vitesse). Cette valeur est absente si aucune
>     usagers n\'a été observé.

**La colonne v85 est la seule pouvant contenir des valeurs vides.**

**Les colonnes lourd, voiture, pieton et velo peuvent contenir des
valeurs à virgule, cela est lié au fait que certaines caméras ne sont
pas toujours actives**, mais avoir un nombre de piétons avec une
décimale n\'a pas de sens. Prenez ceci en compte dans votre schéma et la
transformation des données (voir ci-dessous).

Un exemple de ligne est donné ici :

> | Liege,
> | 4000,
> | Avenue Rogier,
> | 9000003524,
> | 2022-12-16T09:00:00.000Z,
> | 81.2030075188,
> | 601.9334049409,
> | 208.8077336198,
> | 46.4017185822,
> | 
> | \[28.9079229122, 35.9743040685, 21.4132762313,
> | 8.7794432548, 2.9978586724, 1.0706638116, 0.0, 0.8565310493\]\",
> | 
> | \[13.0620985011, 15.8458244111, 17.3447537473, 18.6295503212,
> | 12.4197002141, 8.9935760171, 5.7815845824, 2.9978586724,
>   1.9271948608,
> | 1.0706638116, 0.8565310493, 0.2141327623, 0.0, 0.0, 0.6423982869,
> | 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.2141327623, 0.0, 0.0, 0.0\]\",
> | 
> | 27.0

Le fichier CSV complet est accessible sur moodle.

Nous n\'avons extrait qu\'un nombre limité de rues et d\'observations.
Si vous désirez ajouter des villes et rues pour les besoins de votre
fonctionnalité particulière, vous pouvez le demander à votre
assistant-référent.

Bien que vous puissiez créer une unique grosse table qui contient ces
données, cela serait extrêmement inefficace pour toutes les raisons vues
en cours.

Cette phase comporte une étape intermédiare, où vous devrez envoyer
votre schéma de base de données sur INGInious.

Ensuite, vous devrez implémenter quelques fonctionnalités basées sur le
SQL dans votre site.

Rappels:

:   -   Chaque groupe **DOIT** réaliser son travail en utilisant la
        [Forge UCLouvain\<https://forge.uclouvain.be\>]{.title-ref} qui
        utilise la plateforme GitLab et le gestionnaire de version Git.
    -   Toutes modification du code (excepté les corrections triviales)
        doit se faire à travers une merge request, qui a été reviewé par
        un membre du groupe.
    -   Pensez à organiser votre GitLab proprement et utilisez des
        messages de commit clairs (effectuez des commits régulièrement).
    -   Votre dépôt doit être privé. Invitez votre assistant-référent
        comme contributeur.

# Partie 1

Nous vous demandons d\'imaginer un schéma - c\'est-à-dire une série de
tables et leurs relations - qui permette:

> -   Un schéma plus logique. Les rues et les villes ont une hiérarchie
>     naturelle.
> -   Éviter la redondance des données. Par exemple ne pas dupliquer le
>     nom des rues partout, ce qui prend de l\'espace. Enlevez aussi
>     toute information qui peut être re-calculée.
> -   Ajouter de l\'information: pour chaque ville, le nombre
>     d\'habitants. Vous devez trouver par vous-même un nombre correct.

Dans ce schéma, nous souhaitons voir pas seulement les tables, mais
aussi toutes les contraintes possibles, c\'est-à-dire que chaque clé
primaire et chaque clé étrangère doivent être précisées.

Une série de tâches
[INGInious](https://inginious.info.ucl.ac.be/course/LINFO1002/schema_0)
ont été crées pour vous guider dans la réflexion.

Vous devez avoir terminé une soumission complète du schéma le jour avant
le TP4 afin de pouvoir en discuter au TP4. Mais nous vous conseillons de
le terminer au plus tôt afin de commencer la partie 2 au plus vite.

**Les deadlines sont données sur Moodle !**

# Partie 2

Intégrez ensuite le schéma dans votre site Flask. Dans l\'usine à
application, le CSV sera utilisé directement pour remplir la base de
données.

Vous devrez créer un menu, qui permettra d\'accéder aux pages de votre
site.

Il comportera au moins les pages suivantes :

-   Une page d\'acceuil.
-   Une seule page que présente l\'équipe, en agrégeant les informations
    de la phase zéro.
-   Une page présente des statistiques. **En utilisant des requêtes SQL
    pour effectuer les opérations mathématiques tel que des sommes ou
    des comptages**:
    -   Le nombre d\'entrées par table, selon le schéma discuté
        précédemment.
    -   Le nombre de rues par villes.
    -   Afficher le top des villes les plus cyclables en prenant en
        compte le nombre d\'habitants.
-   Une page de requête qui permet:
    -   De choisir dans un menu déroulant une ville. Après sélection la
        proportion de piétons, cyclistes, \... pour la ville
        sélectionnée sera affichée.
    -   De choisir, pour la ville sélectionnée une rue. Après sélection
        de la rue, affichera la proportion de piétons, cyclistes, \...
        par jours de la semaine (Lundi, Mardi, \...).

Les listes faites au TP1 et TP3 peuvent être supprimées ou déplacée dans
une page de manipulation de la base de données qui est cachée (par
exemple /admin), communément appellée \"backend\".

La partie 2, et donc la phase 1 complète, est à terminer pour le 7 Mars
à 18H (LLN) et le 8 Mars à 18H (Charleroi). Le site doit être en ligne
avec la dernière version du code. Vous devez également faire un
[tag]{.title-ref} git, qui va marquer le dernier commit comme celui du
code final. Pour cela, utilisez [git tag phase1 && git push
phase1]{.title-ref}. Vérifiez que ce tag est disponible sur l\'interface
de la Forge.

# Rapport

Sur Moodle, vous remettrez un rapport qui répond aux critères
ci-dessous.

# Critères d\'évaluation

Rapport :

> -   Le rapport est clair, complet mais concis.
> -   Le rapport présente les fonctionnalités implémentées.

Site :

> -   Le site fonctionne et est en ligne
> -   Le design est réfléchit, le site est navigable, élégant, épuré
> -   Le site est résistant à l\'utilisateur : il n\'y a pas de crash,
>     d\'injections SQL, \... Présenter un site avec une faille de
>     sécurité mènera à un malus conséquent.

Documentation du code :

> -   Le code est commenté

SQL :

> -   Le groupe a présenté un schéma sensé le jour avant le TP.
> -   Le schéma final présenté en partie 1 est correct.
> -   Les requêtes SQL sont correctes.
> -   Les requêtes SQL sont élégantes, directes et efficaces. Elles ne
>     retournent pas de données qui ne seront pas utilisées par le
>     contrôleur.

Git :

> -   L\'ensemble des modifications importantes ont été faites en
>     utilisant des merge request.
> -   Les merge request ont fait l\'objet de review systématiques.

Code :

> -   Le code est correct.
> -   Le code est structuré. L\'architecture MVC est respectée.
> -   Les templates HTML sont propres. Les données paramétrables sont
>     passées par l\'application, et pas codées en dure.

Travail de groupe :

> -   L\'évaluation du groupe se fera via un module dynamo sur Moodle,
>     cloturé 2 jours après la soumission. Une pénalité sera appliquée
>     pour les membres qui n\'y répondent pas.

Pour rappel, la phase 1 dans son ensemble compte pour 15% de la note
finale. Les deadlines sont données sur Moodle.

# Chapitre 6 : Travaux Pratiques #3 : Flask avec une base de donnée {#ref-tp-flask-dynamic}

Ce chapitre est votre troisième séance de travaux pratiques qui sera
suivie en S3. Vous créerez votre seconde application Flask pas-à-pas
pour améliorer votre site web du TP1, mais qui sera cette fois capable
de retenir des villes et des rues en utilisant une base de données.

## Prérequis

Pour comprendre ce TP, il est nécessaire comprendre :

> -   Le concept d\'[arborescence de
>     fichiers](https://wiki.student.info.ucl.ac.be/Documentation/ArborescenceFichiers)
> -   L\'invite de commande, aussi appelée
>     [shell](https://wiki.student.info.ucl.ac.be/Documentation/Shell)
> -   La matière couverte par le premier TP : Flask, le HTML et le CSS.

Prenez le temps de les aborder en cliquant sur les liens si vous n\'êtes
pas à l\'aise, sinon vous serez perdu.

::: {.toctree caption="Contenu du chapitre:"}
tuto_flask_sql/intro.rst tuto_flask_sql/tutorial/database.rst
tuto_flask_sql/tutorial/views_city.rst
tuto_flask_sql/tutorial/views_street.rst
tuto_flask_sql/tutorial/menu.rst tuto_flask_sql/tutorial/next.rst
:::

# Chapitre 7 : Projet phase 1, le SQL

::: toctree
10_db/15_projet1.rst
:::

::: {#ref-test}
:::

> pylint autopep Écrivez feedback framework frameworks l\'implémentation
> illustratifs implémentation précondition préconditions formater wiki
> L\'implémentation

# Comment tester des fonctions en python ?

En parallèle avec l\'apprentissage de l\'écriture de programmes, un
étudiant en informatique doit aussi apprendre à écrire des tests qui
permettent de valider le bon fonctionnement des fonctions et programmes
qu\'il écrit. Ces tests sont extrêmement importants pour avoir confiance
dans la correction d\'un programme. Un programme est souvent composé
d\'un très grand nombre de fonctions qui interagissent entre elles. La
moindre erreur dans une de ces fonctions peut avoir des conséquences
catastrophiques sur le bon fonctionnement du programme.

Il existe de nombreuses stratégies pour tester des programmes de façon
exhaustive. Dans le cadre de ce projet, nous n\'entrerons pas dans tous
ces détails, l\'objectif est de faire une première sensibilisation à
l\'importance des tests et d\'encourager les étudiants à écrire des
tests qui accompagnent leurs programmes.

Souvent, les programmeurs débutants écrivent leurs tests en exécutant
manuellement leurs fonctions avec quelques valeurs d\'entrée et
obs

ervant qu\'elles fonctionnent correctement. D\'autres ajoutent des
appels à `print` dans leur code à certains endroits. Ces approches
peuvent aider à détecter des problèmes simples, mais elles sont à éviter
en pratique. Leur inconvénient majeur est qu\'elles forcent le
programmeur à passer beaucoup de temps pour tester son programme. Comme
celui-ci ou celle-ci manque souvent de temps, les tests sont rarement
exécutés et le code risque fort de ne pas être correct.

Une meilleure approche est de s\'appuyer sur un framework de test qui
permet d\'automatiser les tests. En utilisant un de ces frameworks, il
suffit de taper une commande pour vérifier que l\'ensemble des tests du
programme continuent à s\'exécuter correctement. L\'apprentissage d\'un
tel framework de test prend un peu de temps, mais il offre l\'avantage
de pouvoir facilement éviter les régressions. Une régression est une
modification mineure du code qui provoque une erreur subtile qui n\'est
pas détectée avant que le programme ne soit finalisé. Avant cette
correction, le programme fonctionnait parfaitement et il suffit d\'avoir
changé quelques lignes pour qu\'il se plante lamentablement.

Il existe plusieurs frameworks de test en python. Les plus connus sont
[unittest](https://docs.python.org/3/library/unittest.html), et
[pytest](https://docs.pytest.org/en/latest/). Le wiki de Python contient
une longue liste d\'outils de test:
<https://wiki.python.org/moin/PythonTestingToolsTaxonomy>

Dans la cadre de ce cours, nous nous concentrerons sur unittest, vous
aurez l\'occasion d\'apprendre d\'autres frameworks de test dans le
cadre d\'autres cours d\'informatique dans les prochaines années.
Unittest est décrit en détail dans la documentation python :
<https://docs.python.org/3/library/unittest.html>

Nous utiliserons unittest de façon à vérifier que l\'implémentation
d\'une fonction écrite en python est correcte. .. Dans un second temps,
nous utiliserons les tests à des fins pédagogiques et écrirons de petits
exercices INGInious qui utilisent des tests unitaires écrits en
utilisant unittest pour donner un feedback à des étudiants en
informatique comme vous.

## Tests unitaires simples

Nos premiers tests unitaires avec unittest ont pour objectif de vérifier
qu\'une fonction correspondant à une spécification donnée fourni le
résultat attendu. Commençons par quelques fonctions mathématiques
simples. Notre premier exemple est le calcul de la valeur absolue. Même
si python inclut la fonction `abs()`, nous pouvons redéfinir une
fonction équivalente nous-mêmes dans l\'exemple ci-dessous.

::: {.literalinclude language="python" linenos=""}
../python/abs.py
:::

L\'implémentation de la fonction `my_abs()` ne nécessite pas de
commentaire particulier. Par contre, nous pouvons regarder comment cette
fonction est testée en utilisant unittest. Tout d\'abord (première ligne
du script), il faut importer le module unittest de façon à pouvoir
utiliser ses fonctionnalités.

Avec unittest, un test unitaire s\'écrit en étendant la classe
`unittest.TestCase` et en ajoutant les méthodes permettant de tester les
nouvelles fonctions. Dans le cas du calcul de la valeur absolue, nous
avons ajouté la fonction `test_my_abs()`. Celle-ci vérifie que la
fonction `my_abs()` retourne le résultat attendu pour trois valeurs
différentes de son argument:

> -   `my_abs(0)` retourne `0`
> -   `my_abs(1)` retourne `1`
> -   `my_abs(-1)` retourne `1`

Avec unittest, cette vérification se fait en utilisant un ensemble
d\'assertions. unittest définit dans la classe `TestCase` les assertions
suivantes:

> -   `assertEqual(a, b)` vérifie que `a == b`
> -   `assertNotEqual(a, b)` vérifie que `a != b`
> -   `assertTrue(x)` vérifie que le booléen `x` s\'évalue à `True`
> -   `assertFalse(x)` vérifie que le booléen `x` s\'évalue à `False`
> -   `assertIs(a, b)` vérifie que la référence `a` est le même objet
>     que la référence `b`
> -   `assertIsNot(a, b)` vérifie que la référence `a` n\'est pas le
>     même objet que la référence `b`
> -   `assertIsNone(x)` vérifie que la référence `x` est `None`
> -   `assertIsNotNone(x)` vérifie que la référence `x` n\'est pas
>     `None`
> -   `assertIn(a, b)` vérifie que `a` est présent dans la liste `b`
> -   `assertNotIn(a, b)` vérifie que `a` n\'est pas présent dans la
>     liste `b`
> -   `assertIsInstance(a, b)` vérifie que `a` est une instance de la
>     classe `b`
> -   `assertNotIsInstance(a, b)` vérifie que `a` n\'est pas une
>     instance de la classe `b`

Ces méthodes vérifient leurs arguments en provoquant une erreur qui est
reportée par unittest si une des assertions est invalidée. Pour
comprendre leur utilisation, revenons à notre exemple. Grâce au
framework unittest, il est facile d\'exécuter les tests en ligne de
commande:

``` console
#python -m unittest -v abs
test_my_abs (abs.TestAbs) ... ok

----------------------------------------------------------------------
Ran 1 test in 0.002s

OK
```

La suite de test a exécuté les trois tests définis ci-dessous. Modifions
maintenant l\'implémentation de la fonction `my_abs()`.

::: {.literalinclude language="python" linenos=""}
../python/abs2.py
:::

L\'exécution de la suite de tests nous indique directement la régression
et le message d\'erreur nous montre l\'assertion qui a échoué. Il ne
nous reste plus qu\'à corriger le code.

``` console
#python -m unittest -v abs2
test_my_abs (abs2.TestAbs) ... FAIL

======================================================================
FAIL: test_my_abs (abs2.TestAbs)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "abs2.py", line 29, in test_my_abs
    self.assertEqual(my_abs(-1), 1)
AssertionError: -1 != 1

----------------------------------------------------------------------
Ran 1 test in 0.002s

FAILED (failures=1)
```

La fonction valeur absolue est un fonction très simple à écrire et à
tester.

### Médiane

D\'autres fonctions sont plus compliquées. Prenons l\'exemple classique
du calcul de la médiane entre trois nombres `a`, `b` et `c`. Vous avez
proposé une solution pour calculer cette médiane au début de votre
apprentissage de la programmation.

Voici quelques exemples de solutions proposées par les étudiants.

``` python
# Solution 1
if (a<= c and c<=b) or (b<=c and c<=a):
    median = c
elif (b<=a and a<=c) or (c<=a and a<=b):
    median = a
else:
    median = b
return median
```

``` python
# Solution 2
if a>=b and a<=c:
    median=a
elif b>=a and b<=c:
    median=c
elif c>=a and c<=b:
     median=c
return median
```

``` python
# Solution 3     
median = a
if a < b < c and c < b < a :
     median = b
if b < c < a and a < c < b :
     median = c
return median
```

Seule la première est correcte, les autres sont erronées. Même si le
calcul de la médiane est un calcul simple, on peut rapidement se tromper
dans l\'imbrication des différents tests ou dans les conditions logiques
et ces erreurs ne sont ni faciles à détecter ni à corriger. Pour tester
qu\'une telle fonction est correcte, différentes approches sont
possibles.

Lorsque l\'on demande à un programmeur débutant de tester sa solution,
il fait en général quelques essais rapides et se convainc rapidement du
bon fonctionnement de sa solution. Prenons quelques exemples
illustratifs en supposant que la fonction est `mediane(a,b,c)`.
Pouvez-vous déterminer laquelle des assertions suivantes va permettre de
détecter une erreur dans les solutions 2 et 3 ?

> -   `self.assertEqual(mediane(2,2,2), 2)`
> -   `self.assertEqual(mediane(1,2,3), 2)`
> -   `self.assertEqual(mediane(6,4,5), 5)`
> -   `self.assertEqual(mediane(8,-3,11), 8)`

Ces quatre assertions sont-elles suffisantes pour avoir la garantie que
la fonction `mediane(a,b,c)` fonctionne correctement ?

Malheureusement non. Pour s\'en rendre compte, considérons une
implémentation un peu longue de la fonction `mediane`.

``` python
def mediane(a,b,c):
    if a <= b and b <= c:
       return b
    if a <= c and c <= b:
       return c
    if b <= a and a <= c:
       return a
    if b <= c and c <= a:
       return c
    if c <= b and b <= a:
       return b
    if c <= a and a <= b:
       return a
```

Lorsque l\'on exécute les quatre tests définis ci-dessus sur cette
version de la fonction `mediane`, quelles sont les parties du code qui
sont vraiment exécutées ? Pour répondre à cette question, il faudrait
exécuter pas à pas le programme et voir quelles branches il exécute.
Manuellement, ce serait fastidieux. Heureusement, il existe des
programmes qui vous permettent de vérifier quelles sont les lignes qui
sont exécutées.
[Coverage.py](https://coverage.readthedocs.io/en/coverage-5.0.3/) est un
de ces outils. Il s\'installe comme tout module python et interagit
directement avec les tests unitaires unittest. Il mesure quelles lignes
sont exécutées durant un test unitaire et présente un rapport en format
HTML qui indique clairement la partie du code qui est testée par les
tests et celle qui ne l\'est pas. Si une partie de votre code n\'est pas
exécutée durant vos tests, c\'est probablement une indication que
ceux-ci ne sont pas suffisamment exhaustifs.

``` console
# coverage run -m unittest mediane3
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
# coverage html
# browser htmlcov/index.html 
```

`Coverage.py` s\'exécute en ligne de commande. La figure ci-dessous
montre le résultat obtenu avec le fichier
`../python/mediane3.py`{.interpreted-text role="download"}

![](/figures/coverage-mediane3.png)

Malheureusement, la réponse est non. Dans le cas du calcul de la
médiane, la bonne façon de tester correctement le bon fonctionnement de
cette fonction est testée dans toutes les combinaisons possibles des
valeurs des variables `a`, `b` et `c`. Comme le résultat dépend
uniquement des relations d\'ordre entre les différentes valeurs des
variables entières, il faut écrire des assertions dans lesquelles les
valeurs des variables sont telles que :

> -   `a < b < c`
> -   `a < c < b`
> -   `b < a < c`
> -   `b < c < a`
> -   `c < a < b`
> -   `c < b < a`

Avec ces six tests, on couvre toutes les combinaisons d\'arguments
possibles. Écrivez un test unitaire qui permet de valider
l\'implémentation correcte du calcul de la médiane.

Cette approche exhaustive dans laquelle on essaye toutes les
combinaisons de valeurs possibles est intéressante, car elle permet
d\'avoir confiance dans la correction de l\'implémentation, mais il
n\'est pas toujours facile de définir les tests à réaliser. Il existe
des théories qui permettent de produire les tests à réaliser pour
vérifier une fonction dont on connaît la spécification, mais celle-ci
sortent largement des objectifs d\'un projet de première année. En
outre, le nombre de tests à réaliser peut rapidement devenir très grand
et il est en pratique difficile de les écrire. Pour s\'en convaincre, il
suffit de réfléchir à la façon dont on peut tester la fonction qui prend
comme argument un tableau contenant un nombre impair d\'entiers et
retourne son élément médian.

``` python
def mediane(tab):
"""
@pre: tab est un tableau contenant un nombre impair d'entiers
@ post: retourne l'element median de ce tableau
"""      
```

Il n\'est plus possible de tester cette fonction de façon exhaustive.
Une approche raisonnable est de générer des tableaux contenant des
nombres aléatoires et de vérifier que la fonction retourne le bon
résultat dans tous les cas.

::: {.literalinclude language="python" linenos=""}
../python/mediantab.py
:::

Ces tests unitaires sont l\'occasion de montrer que les assertions de la
classe `unittest.TestCase` prennent un troisième argument très utile en
pratique: une chaîne de caractères à afficher lorsqu\'une assertion
n\'est pas vérifiée. Ces messages d\'erreur sont très utiles pour
corriger les erreurs lorsque celles-ci sont détectées.

Prenons un autre exemple aussi extrait des exercices du premier cours
d\'informatique, le calcul du plus grand diviseur d\'un entier positif.
Cet exercice était proposé comme suit:

``` text
The Greatest Divisor of a number a is the biggest number ( except a itself) such that
   the division of a by this natural is an entire division.

Since 0 is divisible by any natural this may cause some problems if you will look
 for the bigger one, so we expect you to return None.

1 shall also return None.

Recall that the operator % returns the remainder of the Euclidian division.
```

Cette question est intéressante, car elle combine un calcul et des cas
limites. Si l\'argument est `0` ou `1`, la fonction doit retourner
`None`. Sinon, elle doit retourner le plus grand diviseur. Voici
quelques exemples de codes (pas nécessairement corrects) proposés par
des étudiants sur INGInious et quelques tests unitaires.

::: {.literalinclude language="python" linenos=""}
../python/pgd.py
:::

Les assertions supportées par la classe `unittest.TestCase` permettent
de couvrir la plupart des besoins. Il en existe d\'autres que celles qui
ont été présentées précédemment, dont:

> -   `assertAlmostEqual(a, b)` qui permet de vérifier si le réel `a`
>     est \"proche\" du réel `b`. Lorsqu\'un fonction réalise un calcul
>     mathématique, celui-ci peut être entaché d\'erreurs qui dépendent
>     de la façon dont le calcul a été écrit. Le cours de méthodes
>     numériques décrit des techniques qui permettent de minimiser ces
>     pertes de précision, mais il est impossible de les éviter. Si une
>     de vos fonctions retourne un réel, préférez
>     `assertAlmostEqual(a, b)` à `assertEqual(a, b)`. Vous pouvez
>     utiliser les arguments optionnels `place` ou `delta` pour
>     spécifier le niveau de précision que vous souhaitez.
> -   `assertNotAlmostEqual(a, b)`
> -   `assertGreater(a, b)`
> -   `assertGreaterEqual(a, b)`
> -   `assertLess(a, b)`
> -   `assertLessEqual(a, b)`

Il est aussi possible de définir des tests personnalisés en réutilisant
`assertTrue` avec une expression booléenne bien choisie. Par exemple, si
on veut vérifier que le résultat de la fonction `f` appliquée à `7` est
pair, il suffit d\'écrire `assertTrue(f(7)%2==0)`. Lorsqu\'une assertion
existe dans `unittest.TestCase`, il est préférable de l\'utiliser cas
cela rend les tests plus faciles à lire.

# Quelques règles de bonne pratique

L\'écriture d\'un ensemble pertinent de tests unitaires pour une
fonction donnée s\'apprend par la pratique. Il est difficile de lister
des règles précises à suivre, mais voici quelques règles de bonne
pratique qui peuvent s\'avérer utile.

Considérons tout d\'abord des fonctions qui n\'ont pas d\'effet de bord,
c\'est-à-dire des fonctions qui se contentent de lire leurs arguments
(sans modifier leurs valeurs) et retournent un résultat. Pour ces
fonctions, il est important de bien analyser les préconditions et de
prendre en compte les cas suivants:

> -   si la fonction prend des arguments entiers, tester avec `0` ainsi
>     que des entiers positifs et négatifs qui respectent les
>     préconditions
> -   si la fonction prend une chaîne de caractères comme argument, voir
>     comment elle réagit avec un chaîne vide, une chaîne contenant des
>     caractères quelconques, une chaîne contenant des mots séparés par
>     des espaces, virgules ou des retours à la ligne, voir si les
>     chiffres ou caractères spéciaux sont bien supportés, voir s\'il
>     est possible de traiter une très longue chaîne de caractères, \...
> -   si la fonction prend comme argument une liste, il est intéressant
>     de tester une liste vide, une liste avec un seul élément, une
>     liste contenant des éléments tous différents, une liste contenant
>     plusieurs fois le même élément, \... Si le traitement fait dans la
>     fonction dépend de l\'ordre dans lequel les éléments sont placés
>     dans la liste, `random.shuffle()` peut s\'avérer très utile pour
>     produire des variations d\'un même liste dans un ordre différent.
>     Si la fonction doit traiter des éléments se trouvant dans une
>     liste, pensez à placer ces éléments au début, au milieu ou à la
>     fin de la liste pour vérifier que la fonction traite bien tous les
>     cas possibles.
> -   si la fonction traite des fichiers, il faut penser à utiliser des
>     fichiers vides, valides et invalides. Dans ce cas, on préférera
>     généralement créer tous les fichiers au début de la suite de test
>     en utilisant la méthode `setUp` et on veillera à les supprimer
>     dans la méthode `tearDown`.

# Outils d\'aide à l\'écriture de programmes lisibles

Lorsque l\'on écrit des programmes ou des suites de test en groupe, il
est important d\'adopter les mêmes conventions d\'écriture de façon à
faciliter la lecture du code par les différents membres du groupe.
Différentes communautés de programmeurs open-source ont développé des
règles de bonne pratique pour l\'écriture de programmes, l\'utilisation
de l\'indentation, des espaces, etc. La communauté python a codifié ces
règles de façon très précise dans des documents tels que [PEP 8 \--
Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/).

Certains éditeurs de programme python respectent ces conventions par
défaut ou vous aident à le faire. En outre, différents outils
open-source peuvent vous aider à adopter des conventions de codage
uniformes.

Un premier outil est [autopep8](https://pypi.org/project/autopep8/). Il
permet de formater automatiquement un code python de façon à ce qu\'il
respecte le plus possible les conventions standard de codage en python.

Un deuxième outil est [pylint](https://www.pylint.org/). Il est capable
d\'analyser votre code python pour voir si vous respectez les règles
définies dans PEP8, mais il comprend également de nombreux tests qui
détectent des erreurs liées une mauvaise utilisation des variables, la
présence de code qui n\'est pas exécuté, \...


# Analyse statique {#ref-static}

Comme vous l\'avez vu dans le premier cours de programmation consacré au
langage Python, celui-ci est un langage non-typé. Lorsque vous écrivez
une fonction en Python, et contrairement à d\'autres langages de
programmation tels que Java, ou C que vous verrez l\'année prochaine,
Python ne vous oblige pas à préciser le type des arguments de la
fonction et le type de résultat que celle-ci va retourner. Cette
flexibilité est pratique dans certains cas. Par exemple, supposons que
vous devez écrire une fonction qui permet de déterminer le nombre de
fois qu\'une valeur est présente dans une liste.

En Python3, cette fonction peut s\'écrire comme suit.

``` python
def presences(val, tab):
"""
@pre: tab est un tableau 
      val une valeur d'un type quelconque
@ post: retourne le nombre de fois que val est repris dans tab
"""
count = 0
for e in tab:
    if e==val:
        count += 1
return count
```

Elle peut s\'utiliser avec n\'importe que type de données comme illustré
ci-dessous.

``` python
print (presences(1, [2,3,4]) )  # affiche 0
print (presences('a', [2,3,4]) )  # affiche 0   
print (presences('a', [2,'a',4,'a','b']) ) # affiche 2
print (presences(['a'], [2,['a'],4,('a'),'b']) ) # affiche 1    
```

Certains considèrent que cette possibilité de supporter n\'importe quel
type de données comme étant un des avantages importants de Python.
D\'autres et notamment ceux qui doivent gérer des codes de très grande
taille sont parfois plus mitigés. La liberté offerte par Python
s\'accompagne parfois de bugs difficiles à détecter et qui sont liés à
une utilisation incorrecte de certaines fonctions qui n\'est détectée
qu\'à l\'exécution et provoque des erreurs qui affectent les
utilisateurs. La société Dropbox par exemple utilise plusieurs millions
de lignes de code écrit en Python. Elle a d\'ailleurs engagé
l\'inventeur de Python pendant plusieurs années. Dans un [blog publié
fin
2009](https://blogs.dropbox.com/tech/2019/09/our-journey-to-type-checking-4-million-lines-of-../python/),
les informaticiens de Dropbox expliquent comment ils ont petit à petit
converti leur code Python de façon à forcer les développeurs à indiquer
clairement les types de données qu\'ils utilisent. Cela réduit la
liberté du développeur, mais permet d\'éviter de très nombreux bugs.
Cette approche est implémentée par l\'utilitaire
[mypy](https://mypy.readthedocs.io/en/stable/) et supportée par les
versions récentes de Python. Elle s\'appuie sur le typage statique, une
technique utilisée par de nombreux langages de programmation et
compilateurs.

Python3 support plusieurs types de données primitifs dont les entiers,
les booléens, les réels, les chaînes de caractères, \... Chacun de ces
types est identifié par un mot-clé spécifique.

> -   `int` : nombre entier
> -   `float` : nombre réel en virgule flottante
> -   `bool` : booléen (`True` ou `False`)
> -   `str` : chaîne de caractères en représentation Unicode
> -   `bytes` : chaîne de d\'octets
> -   `object` : objet Python quelconque (classe mère de tous les
>     objets)

Il est possible de combiner ces différents types de données primitifs
dans des listes, tuples, dictionnaires, \...

> -   `List[str]` : une liste contenant uniquement des chaînes de
>     caractères
> -   `Tuple[int, float]` : un tuple contenant un entier et un réel
> -   `Tuple[int, ...]` : un tuple contenant un nombre quelconque
>     d\'entiers
> -   `Dict[str, float]` : un dictionnaire qui fait correspondre une
>     chaîne de caractères à un réel

D\'autres structures de données sont définies dans la documentation de
[mypy](https://mypy.readthedocs.io/en/stable/) .

Grâce à ces identifiants de types de données, il est possible d\'annoter
les signatures des fonctions de façon à indiquer le type des arguments
qu\'elle reçoit et les types de résultats qu\'elle retourne. Commençons
par repartir de la fonction qui calcule la valeur absolue d\'un entier.
Avec le typage statique, celle-ci doit s\'écrire:

``` python
def my_abs(i: int) -> int:
 """
 @pre: i est un entier
 @ post: retourne la valeur absolue de l'entier i
 """
 if i <= 0:
     return -i
 return i
```

Les modifications se retrouvent dans la signature de la fonction qui
inclus maintenant le type de son argument et le type de son résultat.
Pour comprendre l\'intérêt du typage statique, considérons un étudiant
qui essaie d\'utiliser la fonction `my_abs` de la façon suivante :

``` python
print ( my_abs(2) )
print ( my_abs(-2.5) )
print ( my_abs( [-2] ) )
print ( my_abs( "-2" ) )
```

Lorsque ces différentes lignes sont exécutées, l\'interpréteur Python
affiche les messages suivants:

``` python
2
2.5
Traceback (most recent call last):
  File "../python/abstype.py", line 32, in <module>
    print ( my_abs( [-2] ) )
  File "../python/abstype.py", line 12, in my_abs
    if i <= 0:
  TypeError: '<=' not supported between instances of 'list' and 'int'
```

Les deux premières lignes sont correctes. Ensuite, Python affiche des
messages d\'erreur car la fonction n\'est pas prévue pour fonctionner
avec une liste, un tuple ou une chaîne de caractères. Si de telles
erreurs sont détectées lors de l\'exécution du programme par
l\'utilisateur, c\'est gênant car en général celui-ci n\'a aucune idée
de l\'origine de l\'erreur et ne sait pas la corriger. Dans un exercice
INGInious, c\'est aussi une source de nombreuses erreurs pour des
étudiants. Le typage statique permet de valider les types des arguments
et des valeurs de retour des fonctions. Dans l\'exemple ci-dessous,
`mypy` indique les erreurs suivantes:

``` python
../python/abstype.py:2: error: Argument 1 to "my_abs" has incompatible type "float"; expected "int"
../python/abstype.py:3: error: Argument 1 to "my_abs" has incompatible type "List[int]"; expected "int"
../python/abstype.py:4: error: Argument 1 to "my_abs" has incompatible type "str"; expected "int"
```

Certaines fonctions ne retournent pas de résultat. Dans ce cas, il faut
indiquer dans leur signature qu\'elles retournent `None`.

``` python
def print_abs(i: int) -> None:
 """
 @pre: i est un entier
 @ post: affiche la valeur absolue de l'entier i
 """
 if i <= 0:
     print (-i)
 print (i)
```

Il est aussi possible de spécifier des listes ou des dictionnaires comme
arguments en indiquant les types primitifs que ces arguments
contiennent.

``` python
def presences(val : int, tab: List[int]) -> int :
 """
 @pre: tab est une liste d'entiers 
       val un entier
 @ post: retourne le nombre de fois que val est repris dans tab
 """
 count = 0
 for e in tab:
     if e==val:
         count += 1
 return count
```

Dans certains cas, il est nécessaire d\'écrire des fonctions qui peuvent
supporter des arguments de plusieurs types différents. Dans le cas de
notre exemple avec la valeur absolue, cette fonction est définie pour
les entiers et les réels. Il est possible d\'indiquer à `mypy` qu\'une
fonction peut recevoir un entier ou un réel via le mot clé `Union`.
Celui-ci s\'utilise comme dans l\'exemple ci-dessous.

``` python
def abs2(i: Union[int,float] ) -> Union[int,float]:
 """
 @pre: i est un nombre
 @ post: retourne la valeur absolue de l'entier i
 """
 if i <= 0:
     return -i
 return i
```

Cette fonction est validée par `mypy` et s\'utilise avec des réels ou
des entiers.

``` python
print ( abs2 (-2) )     # affiche 2
print ( abs2 (-2.3) )   # affiche 2.3
```

Le typage statique facilite l\'écriture du code de test et permet
d\'être sûr que l\'utilisateur utilise bien les arguments du bon type.
Cela évite de devoir vérifier manuellement que les préconditions (au
niveau des types de données) sont bien respectées. `mypy` a été intégré
dans le fichier `../python/inginious/run`{.interpreted-text
role="download"} il vous suffit de mettre à jour ce fichier pour
l\'utiliser dans votre projet. Le manuel officiel de `mypy` est
disponible via <http://mypy.readthedocs.io>.


Ce chapitre présente la phase 2 du projet. Il se basera sur la phase 1,
en ce compris l\'architecture git, coolify, le site web en Flask
utilisant une base de données SQL.

Les deux premières semaines (S5 -\> S7) vous implémenterez des tests
unitaires tel qu\'expliqué ci-dessous. A LLN, le travail et le rapport
est à rendre pour **mardi 21 à 18H**. A Charleroi, pour le **jeudi 23 à
18H**. La troisième semaine (S7 -\> S8) vous ferez une revue par les
pairs (peer-review), c\'est-à-dire la relecture du travail d\'un autre
groupe afin de leurs donner des commentaires pertinants et tester leurs
code et leurs limites. Les commentaires sont à rendre exactement une
semaine plus tard.

Comme d\'habitude, chaque groupe **DOIT** réaliser son travail en
utilisant la [Forge UCLouvain](https://forge.uclouvain.be) qui utilise
la plateforme GitLab et le gestionnaire de version Git. Ceci permettra
de garder une trace des contributions des différents membres du groupe.
Pensez à organiser votre Git proprement et utilisez des messages de
commit clairs.

# Une application testée

On vous demande d\'implémenter et d\'intégrer à votre application web la
fonctionnalité suivante :

> -   Afficher le ratio du nombre de vélos par ans les jours de pleine
>     lunes.

On vous demande aussi d\'intégrer des tests pour cette fonctionnalité
ainsi que pour les requêtes de la phase 1.

Pour se faire vous devrez implémenter les fonctions suivantes dans un
fichier dédié (par exemple, `moon_utils.py`) :

> -   `age(datetime: date) -> Decimal` : qui retourne pour `date`
>     (heure, minute, jour, mois, année selon le format datetime) la
>     phase de la lune correspondante en utilisant par exemple
>     [l\'algorithme
>     suivant](https://en.wikipedia.org/wiki/Lunar_phase#Calculating_phase).
>     Comme la précision de cet algorithme dépend de la précision de
>     l\'arithmétique de nombres décimaux, vous devrez utilisez
>     [decimal.Decimal](https://docs.python.org/3/library/decimal.html)
>     pour représenter les nombres décimaux.
> -   `phase(Decimal: age) -> Phase` : qui retourne la valeur appropriée
>     de la classe [Enum](https://docs.python.org/3/library/enum.html)
>     `MoonPhase` pour un `age` donné tel que retourné pour la fonction
>     précédente.

La classe `MoonPhase` (que vous pouvez mettre dans `moon_utils.py`) :

:::: {#id1 .container .literal-block-wrapper .docutils}
::: {.container .code-block-caption}
`mobility/moon_utils.py`
:::

``` python
from enum import Enum

class MoonPhase(Enum):
    NEW_MOON = 0
    WAXING_CRESCENT = 1
    FIRST_QUARTER = 2
    WAXING_GIBBOUS = 3
    FULL_MOON = 4
    WANING_GIBBOUS = 5
    LAST_QUARTER = 6
    WANING_CRESCENT = 7
```
::::

On vous demande également de fournir une classe de test qui testera la
logique de ces différentes méthodes. Pour ce faire, on vous demande
d\'utiliser le module
[unittest](https://docs.python.org/3/library/unittest.html) comme vu en
LSINF1101 et comme rappelé dans le syllabus et au cours. Vous devrez
créer vos fichiers de tests dans un sous-répertoire `tests` et ils
devront respecter la nomenclature `test_*.py` pour que unittest les
découvre automatiquement et où \* correspond à la classe ou au module
testé.

Une classe de tests unitaires hérite de `unittest.TestCase` et porte un
nom logique `*TestCase` correspondant à la classe ou au module testé.
Chaque classe teste une fonctionnalité précise et chaque méthode de test
dans la classe sera nommée en commençant par `test_` comme
`def test_foo(self) :` contenant une série d\'assertions qui vérifient
que pour un input connu (une fixture), l\'output produit est celui
attendu. Un squelette d\'une telle classe ressemblera donc à ceci.

> :::: {#id1 .container .literal-block-wrapper .docutils}
> ::: {.container .code-block-caption}
> `tests/test_moon_utils.py`
> :::
>
> ``` python
> import unittest
> import mobility.moon_utils
> from datetime import datetime
>
> class MoonUtilsTestCase (unittest.TestCase):
>
>     def test_phase(self):
>         my_fixture = datetime(2019, 1, 21, 5, 16, 0)
>         expected = moon_utils.MoonPhase.FULL_MOON
>         # test phase with assert calls
>         self.assertEqual(moon_utils.phase(moon_utils.age(my_fixture)), expected,
>                          msg=f'My error message on pl.f({my_fixture}) different than {expected}')
>
> if __name__ == '__main__':
>     unittest.main(verbosity=2)
> ```
> ::::

Cette classe doit être enrichie et couvrir un maximum de `moon_utils`
(via l\'utilisation de `coverage`).

Ensuite, nous voulons que vous testiez les fonctionalités liées aux
sélections filtrées dans la base de données afin de vous assurer que vos
données sont correctes. Vous devez donc tester les requêtes implémentées
pour la phase 1 du projet. Un tel test est appelé test d\'intégration
car il fait intervenir plusieurs composants de votre application
(notamment ici l\'app et la db) par opposition au test unitaire qui lui
va tester la fonctionnalité d\'une méthode ou une classe dont la logique
est limitée. Voici un template d\'une classe permettant de faire de tels
tests sur une db de test (on ne veut pas risquer d\'interférer avec la
base de données utilisée en production !). L\'exemple est donné dans le
cadre du
[base-project](https://forge.uclouvain.be/linfo1002/base-project).

> :::: {#id1 .container .literal-block-wrapper .docutils}
> ::: {.container .code-block-caption}
> `tests/test_user.py`
> :::
>
> ``` python
> import os
> import tempfile
> import unittest
>
> from mobility import create_app
> from mobility.db import get_db, close_db
> from mobility.user import search_by_email
>
>
> class TestUser(unittest.TestCase):
>
>     def setUp(self):
>         # generate a temporary file for the test db
>         self.db_fd, self.db_path = tempfile.mkstemp()
>         # create the testapp with the temp file for the test db
>         self.app = create_app({'TESTING': True, 'DATABASE': self.db_path})
>         self.app_context = self.app.app_context()
>         self.app_context.push()
>         self.db = get_db()
>
>         # read in SQL for populating test data
>         with open(os.path.join(os.path.dirname(__file__), "schema_test.sql"), "rb") as f:
>             self.db.executescript(f.read().decode("utf8"))
>
>     def tearDown(self):
>         # closing the db and cleaning the temp file
>         close_db()
>         os.close(self.db_fd)
>         os.unlink(self.db_path)
>
>     def test_search_by_email(self):
>         # unit test against the test db.
>         users = search_by_email('test@gmail.com')
>         self.assertEqual(len(users), 1)
>         self.assertEqual(users[0]["email"], 'test@gmail.com')
>
>
> if __name__ == '__main__':
>     unittest.main(verbosity=2)
> ```
> ::::

Notez que la méthode
[setUp](https://docs.python.org/3/library/unittest.html#unittest.TestCase.setUp)
est héritée de `unittest.TestCase`. Elle est exécutée avant chaque test
et permet de travailler avec une db de test neuve à chaque fois. Ici,
une instance de l\'app avec une db de test stockée dans un fichier
temporaire est créée pour chaque test. Vous pouvez mettre les données de
test que vous désirez dans un (ou plusieurs) fichiers sql. Ici dans
`tests/schema_test.sql`.

> :::: {#id1 .container .literal-block-wrapper .docutils}
> ::: {.container .code-block-caption}
> `tests/test_user.py`
> :::
>
> ``` sql
> INSERT INTO users (username, email)
> VALUES
>   ('test', 'test@gmail.com'),
>   ('other', 'other@gmail.com');
> ```
> ::::

La méthode
[tearDown](https://docs.python.org/3/library/unittest.html#unittest.TestCase.tearDown)
est elle aussi héritée de `unittest.TestCase` et permet de nettoyer la
db après chaque test.

Les tests seront finalement automatiquement découvert par unittest. Pour
les lancer, vous pouvez:

> -   Soit utilisez l\'outillage proposé par pycharm. Clic droit sur
>     `tests` puis \"Run \'Python tests in \...\'\". Après avoir
>     installé coverage (pour rappel, `$ pip install coverage` dans
>     votre venv) vous pouvez aussi faire Clic droit sur `tests` puis
>     \"More Run/Debug\" \"Run \'Python tests in \...\' with Coverage\".
> -   Soit directement depuis le terminal dans le venv en supposant que
>     vous êtes à la racine du projet avec
>     `$ python -m unittest discover -v -s ./tests`.

# Rapport

Sur Moodle, vous remettrez un rapport qui répond aux critères
ci-dessous.

# Critères d\'évaluation

Rapport:

-   Le rapport est clair, complet mais concis.
-   Le rapport présente les fonctionnalités implémentées, en particulier
    il détaillera l\'implémentation des phases de la lune, un exemple de
    requête SQL pour afficher les données et les filtrer.
-   Le rapport détaille aussi les stratégies de tests utilisées et le
    taux de coverage.
-   Le rapport décrit le fonctionnement du groupe. Il explique les
    problèmes rencontrés, et les pistes de solutions le cas échéant.

Site:

-   Le site fonctionne et est en ligne
-   L\'intégration des nouvelles fonctionnalités (lunes et filtres de
    données) est complète

Documentation du code:

-   Le code est commenté en utilsant des docstrings tels que présenté au
    cours.

SQL:

-   Au moins un test d\'intégration interagissant avec la db est proposé
-   Une db de test temporaire différent de la db \"de prod\" est
    utilisée dans les tests
-   Les tests sont complets et commentés. Ils ne sont pas triviaux et
    couvrent la logique

Code:

-   Le code est correct.
-   Le code Python de votre suite de tests est clair et compréhensible
-   Le code est structuré. La nomenclature et l\'organisation des
    modules et répertoires présentés dans l\'énoncé sont respectées.

Git:

-   L\'ensemble des modifications importantes a été fait en utilisant
    des merge request.
-   Les merge request ont fait l\'objet de review systématiques.

Pour rappel, la phase 2 dans son ensemble compte pour 15% de la note
finale.


# Comment faire une bonne review

Lors de la phase de peer-review du code, nous vous demandons de vérifier
la qualité et la structure du code de l\'application d\'un autre goupe
d\'étudiant ainsi que de la suite de test. Guidez-vous en répondant aux
questions suivantes :

> -   Le code de l\'application respecte-t-il la structure proposée ?
> -   Les différentes fonctionalités sont-elles dans des fichiers
>     séparés ?
> -   Le code python proposé est-il clair et bien documenté ?
> -   Les noms des variables sont-ils bien choisis ?
> -   Les commentaires sont-ils appropriés et clairs ?
> -   Les tests montrent-ils qu\'ils ont été écrits par des étudiants
>     qui maîtrisent le langage python (utilisation de fonctions, éviter
>     d\'avoir trop de code dupliqué, même si dans des tests unitaires
>     il y a plus souvent du code dupliqué que dans le code normal)
> -   Les test sont-ils complets et corrects ? Si non, proposez dans
>     votre rapport d\'éventuels cas de test supplémentaires en
>     justifiant leur utilité.

Cette analyse prend du temps, mais c\'est important que vous appreniez à
lire du code écrit par d\'autres informaticiens. Dans votre vie
professionnelle, vous devrez beaucoup plus souvent modifier des
programmes écrits par d\'autres informaticiens que de développer des
programmes à partir de rien. Il est aussi important que vous appreniez à
écrire des commentaires constructifs qui permettent à ceux qui les
lisent d\'améliorer leur travail. Évitez les formulations négatives ou
blessantes. Relisez votre review en vous mettant à la place du groupe
receveur et demandez-vous si elle vous semble utile et constructive.

La review que vous écrivez dans le cadre de ce projet compte pour 5% de
la cote finale, et la participation dans l\'évaluation de groupe. Vous
avez donc tout intérêt à la faire correctement. Par contre, votre review
n\'influence pas la côte qui sera attribuée aux groupes que vous
évaluez. Vous les aidez à améliorer leur travail et obtenir une
meilleure note mais vous ne leur attribuez pas de note.

Une review de qualité contient les éléments suivants :

-   Au moins deux commentaires positifs sur le travail effectué. Cela
    comprend :
    -   au moins un commentaire sur le fond,
    -   au moins un commentaire sur la forme.
-   Au moins deux suggestions d\'améliorations possibles. Cela comprend
    :
    -   au moins une suggestion sur le fond, et/ou une suggestion de
        test unitaire à ajouter pour compléter la suite de test,
    -   au moins une suggestion sur la forme.

Évidemment, il s\'agit là de l\'attente minimale. Vous êtes vivement
encouragés à apporter plus d\'informations dans votre review, en suivant
les conseils plus haut sur cette page !

# En Pratique

Pendant la S7 (voir au début du chapitre), vous aurez fini la partie
rapport de la phase 2. Vous enverrez un zip du code source de
l\'application au groupe qui porte le numéro (XX + 8) mod N où XX est
votre numéro de groupe et N est le nombre total de groupes, soit 36.

Exemple, si je suis dans le groupe 30, je dois envoyer le code de mon
groupe au groupe (30 + 8) mod N = 38 mod 36 = 2.

Pour trouver l\'email du groupe, vous suivrez la démarche suivante :

:   -   aller dans le menu en haut à gauche sur le cours moodle

    -   cliquer sur \"Participants\"

    -   filtrer sur le groupe

    -   

        pour chaque étudiant du groupe :

        :   -   cliquer sur le nom de l\'étudiant
            -   copier son adresse email

Votre review de code sera à intégrer dans un court rapport à envoyer en
réponse au mail par lequel vous aurez reçu votre propre zip à reviewer
ainsi que sur moodle.


# Chapitre 11 : Projet phase 3, le grand final! {#ref-chapitre11}

::: {#ref-projet3}
Ce chapitre présente la phase 3 du projet. Il se basera sur les phases 1
et 2.
:::

L\'objectif de cette phase est d\'ajouter des graphes à votre site afin
de visualiser les données présentes dans la base de donnée. Pour cela,
vous allez utiliser la bibliothèque
[Chart.js](https://www.chartjs.org/). Cette bibliothèque JavaScripts
open source permet de créer des graphiques et de les intégrer à un site
web. La prise en main de Chart.js ne demande pas de base en JavaScripts

## Des graphes pour une meilleur visualisation

Pour créer un graphique efficace qui permet de visualiser les données de
manière claire et concise, il est important de prendre en compte
plusieurs facteurs clés. Tout d\'abord, il est essentiel de choisir le
type de graphique le plus approprié en fonction des données que l\'on
souhaite visualiser.

Ensuite, il est important de bien choisir les axes du graphique et de
s\'assurer qu\'ils sont nommés de manière claire et précise, en incluant
les unités de mesure si nécessaire. Il est également important de
s\'assurer que le graphique est suffisamment grand pour que les données
soient facilement lisibles.

Enfin, il est important d\'utiliser des couleurs claires et cohérentes
pour les différentes parties du graphique, en utilisant des nuances
différentes pour les différents groupes de données si nécessaire. Il est
également important d\'inclure une légende claire qui permet de
comprendre facilement ce que chaque élément du graphique représente. En
suivant ces principes de base, il est possible de créer des graphiques
qui permettent de visualiser efficacement les données et de communiquer
clairement les informations importantes.

Ces concepts ont été présentés en S4 à LLN. Pour Charleroi et pour
rappel à LLN, vous trouverez sur moodle, une [vidéo de
présentation](https://moodle.uclouvain.be/mod/hvp/view.php?id=323901)
introduisant la visualisation de données ainsi que l\'utilisation de
Chart.js et son intégration dans votre projet.

## Objectif de la phase:

Durant cette phase vous devrez implémenter les fonctionnalités
suivantes:

-   Un graphe cumulatif des modes de transport par villes.
-   Pouvoir afficher au choix les nombres de vélos, voitures, \... pour
    une durée choisie et pour une ville et une rue donnés.
-   Une fonctionnalité au choix : demander à votre assistant référent si
    vous n\'avez pas d\'idées.

Votre code Python devra être clair, documenté et accompagné de tests
unitaires.

Comme d\'habitude, chaque groupe **DOIT** réaliser son travail en
utilisant la [Forge UCLouvain](https://forge.uclouvain.be) qui utilise
la plateforme GitLab et le gestionnaire de version Git. Ceci permettra
de garder une trace des contributions des différents membres du groupe.

Vous veillerez, bien entendu, à écrire du code Python clair, documenté
et accompagné de tests unitaires. Une première version de votre projet
devra être prête avant la fin de la S11. En S12, vous fournirez du
feedback détaillé à d\'autres groupes d\'étudiants. Ensuite vous
utiliserez le feedback reçu pour améliorer votre propre projet et
présenterez votre prototype à l\'équipe enseignante.

## Rapport

Sur Moodle, vous remettrez un rapport qui répond aux critères
ci-dessous, et contiendra également des captures d\'écrans de toutes les
pages importantes du site, de façon à ce que si un problème sur la
version Coolify du site se présente, nous puissions nous faire une idée
du design du site. La soumission du rapport se fait au format ZIP, avec
le rapport d\'une part, et une copie du code du site d\'autre part. Le
code ne doit pas contenir de fichiers binaires ou le VENV, il devrait
donc être équivalent au contenu taggué du Git.

## Critères d\'évaluation

Rapport:

-   Le rapport est clair, complet mais concis.
-   Le rapport présente les fonctionnalités implémentées, en particulier
    il détaillera l\'implémentation des graphes et les choix pour la
    représentation des données.
-   Le rapport détaille aussi les nouveaux tests ajoutés pour la
    visualisation et la nouvelle fonctionnalité.
-   Le rapport décrit le fonctionnement du groupe. Il explique les
    problèmes rencontrés, et les pistes de solutions le cas échéant.

Site:

-   Le site fonctionne et est en ligne
-   L\'intégration des nouvelles fonctionnalités est complète
-   Le design est soigné
-   L\'interface est cohérente, le layout du site est compréhensible

Documentation du code:

-   Le code est commenté en utilsant des docstrings tels que présenté au
    cours.

Code:

-   Le code est correct.
-   Le code est vérifié par des tests (point important).
-   Le code est structuré. La nomenclature et l\'organisation des
    modules et répertoires présentés dans l\'énoncé sont respectées.

Git:

-   L\'ensemble des modifications importantes a été fait en utilisant
    des merge request.
-   Les merge request ont fait l\'objet de review systématiques.

## Peer review

Un rendu préliminaire du projet (code uniquement) est à remettre à un
autre groupe pour peer-review en S11, pour **mardi 2 Mai à 18H** à LLN
et pour le **jeudi 4 Mai à 18H** à Charleroi. Vous ferez ensuite une
revue par les pairs (peer review) du travail rendu par un autre groupe,
comme lors de la phase 2. Le même schéma de partage du code est à
suivre, notamment pour l\'envoi du code au groupe concerné. Il ne faut
pas rendre ce code préliminaire sur Moodle, uniquement au groupe
concerné par e-mail. Cette review sera à faire dans les 3 jours. Donc le
**vendredi 5 Mai à 18H** à LLN et pour le **dimanche 7 Mai à 18H** à
Charleroi.

## Rendu final

Le rendu final du rapport et de votre code est à faire à LLN le **mardi
9 Mai à 18H** et à Charleroi le **jeudi 11 Mai à 18H** sur Moodle. Vous
n\'aurez donc que 4 jours pour intégrer les commentaires faits par
l\'autre groupe lors de la peer-review. Cependant vous pourrez présenter
des modifications proposées dans la peer review mais que vous n\'auriez
pas eu le temps de faire à la présentation.

## Présentation et dynamo

En S13, pour le lundi 15 vous devrez avoir remplis un nouveau module
Dynamo sur Moodle, différent de celui de la phase 1 afin d\'évaluer le
travail de groupe.

Vous devrez présenter votre site web ainsi que ces fonctionnalités lors
d\'une présentation orale le 17 Mai pour LLN, le 19 Mai à Charleroi.

La présentation comportera une partie sur le projet, l\'architecture du
code, (avec des diapositives en support) de 5 minutes, une démonstration
de 3 minutes et un Q&A de 2 minutes. Prévoyez une vidéo de secours pour
la démonstration.

Les détails de cette présentation vous seront communiqués en temps voulu
sur Moodle.


# Construire et accéder à la base de données

:::::::::::::::: {#define-and-access-the-database .container .section}
**Construire et accéder à la base de données**

L'application va utiliser une base de données
[SQLite](https://sqlite.org/about.html) pour stocker les villes et les
rues. Python intègre un support pour SQLite dans le module
[sqlite3](https://docs.python.org/3/library/sqlite3.html#module-sqlite3).

SQLite est intéressant, car il peut s'utiliser sans nécessiter
l'installation d'un serveur de base de données séparé et il est
directement intégré à Python. Cependant, si plusieurs accès en écriture
à la base de données se font en même temps, l'application va ralentir,
car ceux-ci doivent être séquentiels. Pour de petites applications, ce
n'est pas important. Si votre application prend de l'ampleur et
nécessite beaucoup d'écritures, vous devrez peut-être passer à une autre
base de données.

Ce tutoriel ne rentre pas dans les détails du langage SQL. N\'hésitez
pas à retourner lire le \"`ref-sql`{.interpreted-text role="ref"}\", les
slides des deux cours sur le SQL sur Moodle, ou [la documentation de
SQL](https://sqlite.org/lang.html).

::::: {#connect-to-the-database .container .section}
**Connexion à la base de données**

La première chose à faire pour travailler avec une base de données
SQLite (et la plupart des autres librairies Python de gestion de bases
de données) est de créer une connexion avec la base de données. Toutes
les requêtes et les opérations se font en utilisant la connexion qui est
fermée lorsque le travail est terminé.

Dans une application web, cette connexion est généralement associée à la
requête. Elle est créée pendant le traitement de la requête et fermée
avant l'envoi de la réponse.

:::: {#id1 .container .literal-block-wrapper .docutils}
::: {.container .code-block-caption}
`mobility/db.py`
:::

``` python
import sqlite3
from flask import current_app, g


def get_db():
      if 'db' not in g:
         g.db = sqlite3.connect(
            current_app.config['DATABASE'],
            detect_types=sqlite3.PARSE_DECLTYPES
         )
         g.db.row_factory = sqlite3.Row

      return g.db


def close_db(e=None):
      db = g.pop('db', None)

      if db is not None:
         db.close()
```
::::

[g](https://flask.palletsprojects.com/en/1.1.x/api.html#flask.g) est un
objet spécial qui est unique pour chaque requête. Il est utilisé pour
stocker des données qui pourraient être accédées par plusieurs fonctions
durant le traitement de la requête. La connexion est conservée et
réutilisée si `get_db` est appelé une deuxième fois dans le traitement
de la même requête.

[current_app](https://flask.palletsprojects.com/en/1.1.x/api.html#flask.current_app)
est un autre objet spécial qui pointe vers l'application Flask qui
traite la requête. Comme vous avez utilisé une usine à application, il
n'y a pas d'objet application en écrivant la suite de votre code.
`get_db` sera appelée lorsque l'application a été créée et qu'elle
traite une requête. De cette façon,
[current_app](https://flask.palletsprojects.com/en/1.1.x/api.html#flask.current_app)
peut être utilisé.

[sqlite3.connect()](https://docs.python.org/3/library/sqlite3.html#sqlite3.connect)
crée une connexion avec le fichier correspondant au paramètre de
configuration `DATABASE`. Il n'est pas nécessaire que ce fichier existe.
Il sera créé plus tard lors de l'initialisation de la base de données.

Le paramètre
[sqlite3.Row](https://docs.python.org/3/library/sqlite3.html#sqlite3.Row)
indique que la connexion doit retourner des lignes qui sont équivalentes
à des dictionnaires Python. Cela permet d'accéder aux colonnes en
indiquant leur nom.

`close_db` vérifie si une connexion a été créée en regardant si `g.db` a
été initialisé. Si la connexion existe, elle est fermée. Vous apprendrez
plus tard à votre application d'utiliser la fonction `close_db` depuis
l'usine à applications de façon à l'appeler automatiquement après le
traitement de chaque requête.
:::::

::::::: {#create-the-tables .container .section}
**Création des tables**

Dans SQLite, les données sont stockées dans des *tables* et des
*colonnes*. Elles doivent être créées avant que vous ne puissiez stocker
et récupérer des données dans la base de données. Flask va stocker les
utilisateurs dans la table `user` et les messages dans la table `posts`.
Une telle base de données peut être créée en utilisant les commandes SQL
ci-dessous:

:::: {#id2 .container .literal-block-wrapper .docutils}
::: {.container .code-block-caption}
`mobility/schema.sql`
:::

``` sql
DROP TABLE IF EXISTS ville;
CREATE TABLE IF NOT EXISTS ville (
   code_postal INTEGER PRIMARY KEY,
   nom TEXT NOT NULL,
   population INTEGER NOT NULL
);
```
::::

Vous pouvez exécuter ces commandes SQL en les intégrant comme ci-dessous
dans le fichier `db.py`:

:::: {#id3 .container .literal-block-wrapper .docutils}
::: {.container .code-block-caption}
`mobility/db.py`
:::

``` python
def init_db():
      db = get_db()

      with current_app.open_resource('schema.sql') as f:
         db.executescript(f.read().decode('utf8'))


def init_app(app):
   app.teardown_appcontext(close_db)
```
::::

[open_resource()](https://flask.palletsprojects.com/en/1.1.x/api.html#flask.Flask.open_resource)
ouvre un fichier qui est relatif au package `mobility`. L'utilisation
d'un chemin relatif est intéressant car vous ne saurez pas
nécessairement quel sera ce répertoire lorsque vous mettrez votre
application en production. `get_db` retourne une connexion à la base de
données, qui est utilisée pour exécuter les commandes lues dans le
fichier passé en argument.
:::::::

::::::: {#register-with-the-application .container .section}
**Enregistrement à l'application**

La fonction `close_db` doit être enregistrée dans l'instance de
l'application. Sinon, elle ne peut pas être utilisée par l'application.

:::: {#id4 .container .literal-block-wrapper .docutils}
::: {.container .code-block-caption}
`mobility/db.py`
:::

``` python
def init_app(app):
      app.teardown_appcontext(close_db)
```
::::

[app.teardown_appcontext()](https://flask.palletsprojects.com/en/2.2.x/api/#flask.Flask.teardown_appcontext)
demande à Flask d'appeler cette fonction lorsqu'elle libère les
ressources associées à une requête après avoir retourné la réponse.

Vous devez importer et appeler cette fonction depuis l'usine à
applications. Placez le nouveau code à la fin de la fonction contenant
l'usine à applications et juste avant de retourner l'application.

Si ce n\'est pas fait, définissez également la variable \"DATABASE\".

:::: {#id5 .container .literal-block-wrapper .docutils}
::: {.container .code-block-caption}
`mobility/__init__.py`
:::

``` python
def create_app():
      app = ...

      # existing code omitted

      app.config.from_mapping(
               SECRET_KEY='dev',
               DATABASE=os.path.join(app.instance_path, 'db.sqlite')
            )


      # existing code omitted

      from . import db
      db.init_app(app)

      with app.app_context():
         db.init_db()

      return app
```
::::
:::::::
::::::::::::::::

::: only
html

Continuez en lisant le document [Plans et vues pour les
villes](views_city.html).
:::

# Configuration de l\'application

**Configuration de l'application**

Une application Flask est une instance de la classe
[Flask](https://flask.palletsprojects.com/en/1.1.x/api.html#flask.Flask).
Tout ce qui concerne cette application, que ce soit sa configuration ou
ses URLs, sera enregistré dans cette classe.

La façon la plus simple de créer une application Flask est de créer une
instance de la classe
[Flask](https://flask.palletsprojects.com/en/1.1.x/api.html#flask.Flask)
globale, directement au début de votre code, comme l'exemple « Hello,
World! » sur la page précédente. Bien que cette approche soit simple et
utile dans certains cas, elle peut causer des soucis lorsque le projet
grandit.

Au lieu de créer un instance globale de la classe
[Flask](https://flask.palletsprojects.com/en/1.1.x/api.html#flask.Flask),
vous allez la créer dans une fonction. Cette fonction est généralement
appelée l'usine à applications (*application factory* en anglais).
Toutes les opérations liées à la configuration de l'application doivent
se faire dans cette fonction qui retourne l'application.

::: {#the-application-factory .container .section}
**L'Usine à Applications**

Il est temps de commencer à coder. Créez le répertoire `mobility` et
ajoutez-y le fichier `__init__.py`. Le fichier `__init__.py` a deux
rôles. Tout d'abord, il contient l'usine à applications. Depuis, il
indique à Python que le répertoire `mobility` doit être considéré comme
étant un package.

``` console
$ mkdir mobility
```

``` python
import os

from flask import Flask


def create_app(test_config=None):
      # create and configure the app
      app = Flask(__name__, instance_relative_config=True)
      app.config.from_mapping(
         SECRET_KEY='dev'
      )

      if test_config is None:
         # load the instance config, if it exists, when not testing
         app.config.from_pyfile('config.py', silent=True)
      else:
         # load the test config if passed in
         app.config.from_mapping(test_config)

      # ensure the instance folder exists
      try:
         os.makedirs(app.instance_path)
      except OSError:
         pass

      # a simple page that says hello
      @app.route('/hello')
      def hello():
         return 'Hello, World!'

      return app
```

`create_app` est la fonction contenant l'usine à applications. Vous la
compléterez plus tard dans ce tutoriel, mais elle réalise déjà beaucoup
d'opérations.

1.  `app = Flask(__name__, instance_relative_config=True)` crée une
    instance de la classe
    [Flask](https://flask.palletsprojects.com/en/1.1.x/api.html#flask.Flask).
    -   `__name__` est le nom du module Python courant. L'application
        doit connaître l'endroit où est elle installée pour configurer
        certains chemins et `__name__` est une solution classique pour
        obtenir cette information.
    -   `instance_relative_config=True` indique à l'application que les
        fichiers de configuration sont relatifs au répertoire [instance
        folder](../config.html#instance-folders). Ce répertoire est
        localisé en dehors du package `mobility` et peut contenir des
        données locales qui ne doivent pas être intégrées au contrôle de
        version, comme les secrets utilisés dans la configuration et le
        fichier contenant la base de données.
2.  [app.config.from_mapping()](https://flask.palletsprojects.com/en/1.1.x/api.html#flask.Config.from_mapping)
    spécifie plusieurs paramètres par défaut que l'application va
    utiliser:
    -   [SECRET_KEY]{.title-ref} est utilisé par Flask et des extensions
        pour stocker de données de façon sûre. Il est initialisé à la
        valeur `'dev'` qui est une valeur facile pendant le
        développement de l'application, mais doit être remplacé par une
        valeur aléatoire lorsque celle-ci est mise en production.
3.  [app.config.from_pyfile()](https://flask.palletsprojects.com/en/1.1.x/api.html#flask.Config.from_pyfile)
    remplace le configuration par défaut avec des paramètres spécifiés
    dans le fichier `config.py` qui se trouve dans l"*instance folder*
    si celui-ci exite. Par exemple, en production, cela peut être
    utilisé pour fixer une `SECRET_KEY` vraiment secrète.
    -   Le paramètre `test_config` peut aussi être passé à l'usine à
        applications. Dans ce cas, il sera utilisé à la place de la
        configuration de l'instance. Cela vous permettra de spécifier
        des paramètres pour vos tests qui sont indépendants de ceux que
        vous utilisez durant le développement de l'application.
4.  [os.makedirs()](https://docs.python.org/3/library/os.html#os.makedirs)
    vérifie que le chemin
    [app.instance_path](https://flask.palletsprojects.com/en/1.1.x/api.html#flask.Flask.instance_path)
    existe. Flask ne créer pas l'instance folder automatiquement, mais
    celui-ci doit être créé, car votre projet cherchera à y créer le
    fichier contenant sa base de données SQLite.
5.  [\@app.route()](https://flask.palletsprojects.com/en/1.1.x/api.html#flask.Flask.route)
    crée une route simple de façon à vous permettre de voir
    l'application fonctionner avant de faire l'entièreté du tutoriel.
    Elle relie l'URL `/hello` à une fonction qui retourne une réponse,
    dans ce cas la chaîne de caractères `'Hello, World!'`.
:::

::::::: {#run-the-application .container .section}
**Lancer l'application**

Vous pouvez maintenant lancer votre application en utilisant la commande
`flask`. Depuis le terminal, indiquez à Flask où trouver l'application
et ensuite lancez-le en mode développement. N'oubliez pas de vous placer
d'abord dans le répertoire `base-project` et non dans le package
`mobility`.

Le mode de développement lance automatiquement un débugger interactif
lorsqu'une page lance une exception et relance le serveur chaque fois
que vous modifiez votre code. Vous pouvez le laisser fonctionner et
devez juste recharger la page dans votre navigateur au fur et à mesure
de votre progression dans le tutoriel.

``` console
$ flask --app=mobility --debug run
```

Vous devriez observer une sortie équivalente au texte ci-dessous sur la
sortie standard:

:::: {.container .highlight-none .notranslate}
::: {.container .highlight}
    * Serving Flask app "mobility"
    * Environment: development
    * Debug mode: on
    * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
    * Restarting with stat
    * Debugger is active!
    * Debugger PIN: 855-212-761
:::
::::

Vous pouvez maintenant visiter l'URL <http://127.0.0.1:5000/hello> dans
un navigateur et vous devriez voir le message « Hello, World! ».
Félicitations, vous exécutez maintenant votre première application web
en Flask!

:::: note
::: title
Note
:::

Dans une précédente version du cours, nous proposions d\'utiliser des
variables d\'environnement plutôt que les paramètres
[\--app]{.title-ref} et [\--debug]{.title-ref}. Nous laissons ces
informations au cas où vous les chercheriez, mais la méthode ci-dessus
convient parfaitement.

Pour Linux et Mac:

``` console
$ export FLASK_APP=mobility
$ export FLASK_DEBUG=1
$ flask run
```

Pour Windows via l'invite de commandes, utilisez `set` au lieu de
`export`:

``` bash
> set FLASK_APP=mobility
> set FLASK_DEBUG=1
> flask run
```

Pour Windows Powershell, utilisez `$env:` au lieu de `export`:

``` bash
> $env:FLASK_APP = "mobility"
> $env:FLASK_DEBUG = "1"
> flask run
```
::::
:::::::

::: only
html

Continuez en lisant le document [Plans et vues](view_new).
:::

# Tutoriel Git

## Prérequis

Pour comprendre ce TP, il est nécessaire comprendre :

> -   Le concept d\'[arborescence de
>     fichiers](https://wiki.student.info.ucl.ac.be/Documentation/ArborescenceFichiers)
> -   L\'invite de commande, aussi appelée
>     [shell](https://wiki.student.info.ucl.ac.be/Documentation/Shell)

Prenez le temps de les aborder en cliquant sur les liens si vous n\'êtes
pas à l\'aise, sinon vous serez perdu.

## Notions clefs

1.  Dépôt (repository)

Un ensemble de fichiers consituant le code source d\'un programme que
l\'on désignera comme un [projet]{.title-ref} est enregistré dans un
répertoire. La figure ci-dessous illustre un répertoire avec un
[projet]{.title-ref}.

![](/tuto_git/_images/repository.png)

Le répertoire caché `.git` est nommé le dépôt (\"repository\" en
anglais). Ce répertoire contient l'historique des modifications du
projet. Le dossier du projet ne contient qu\'une version des fichiers du
projet (la dernière version).

2.  Commit

L'historique d\'un projet est une séquence de \"photos\" de l'état du
projet à un moment donné. On appelle ces \"photos\" des commits.

Les commits possèdent

:   -   Une date
    -   Un auteur
    -   Une description textuelle
    -   Un lien vers le(s) commit(s) précédent(s)

![](/tuto_git/_images/commit.png)

3.  Copie de travail

On appelle \"Copie de travail\" les fichiers effectivement présents dans
le répertoire géré par Git. Leur état peut être différent du dernier
commit de l'historique.

4.  Index

L'index est un espace temporaire contenant modifications prêtes à être «
commitées ». Ces modifications peuvent être :

-   Création de fichier
-   Modification de fichier
-   Suppression de fichier

On doit ajouter un fichier à l'index pour qu'il soit pris en
considération.

:::: note
::: title
Note
:::

Que l\'on apprécie ou pas, l\'utilisation de mots francisés tels que
\"commiter\" est la norme dans le monde du développement. Nous nous
permettrons donc l\'utilisation de tels anglicismes plutôt que
d\'utiliser des termes français correct qui ne sont en réalité pas
d\'usage chez les développeurs.
::::

## Installation de Git

:::: warning
::: title
Warning
:::

Cette partie du TP est à faire individuellement, car tout le monde aura
besoin de ces connaissances.
::::

Si vous ne l\'avez pas encore, vous devez installer Git. Voici un
tutoriel pour vous y aider :
<https://wiki.student.info.ucl.ac.be/Logiciels/Git>.

:::: warning
::: title
Warning
:::

**Utilisateurs Windows, attention !**

Par défaut, Windows cache les extensions des fichiers. Cela veut dire
que dans l\'explorateur Windows, si vous créez un fichier appelé
README.md, il s\'appellera en fait `README.md.txt`.

Vous devez afficher les extensions sur Windows. En tant
qu\'informaticien·ne·s, c\'est inévitable.

1.  Allez dans l\'explorateur Windows
2.  Allez dans Option dans la barre du dessus. Cela peut être caché sous
    le symbole `...`:

![](/tuto_git/_images/windows_options.png)

3.  Dans l\'onglet affichage\...

![](/tuto_git/_images/windows_ext.png)

4.  Décochez [Masquer les extensions des fichiers dont le type est
    connu.]{.title-ref}
5.  Cliquez sur [Ok]{.title-ref}
::::

## Utilisation de Git localement

### Création d\'un dépôt Git

Créez d\'abord un répertoire `MyProject`. Pour initialiser un dépôt Git
local, naviguez jusqu\'au répertoire que vous venez de créer et utilisez
la commande `git init` . Cela crée un sous-répertoire caché appelé
`.git` qui contient toutes les informations de suivi de version de votre
projet.

### Ajouter des fichiers au dépôt et commits

Créez un fichier nommé `README.md` dans le répertoire `MyProject` et
ajoutez une phrase de votre choix.

Pour ajouter le fichier `README.md` à l\'index, utilisez la commande
`git add` suivie du nom du fichier, par exemple :

``` console
$ git add README.md
```

Pour enlever un fichier de l\'index, utilisez la commande `git rm`
suivie du nom du fichier, par exemple :

``` console
$ git rm README.md
```

Pour afficher le statut de l\'index, utilisez la commande `git status`.

### Enregistrer les modifications de l\'index dans le dépôt

Pour enregistrer les modifications de l\'index dans le dépôt, utilisez
la commande `git commit`. Voici un exemple :
`git commit -m "Ajout du fichier README.md"`

Commentaires sur les commits :

:   -   Il faut un message pour faire un commit sur git.
    -   Le message de commit doit indiquer clairement les modifications
        apportées au contenu du dépôt.

Ajoutez un second fichier au dépôt, par exemple un fichier `.txt` avec
une phrase de votre choix. Ajoutez-le à l\'index et enregistrez-le dans
le dépôt. Regardez l\'historique de votre dépôt avec la commande
`git log`. Effectuez une modification sur le fichier `README.md` et
enregistrez-la dans le dépôt. Regardez l\'historique de votre dépôt avec
la commande `git log`.

### Observation de l\'historique

Vous connaissez déjà la commande `git log` qui affiche l\'historique des
commits. On peut observer les changements apportés par un commit
particulier avec la commande `git diff`.

`git diff <AAAA> <BBBB>` où \<AAAA\> et \<BBBB\> sont les premières
lettres des identifiants des commits à comparer. Par exemple :
`git diff 6abc87 2bf521`.

### Navigation dans l\'historique

Pour observer l\'état du dépôt dans le passé, utilisez la commande
`git checkout`.

Attention, `git checkout` est une commande dangereuse, car elle modifie
l\'état de votre copie de travail si vous n\'avez pas commité vos
dernières modifications. De plus on ne modifie pas une ancienne version.
Exemple : `git checkout 6abc87`

Pour revenir à la version la plus récente, utilisez la commande
`git checkout master`.

Observez l\'état du dépôt après votre premier commit et revenez à la
version la plus récente.

## Utilisation d\'un dépôt distant

Un dépôt distant est un dépôt Git hébergé sur un serveur distant
(GitHub, GitLab, Bitbucket, \...). Pour le projet et le TP nous
utiliserons celui hébergé sur les serveurs de l\'UCLouvain
(<https://forge.uclouvain.be/>). Un dépôt local peut être lié à un dépôt
distant. Git permet de synchroniser les deux dépôts en copiant les
commits de l\'un à l\'autre. Un dépôt peut être public et donc
accessible à tous, ou privé.

### Création d\'un dépôt distant

Connectez-vous sur le GitLab de l\'UCL : <https://forge.uclouvain.be/> .

![](/tuto_git/_images/login_gitlab.png)

Créez un nouveau projet en cliquant sur le bouton \"New project\". Vous
devriez voir une page comme celle illustrée par l\'image ci-dessous. Sur
cette page, sélectionnez \"Create blank project\". Laissez
l\'initialisation du projet avec un fichier `README.md`. Le
[README]{.title-ref} est un fichier texte qui contient des informations
sur le projet. L\'extension `.md` signifie qu\'il est au format
Markdown. C\'est un standard qui définit quelques moyens de mettre en
forme le texte, un peu comme le HTML. Prenez le temps d\'écrire quelques
lignes.

![](/tuto_git/_images/create_project.png)

Configurez le projet en indiquant le nom du projet, la description et le
type de projet (pour le TP, publiez-le en privé).

![](/tuto_git/_images/configure_project.png)

Si votre projet est correctement configuré, vous devriez obtenir une
page comme celle illustrée par l\'image ci-dessous.

![](/tuto_git/_images/initialized_project.png)

### Clonage d\'un dépôt distant

Pour créer une copie locale du dépôt distant, on utilise la commande
`git clone`.

> Exemple : `git clone https://github.com/vivian/my-project.git`

L\'image ci-dessous vous indique comment trouver l\'adresse du dépôt
distant. Choisissez \"Clone with HTTPS\" et copiez l\'adresse.

![](/tuto_git/_images/clone_project.png)

Créez un nouveau répertoire et clonez le dépôt distant que vous avez
créé à l\'exercice précédent
(<https://forge.uclouvain.be/votre_pseudo/my-project> ). Un nouveau
dossier devrait être créé avec les fichiers du dépôt. Dans la copie
locale obtenue par le clone, les commits se feront toujours localement,
on navigue dans l\'historique local. Mais on synchronise le dépôt
distant avec les commandes `git push` et `git pull`.

### Modification du dépôt

Modifiez le fichier `README.md` qui a été cloné avec votre éditeur de
texte préféré, comme `gedit`, `thonny` ou même `pycharm`.

Enregistrez ensuite les modifications dans le dépôt local:

``` console
$ git add README.md
$ git commit
```

La dernière commande, `git commit` ouvrira un éditeur de texte. Par
défaut c\'est souvent [vim]{.title-ref}, un éditeur de texte en ligne de
commande avec des symboles tildes `~` comme sur l\'image ci-dessous. Si
vous êtes perdu avec vim, consultez [la documentation
INGI](https://wiki.student.info.ucl.ac.be/Documentation/Vi).

![](/tuto_git/_images/vim.png)

Entrez d\'abord un titre de maximum 80 caractères, puis une ligne vide,
et finalement une description claire, nette et précise.

Pour quitter VIM il faut appuyer la touche [ESC]{.title-ref} et entrer
`:q` suivi de la touche [ENTER]{.title-ref}.

Une alternative au git add est d\'utiliser directement
`git commit --interactive` tel que vu en cours.

### Synchronisation avec un dépôt distant

Ensuite synchronisez votre dépôt local avec votre dépôt distant en
faisant `git push`.

Sur la Forge, vous devriez pouvoir observer vos modifications. Vous
pouvez également visualiser ce commit en ligne, et voir le contenu d\'un
fichier sur la Forge.

Cliquez sur le fichier `README.md` que vous venez de modifier. Vous
aurez une visualisation en ligne du fichier comme celle-ci :

![](/tuto_git/_images/edit_online_btn.png)

Cliquez sur le bouton \"Edit\" afin de modifier le fichier en ligne :

![](/tuto_git/_images/edit_online_editor.png)

Vous pouvez ajouter une phrase, et de la même façon entrer une
description commençant par un titre, une ligne vide et puis la
description.

Cliquez sur \"commit change\".

:::: warning
::: title
Warning
:::

NE **JAMAIS** MODIFIER DU CODE EN LIGNE !!!

Il convient de toujours tester votre code avant de le publier sur le
dépôt commun. Seuls le texte ou des commentaires peuvent être modifiés
en ligne. Si vous modifiez du code en ligne, ce sera la preuve que vous
êtes très peu consciencieux et cela sera pénalisé. Imposer à vos
condisciples de vérifier votre code à votre place est un acte lâche qui
attirera assurément des remontrances de vos collègues.
::::

Il faut maintenant récupérer le contenu de la modification distante dans
votre dépôt local :

``` console
$ git pull
```

### Travailler à plusieurs sur un dépôt distant

:::: warning
::: title
Warning
:::

Remarque : les exercices suivants sont à faire en groupes de 2 ou 3
personnes.
::::

Formez maintenant des groupes de 2 ou 3 personnes et désignez un dépôt
distant sur lequel vous allez travailler à plusieurs. Les autres peuvent
supprimer leurs dépôts de test.

Le propriétaire du dépôt distant doit ajouter les autres du groupe. Pour
cela, le propriétaire du Git doit aller dans le menu à gauche sur Gitlab
et cliquer sur \"Project informations\" et ensuite \"Members\". Vous
devriez voir une page comme celle illustrée ci-dessous. Sur cette page,
le propriétaire doit ajouter les autres personnes du groupe en tant que
\"Developer\".

![](/tuto_git/_images/invite_member.png)

Quand vous obtenez les accès, clonez localement ce dépôt distant comme
vous aviez fait précédemment.

Un·e membre de votre groupe crée des modifications dans le dépôt local
et les synchronise du dépôt local vers le dépôt distant. Les autres
personnes du groupe doivent synchroniser leur dépôt avec la commande
appropriée.

Tou·e·s les membres du groupe devraient avoir les mêmes modifications
dans leur dépôt local.

Pour vous en assurer vous pouvez utiliser `git log` et vérifier que
l\'id du dernier commit est bien la même chez tout le monde.

### Modifications simultanées sur deux fichiers différents

En même temps, un·e membre du groupe modifie le fichier `README.md`.
Une· autre membre du groupe crée un fichier `main.py`. Les deux membres
du groupe qui ont apporté les modifications synchronisent leurs dépôts
avec le dépôt distant. Quel est le résultat ?

> Le push du deuxième membre du groupe échoue, car il faut être à jour
> avec le dépôt distant. Il y a un conflit, car vous avez modifié le
> dépôt en même temps.

Comme vous avez modifié des fichiers différents, tout devrait bien se
passer. La·le deuxième membre qui n\'a pas pu pousser ses modifications
doit simplement faire `git pull --rebase` pour appliquer ses
modifications au-dessus des modifications du premier à pousser. Après
cela, comme git a rebasé ses modifications sur celle du premier, vous
pouvez faire `git push` sans soucis.

### Modifications simultanées à deux endroits différents d\'un même fichier

Assurez-vous avant cet exercice que le fichier `README.md` fait
plusieurs lignes avec un texte bidon, et que tou·te·s les membres ont
bien exécuté `git pull`. Un·e membre du groupe modifie la première ligne
du fichier `README.md`. Un·e autre membre du groupe modifie une ligne
différente du fichier `README.md`, par exemple la ligne numéro 5. Les
deux membres du groupe qui ont apporté les modifications synchronisent
leurs dépôts avec le dépôt distant. Quel est le résultat ?

> Comme dans l\'exercice précédent, le deuxième ne peut pas pousser ses
> modifications. Cependant `git pull --rebase` fonctionne toujours, car
> git est assez puissant que pour fusionner des modifications dans le
> même fichier qui ne sont pas faites au même endroit. Il faut en
> général une ligne d\'écart pour que les choses se passent
> correctement.

### Modifications simultanées aux mêmes endroits

Deux membres du groupe modifient la même ligne du fichier `README.md`.
Les deux personnes synchronisent leurs dépôts avec le dépôt distant.
Quel est le résultat ?

> Cette fois, comme vous avez modifié le même fichier au même endroit,
> `git pull --rebase` va échouer:
>
> ``` {.console emphasize-lines="10"}
> $ git pull --rebase
> remote: Enumerating objects: 3, done.
> remote: Counting objects: 100% (3/3), done.
> remote: Compressing objects: 100% (3/3), done.
> remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
> Unpacking objects: 100% (3/3), 418 bytes | 418.00 KiB/s, done.
> From forge.uclouvain.be:XXX/YYY
>    adb1137..09709a5  main       -> origin/main
> Auto-merging README.md
> CONFLICT (content): Merge conflict in README.md
> error: could not apply d70f38d... My commit
> hint: Resolve all conflicts manually, mark them as resolved with
> hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
> hint: You can instead skip this commit: run "git rebase --skip".
> hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
> Could not apply d70f38d... My commit
> ```

Git vous invite à résoudre le conflit et à faire un commit de cette
résolution.

Vous avez deux solutions: corriger manuellement le conflit, ou utiliser
un éditeur de texte supportant la fusion de document, tel que `meld`.

#### Manuellement

On doit pour cela ouvrir le fichier incriminé avec un éditeur de fichier
texte. Les zones en conflit sont marquées par des chevrons ajoutés par
Git.

``` 
# Readme of the project

<<<<<<< HEAD
The modification of the first member
=======
The modification of the second member
>>>>>>> d70f38d (My commit)
```

La première version est celle de cellui qui a modifié le fichier en
premier. La seconde est la différence locale.

Vous pouvez corriger le fichier en enlevant bien les chevrons et tout
texte superflu. Ensuite, marquez le fichier comme corrigé en l\'ajoutant
à l\'index comme d\'habitude avec `git add`.

**Attention !** pour continuer le rebasage, faites **git rebase
\--continue**.

#### À l\'aide d\'un éditeur

Alors qu'un `git pull --rebase` vient d\'échouer, lancez la commande
`git mergetool`.

Si la commande ne lance [vimdiff]{.title-ref} ou un outil qui ne vous
convient pas, installez le logiciel *meld*. Si `git mergetool` ne lance
toujours pas *meld*, utilisez `git mergetool --tool=meld`. Sur Windows,
si cela ne fonctionne toujours pas, suivez les conseils de [cet article
sur
stackoverflow](https://stackoverflow.com/questions/14821358/git-mergetool-with-meld-on-windows).

![](/tuto_git/_images/meld.png)

La fenêtre de *meld* vous montre à gauche le fichier local, au milieu la
version finale, et à droite la version distante.

Le jeu consiste à envoyer les modifications vers le centre. La ligne
verte a été ajoutée seulement d\'un côté et est donc simple à ajouter au
milieu. Il suffit de cliquer sur la flèche pointant vers le centre.

La ligne rouge a été modifiée à droite et à gauche, vous devez choisir
laquelle est la bonne, ou vous-même écrire une nouvelle version qui
contente tout le monde.

Enregistrez et quittez lorsque vous avez fusionné toutes les
modifications.

`git mergetool` va ouvrir tous les fichiers en conflit les uns après les
autres. Une fois terminé, vous pouvez faire `git push`.

### Fusion

Le rebasage est plus propre que la fusion. En effet, `git rebase` va
reprendre les différences locales depuis l\'historique commun avec la
branche distante, et les réappliquer sur la version distante. C\'est
plus propre, car le résultat final sera équivalent à un cas où
l\'utilisateur local aurait écrit son code après avoir récupéré la
dernière version du code. Préférez donc l\'utilisation du rebasage tel
que vu ci-dessus pour gérer les conflits plutôt que la fusion (*git
merge*). La fusion va fusionner deux branches, il restera donc en ligne
deux \"histoires\" indépendantes. Pour comprendre l\'historique du
projet, un lecteur devra remonter votre branche locale et la distante et
comprendre comment elles ont été fusionnées. Dans le cas d\'un rebasage,
elles apparaitront comme venant l\'une après l\'autre.

## Les branches

Dans certaines situations, il est utile de travailler sur plusieurs
versions d\'un même projet en parallèle. Par exemple, on peut vouloir
travailler sur une nouvelle fonctionnalité sans modifier la version
stable du projet. Ces versions peuvent parfois être fusionnées (mais pas
forcément).

Notions fondamentales

> -   Une branche est une lignée de commits à laquelle on a donné un
>     nom.
> -   Le commit le plus récent d\'une branche est appelé sommet (en
>     anglais : tip).
> -   La copie de travail est en général liée au sommet d\'une branche
>     (main, ou anciennement master par défaut).
> -   Chaque nouveau commit, le sommet de la branche courante est avancé
>     vers ce nouveau commit (la branche « pousse »).

Quelques commandes utiles pour l\'exercice suivant

> -   Pour créer une nouvelle branche, on utilise la commande \"git
>     branch\" : `git branch nom_de_la_branche`
> -   Pour basculer sur une branche, on utilise la commande \"git
>     checkout\" : `git checkout nom_de_la_branche`

### Création d\'une nouvelle branche

Créez une nouvelle branche `my_first_branch` et basculez sur cette
branche nouvelle branche.

Exécutez la commande `git branch` pour vérifier que vous êtes bien sur
la branche `my_first_branch`.

Synchronisez la branche `my_first_branch` avec le dépôt distant à
l\'aide de la commande `git push origin my_first_branch` .

Apportez une modification localement au fichier `README.md` sur la
branche `my_first_branch` et synchronisez la branche avec le dépôt
distant. Pour le push utilisez la commande
`git push origin my_first_branch`

Normalement, vous devriez pouvoir voir vos deux branches sur le dépôt
distant comme sur l\'image ci-dessous (en cliquant sur le lien
\"Branches\").

![](/tuto_git/_images/new_branch.png){width="100.0%"}

Mettez à jour la branche `main` avec les modifications de la branche
`my_first_branch`.
\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~

Basculez sur votre branche principale `main`. Mettez à jour la branche
`my_first_branch` avec la branche `main` à l\'aide de la commande
`git FG <nom de la branche>`.

## Les Forks et les Merge Requests

### Forker un dépôt distant

Le fork est une copie d\'un dépôt distant. Il permet de travailler sur
un projet sans avoir les droits d\'écriture sur le dépôt distant.

Commencez par changer la permission du dépôt distant que vous aviez créé
au début de ce tutoriel pour la mettre en public. Cela permettra à vos
camarades de groupe de pouvoir forker ce dépôt. Vous devriez trouver
cette option dans le menu \"Settings\" du dépôt distant. L\'image
ci-dessous montre où se trouve cette option dans le menu Settings.

![](/tuto_git/_images/change_permission.png)

Forkez le dépôt distant de vos camarades de groupe et clonez-le sur
votre machine.

![](/tuto_git/_images/fork_project.png)

Ajoutez des modifications à un fichier de votre choix (le fichier
`README.md` par exemple) et synchronisez le dépôt local avec le dépôt
distant.

Le but de l\'exercice suivant sera d\'\"envoyer\" vos modifications au
dépôt distant de votre camarade de groupe à l\'aide d\'une \"merge
request\".

### Merge request

Une \"merge request\" (ou aussi appelée \"pull request\") est une
demande de fusion de modifications d\'une branche vers une autre
branche.

Dans l\'exercice suivant, vous allez faire une merge request depuis le
dépôt que vous avez forké vers le dépôt distant de vos camarades de
groupe.

Ensuite, faites une pull request sur le dépôt distant de vos camarades
de groupe. Vous pouvez faire des merge request sur GitLab depuis
l\'interface web.

Cliquez sur Merge request et ensuite sur le bouton \"New merge request\"
et sélectionnez la branche depuis laquelle vous avez fait vos
modifications.

![](/tuto_git/_images/merge_request.png)

\"Source branch\" est la branche sur laquelle vous avez fait vos
modifications (dans cet exercice, c\'est depuis votre fork)

\"Target branch\" est la branche sur laquelle vous voulez faire vos
modifications (vers le dépôt de vos camarades de groupe)

Cliquez sur \"compare branches and continue\" et ensuite sur \"Create
merge request\".

Dans l\'onglet \"Changes\" il peut voir les modifications que vous avez
ajoutées. Pour accepter la merge request, cliquez sur le bouton
\"Merge\".

![](/tuto_git/_images/merge_request_2.png)

Le processus de vérification d\'une Merge Request est appelé \"faire une
review\". Le camarade a une lourde responsabilité : valider le
changement (en général, le code) proposé par son collègue. Si le code
introduit un problème, les deux sont tout autant responsables.

Quand votre camarade de groupe accepte votre merge request, son dépôt
distant aura les modifications que vous avez apportées. Il pourra
synchroniser ces modifications sur son dépôt local avec le distant avec
l\'habituel `git pull`.

Dans ce cours, vous êtes obligés d\'utiliser des Merge Requests pour
toutes modifications de la branche main!

## Les issues

Les issues sont des tickets qui permettent de suivre les problèmes et
les demandes de fonctionnalités d\'un projet. Vous pouvez les créer sur
GitLab depuis l\'interface web.

Créez une issue sur le dépôt distant de vos camarades de groupe et
ajoutez une description de l\'issue.

![](/tuto_git/_images/new_issue.png)

L\'image ci-dessous illustre la configuration d\'une issue que vous
devriez remplir. Vous devez ajouter un titre avec une description du
problème (dans le cadre de description).

![](/tuto_git/_images/edit_issue.png)

Remplissez les champs et cliquez sur \"Create issue\".

Dans cet issue, taguez l\'assistant qui vous encadre en utilisant \"@\"
et en tapant les premières lettres de son pseudo ou son login.
Lorsqu\'il aura répondu, fermez l\'issue.

## Utiliser Git dans PyCharm.

Utilisez PyCharm pour ouvrir le projet `my-project` qui a été créé
précédemment. Modifiez le fichier `README.md`.

Vous constatez que le fichier README.md est en bleu dans l\'explorateur
de fichiers. Cela signifie que le fichier a été modifié, mais n\'a pas
encore été ajouté au dépôt local.

![](/tuto_git/_images/pycharm_modification.png)

Cherchez dans le menu PyCharm \"Git\" et sélectionnez \"Commit\".

![](/tuto_git/_images/pycharm_menu_commit.png)

Un menu s\'ouvre (illustré ci-dessous).

![](/tuto_git/_images/pycharm_commit.png){width="100.0%"}

Dans l\'encadré [Commit Message]{.title-ref} vous devez ajouter un
message pour le commit. Dans l\'encadré supérieur, vous pouvez voir les
fichiers qui ont été modifiés.

Cliquez sur le bouton \"Commit\" pour faire le commit. Pour synchroniser
le dépôt local avec le dépôt distant, cliquez sur le bouton \"Push\"
dans le menu \"Git\".

La première fois que vous faites un push depuis Pycharm, vous devez
entrer votre nom d\'utilisateur et votre mot de passe pour vous
authentifier sur Gitlab.

![](/tuto_git/_images/pycharm_gitlab_auth.png){width="40.0%"}

Pour \"pull\" les modifications du dépôt distant, cliquez sur le bouton
\"Pull\" dans le menu \"Git\".

## Fin du tutoriel

Vous avez terminé ce tutoriel sur Git. C\'est l\'occasion de commencer
votre `projet phase 0<ref-projet0>`{.interpreted-text role="ref"} !

# Installation - Préembule

## Logiciels auxiliaires et environnements virtuel

Dans ce projet, vous **DEVEZ** utiliser Python 3. Il vous faut au moins
la version 3.6 de Python. Vous pouvez vérifier votre version de python à
tout moment avec la commande `python --version`.

En plus de Python et Flask, les logiciels suivants seront installés
automatiquement sur votre machine:

> -   [Werkzeug](https://palletsprojects.com/p/werkzeug/) implémente
>     WSGI, l\'interface standard Python entre l\'application et le
>     serveur.
> -   [Jinja](https://palletsprojects.com/p/jinja/) est un langage de
>     modèle qui gère le rendu des pages de votre application serveur.
> -   [MarkupSafe](https://palletsprojects.com/p/markupsafe/) vient avec
>     Jinja. Il échappe les données en entrée des utilisateurs dans les
>     modèles Jinja pour éviter l\'attaque par injection.
> -   [ItsDangerous](https://palletsprojects.com/p/itsdangerous/) permet
>     de signer les données et vérifier leur intégrité. C\'est utilisé
>     pour protéger les cookies des session Flask.
> -   [Click](https://palletsprojects.com/p/click/) est un framework
>     pour écrire des applications en ligne de commande. Il est utilisé
>     pour la ligne de commande \"flask\".

Nous vous conseillons d\'utiliser un *environnement virtuel* pour gérer
les dépendances pour votre projet, tant en développement qu\'en
production. Un *environnement virtuel* est un groupe indépendant de
bibliothèques Python. Il est conseillé d\'en créer un pour chacun de vos
projets. Ainsi, les paquets installés pour un projet n\'affecteront pas
les autres projets ou les packages du système d\'exploitation.

> Quel problème un environnement virtuel résout-il ? Plus vous avez de
> projets Python, plus il est probable que vous deviez travailler avec
> différentes versions des bibliothèques Python, ou même Python
> lui-même. Les bibliothèques plus récentes pour un projet peuvent
> casser la compatibilité dans un autre projet. Un environnement virtuel
> permet de ne pas ce soucier de ce genre de problème.

Python 3 est fourni avec le module
[venv](https://docs.python.org/3/library/venv.html#module-venv) pour
créer des environnements virtuels.

## Installation de Flask

Avant de commencer, nous vous rappelons que vous **DEVEZ** utiliser
Python 3. Voici les étapes pour partir sur de bonnes bases pour votre
projet:

1.  Créer un environnement

    > Créez un dossier pour votre projet avec et un dossier `venv` à
    > l\'intérieur:
    >
    > Sur Mac/Linux (y compris WSL):
    >
    > ``` console
    > $ mkdir base-project
    > $ cd base-project
    > $ python3 -m venv venv
    > ```
    >
    > Sur Windows (pas WSL):
    >
    > ``` bat
    > > mkdir base-project
    > > cd base-project
    > > python -m venv venv
    > ```
    >
    > Attention, il est possible que la commande `python` ne soit pas
    > accessible sur votre Windows. Dans ce cas, essayez de la remplacer
    > par `python3`. Si ça ne fonctionne pas, voyez les aides
    > ci-dessous.
    >
    > Le resultat des commandes ci-dessus est la création d\'un dossier
    > `base-project` contenant lui-même un dossier `venv`. Dans le
    > premier, vous mettrez tous les fichiers se rapportant au site que
    > vous allez créer. Ne touchez pas au second.

2.  Activer l\'environnement

    > Avant de commencer votre projet, activez l\'environnement
    > correspondant:
    >
    > Sur Mac/Linux
    >
    > ``` sh
    > $ . venv/bin/activate
    > ```
    >
    > Sur Windows:
    >
    > ``` bat
    > > venv\Scripts\activate
    > ```
    >
    > Votre commande shell changera avec le nom de l\'environnement
    > (*venv*).

3.  Installer Flask

    > Dans l\'environnement activé, utilisez la commande suivante pour
    > installer Flask:
    >
    > ``` sh
    > $ pip install flask
    > ```
    >
    > Flask est maintenant installé. Vous pouvez commencer le
    > [tutoriel](tutorial).

4.  Version de Flask

    > Nous utiliserons ici Flask 3.0.2. Vérifiez la version de Flask
    > avec :
    >
    > ``` sh
    > $ flask --version
    > ```

## Problèmes sur Windows

Notez que **si vous utilisez WSL, vous devez suivre les instructions
pour Linux** et non pour Windows.

### \'python\' n'est pas reconnu en tant que commande interne

Si vous n\'avez pas coché \"Add Python 3.\* to PATH\" lors de
l\'installation, alors vous ne pourrez pas taper \"python\" dans votre
ligne de commande, car le système ne saura pas où trouver `python`.
D\'abord, remarquez qu\'il est utile de lire les consignes correctement,
puisque c\'est indiqué visuellement dans le tutorial d\'installation
`python` qui vous est proposé.

Pour confirmer le problème, essayez de lancer directement python.exe en
trouvant le chemin complet. Il est en général installé dans
`%LOCALAPPDATA%\Programs\Python\`. Naviguez vers ce dossier en le tapant
dans la barre d\'adresse de l\'explorateur Windows, puis trouvez le nom
du dossier qui dépend de la version de Python, par exemple `Python311`.
Le chemin complet dans ce cas sera
`%LOCALAPPDATA%\Programs\Python\Python311\python.exe`.

Essayez de lancer `python` en ligne de commande en utilisant ce chemin
complet:

> ``` bat
> $ %LOCALAPPDATA%\Programs\Python\Python311\python.exe --version
> ```

Si cela fonctionne, le problème est bien la variable d\'environnement et
continuez. Sinon demandez de l\'aide à votre assistant.

Pour ajouter la variable d\'environnement:

> -   Appuyer sur la touche Windows + R
> -   Taper \"sysdm.cpl\" et cliquer sur OK
> -   Aller dans \"Paramètres système avancés\"
> -   Cliquer sur \"Variables d\'environnement\"
> -   Trouver \"Path\" ou \"PATH\" dans la liste des variables
>     utilisateur et sélectionner la ligne.
> -   Faites \"nouveau\" et ajoutez le chemin trouvé ci-dessus sans la
>     partie \"python.exe\", c\'est-à-dire seulement le chemin vers le
>     dossier qui le contient.

### Flask est introuvable

Il est possible que sur Windows la commande \"flask\" soit introuvable.
Dans ce cas, utilisez [python -m flask]{.title-ref} à la place. Il
arrive également qu\'une version embarquée de python, par exemple avec
Inkscape crée des conflits. Dans ce cas, utilisez le chemin complet vers
`python`, quelque chose comme
`C:\\Users\\tom\\AppData\\Local\\Programs\\Python\\Python311\\python.exe -m flask --version`,
ou changez l\'ordre des variables d\'environnement comme indiqué
ci-dessus.



