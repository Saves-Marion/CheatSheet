# HTML - CSS

## Sommaire
* Code type HTML
* Balises
  1.HTML
    * Structure
    * Listes
    * Tableau
    * Formulaire
    * Section
    * Générique
  2.CSS
    * Propriété mise en forme
    * Propriété couleur/fond
    * Propriété boîte
    * Propriété positionnement/affichage
    * Propriété listes
    * Propriété tableaux
    * Autres
* A savoir faire
  * Display/Flexbox
  * Position
  * Float/Clear
* Sources

## Code type HTML
```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Titre_Ma_Page_Visible_Onglet</title>
    </head>

    <body>
    //son code ici
    </body>
</html>
```

| Balise         | Description      | 
|:--------------:|:----------------:| 
| `<html>`       | Principale       | 
| `<head>`       | En-tête, info gé | 
| `<body>`       | Corps page       | 
| `<meta    />`  |                  | 
| `<link    />` | Lien             | 
| `<script>`     | Code javascript  | 
| `<style>`      | Code CSS         | 

**meta**

*En général:* `<meta name|http-equiv="Mot-clé" content="Valeur" />`

*TypeDoc et Encodage:* `<meta http-equiv="Content-Type" content="text/html; charset=utf-8" /> <meta charset="utf-8">`

*Description page:* `<meta name="description" content="Pour recherche Google" />`

*Robot indexer ou page page etc*

## Balises
### HTML

#### Structure

| Balise         | Description                       | 
|:--------------:|:---------------------------------:| 
| `<h1>-<h6> `   | Titre                             | 
| `<p>`          | Paragraphe                        | 
| `<a>`          | Lien hypertexte                   | 
|:--------------:|:---------------------------------:| 
| `<strong>`     | Mise valeur forte                 | 
| `<em>`         | Mise valeur normale               |  
| `<mark>`       | Mise valeur visuelle              | 
|:--------------:|:---------------------------------:| 
| `<img     />`  |  Image                            | 
| `<figure> `    | Figure (image,code)               | 
| `<figcaption>` | Description figure                | 
| `<audio>`      | Son                               | 
| `<video>`      | Video                             | 
| `<source> `    | Format source pour audio et video |
|:--------------:|:---------------------------------:| 
| `<br/>`        |   Retour ligne                    | 
| `<hr/>`        | Ligne séparation horizontale      |
|:--------------:|:---------------------------------:| 
| `<blockquote>` | Citation longue                   | 
| `<cite>`       | Citation titre                    | 
| `<q> `         | Citation courte                   |
|:--------------:|:---------------------------------:| 
| `<progress>`   | Barre Progression                 | 
| `<time> `      | Date/heure                        | 
|:--------------:|:---------------------------------:| 
| `<abbr>`       | Abbréviation                      | 
| `<sup> `       | Exposant                          | 
| `<sub> `       | Indice                            |  
| `<adress> `    | Adresse contact                   | 
| `<del>    `    | Texte supprimé                    | 
| `<ins>`        | Texte inséré                      | 
| `<dfn>`        | Définition                        | 
| `<kbd> `       |    Saisie clavier                 | 
| `<pre>`        | Code source (formaté)             | 

#### Listes

| Balise       | Description        | 
|:------------:|:------------------:| 
| `<ul>`       | Liste non num      | 
| `<ol>`       | Liste num          | 
| `<li> `      | El                 | 
|:------------:|:------------------:| 
| `<dl> `      | Liste de def       | 
| `<dt> `      | El à def           | 
| `<dd> `      | El définition      | 
  
#### Tableau

| Balise         | Description      | 
|:--------------:|:----------------:| 
| `<table> `     | Tableau          | 
| `<caption> `   | Titre tableau    | 
|:--------------:|:----------------:| 
| `<thead>  `    | En-tête          | 
| `<th>  `       |Cellule d'en-tête | 
|:--------------:|:----------------:| 
| `<tbody>  `    | Corps            | 
| `<tr>    `     | Ligne            | 
| `<td>   `      | Cellule          | 
| `<tfoot>  `    | Pied             | 
  
#### Formulaire

| Balise         | Description                  | 
|:--------------:|:----------------------------:| 
| `<form>   `    | Formulaire                   | 
| `<fieldset>`   | Groupe champs                | 
| `<legend>  `   | Titre groupe champs          | 
| `<label>  `    |  Libellé un champ            | 
| `<input   />`  | Champ                        | 
| `<textarea> `  | Saisie Multiligne            | 
| `<select>   `  | Liste déroulante             | 
| `<option>   `  | Element liste déroulante     | 
| `<optgroup>`   | Groupe d'el liste déroulante | 
  
#### Section

| Balise         | Description           | 
|:--------------:|:---------------------:| 
| `<header> `    | En-tête               | 
| `<nav>   `     | Navigation            | 
| `<footer>  `   | Pied page             | 
| `<section> `   |  Section              | 
| `<article> `   | Article               | 
| `<aside>   `   | Info complémentaires  | 
  
#### Générique

| Balise         | Description        | 
|:--------------:|:------------------:| 
| `<span> `      | Inline             | 
| `<div> `       | Div                | 
| class          | Class (non unique) | 
|id              |  Id (unique)       | 


### CSS

**Selectionner un id #id{} et class .class{}**

#### Propriété mise en forme

| Balise               | Description                | Valeur                                         | 
|:--------------------:|:--------------------------:|:----------------------------------------------:|  
| font-family          | Nom Police                 | serif, police 1                                | 
| @font-face           | Police perso               | nom+source                                     | 
| font-size            | Taille text                | 1em,10px,100%                                  | 
| font-weight          | Gras                       | bold, normal                                   | 
| font-style           | Italique                   | italic, oblique, normal                        | 
| font-variant         | Petites capitales          | small-caps, normal                             | 
| font                 | tous hors family           |                                                | 
|:--------------------:|:--------------------------:|:----------------------------------------------:| 
| text-decoration      | Effet ligne                | underline, overline, line-through, blink, none | 
| text-transformation  | Capitales                  | capitalize,lowercase,uppercase                 |  
| text-shadow          | Ombre                      | horipx vertipx fondupx couleur                 | 
|:--------------------:|:--------------------------:|                                                |  
| text-align           |  Alignement hori           | left,center,right,justify                      | 
| vertical-align       | Alignement verti*          | baseline, middle, sub, super, top, bottom      |  
| line-height          | Hauteur ligne              | 10px,100%,normal                               |  
| text-indent          | Alinea                     | px                                             |  
| white-space          | Césure                     | pre,nowrap,normal                              | 
| word-wrap            | Césure forcé               | break-word,normal                              | 

*(si tableau ou inlign-block)

#### Propriété couleur/fond

| Balise                  | Description                | Valeur                                      | 
|:-----------------------:|:--------------------------:|:-------------------------------------------:|  
| color                   | Couleur text               | nom, rgb(0,254,0),rgba(0,0,0,100), #FFFFFF  | 
| background-color        | Couleur fond               |                                             | 
| background-image        | Image fond                 | url('img.jpg')                              | 
| backgroung-attachment   | Fixe                       | fixed,scroll                                | 
| background-repeat       | Répétition                 | repeat-x,repeat-y,no-repeat,repeat          | 
| background-position     | Position                   | (x,y),top,center,bottom,left,right          | 
| opacity                 | Transparence               | 0.5                                         | 

#### Propriété boîte

| Balise                                  | Description                | Valeur                                              | 
|:---------------------------------------:|:--------------------------:|:---------------------------------------------------:|  
| width / min-width / max-width           | Largeur /min/max           | 100px,80%                                           | 
| height / min-height / max-height        | Hauteur  /min/max          | 100px,80%                                           | 
| margin / margin-top/left/right/bottom   | Marge extérieur            | 5px 5px 5px 5px / 5px                               | 
| padding                                 | Marge interne              | fixed,scroll                                        | 
| border-width                            | Epaisseur                  | 5px                                                 | 
| border-color                            | Couleur                    |                                                     | 
| border-style                            | Type                       |solid,dotted,dashed,double,groove,ridge,inset,outset | 
| border-radius                           | Arrondi                    |5px                                                  | 
| border-shadow                           | Ombre                      | horipx,vertipx,fondupx,couleur                      | 

#### Propriété positionnement/affichage

| Balise                 | Description                              | Valeur                                                   | 
|:----------------------:|:----------------------------------------:|:--------------------------------------------------------:|  
| display                | Type element                             | block, inline, inline-block, table, table-cell, none...  | 
| visibility             | Visibilité                               | visible, hidden                                          | 
| clip                   | Affichage une part                       | rect (hautpx, droitepx, baspx, gauchepx)                 | 
| overflow               | Dépassement                              | 	auto, scroll, visible, hidden                          | 
| float                  | Flottant                                 | left, right, none                                        | 
| clear                  | Arret d'un flottant                      | left, right, both, none                                  | 
| position               | Positionnement                           |relative, absolute, static                                | 
| top/bottom/left/right  | Position par rapport                     |5px                                                       | 
| z-index                | Ordre affichage, +grand + devant/dessus  | 10                                                       | 

#### Propriété listes

| Balise                 | Description            | Valeur                                                                                  | 
|:----------------------:|:----------------------:|:---------------------------------------------------------------------------------------:|  
| list-style-type        | Type liste             |disc, circle, square, decimal, lower-roman, upper-roman, lower-alpha, upper-alpha, none  | 
| list-style-position    | Position en retrait    | inside, outside                                                                         | 
| list-style-image       | Puce personnalisé      | url('puce.png')                                                                         | 
| list-style             | Combinaison            |                                                                                         | 

#### Propriété tableaux

| Balise                 | Description                 | Valeur             | 
|:----------------------:|:---------------------------:|:------------------:|  
| border-collapse        | Fusion bordure              | collapse, separate | 
| empty-cells            | Affichage cellule vide      | hide, show         | 
| caption-side           | Position titre              | bottom, top        | 

#### Autres

| Balise       | Description       | Valeur                                                                                     | 
|:------------:|:-----------------:|:------------------------------------------------------------------------------------------:|  
| cursor       | Curseur souris    |crosshair, default, help, move, pointer, progress, text, wait, e-resize, ne-resize, auto... | 

## A savoir faire

#### Display/Flexbox

Block: retour à la ligne.

Inline dans un block à la suite les uns des autres.

**Flexbox**

Parent

display: flex;

flex-direction: row (gauche à droite), column (haut en bas), truc-reverse; (est-ce que les éléments vont être en ligne ou en colonne)

flex-wrap: nowrap(1ligne), wrap(ligne de top à bottom avec -reverse);

*position horizontale*
justify-content: flex-start(collé le plus à gauche container), flex-end, center, space-between(plus d'espace entre item touche à g et à d), space-around/evenly(espace g et d egal plus grand possible);

*position verticale*
align-item: flex-start(collé haut), flex end, center, strech (etire touche haut et bas), baseline;

*position block, ligne multiple*
align-content: même que align item;

-------------------

Enfants

order: +petit gauche haut +grand bas droite

flex-grow: 4 = 4fois plus de place qu'un1;

flex-shrink: nb positif

*alignement vertical*
align-self: auto | flex-start | flex-end | center | baseline | stretch;

#### Position

Fixed: va garder sa position dans l'ecran meme si on scroll, défini à partir du plus gros container. 

Relative: va se déplacer par rapport à sa place de base.

Absolute: se déplace par rapport à son parent.

#### Float/Clear

Float-right fait en sorte que l'element soit à la droite de son container, les restes des éléments se disposent autour de lui normalement.

Clear-right fait en sorte que la droite de l'élément flottant ne contienne rien. 

## Sources
OpenClassroom
