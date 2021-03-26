# AngularJS - Node.js - React.js - Javascript

## Sommaire
* Installation et Configuration
* Création projet
* Utiliser styles ou script

## Installation et Configuration

AngularJS:
`npm install angular@1.8.2`

Angular CLI:
`npm install -g @angular/cli`

Node.js et npm
[Node.js](https://nodejs.org/en/download/)
`node -v`
`npm -v`

## Création projet

Se situer dans le dossier voulu.

`ng new my-app`

`cd my-app`

`ng serve --open`
Ou
`ng serve // ouvrir http://localhost:4200/`

## Utiliser styles ou script

Modifier angular-cli.json ou angular.json

```
      "architect": {
        "build": {
          "builder": "@angular-devkit/build-angular:browser",
          "options": {
            //....
            "assets": [
              "src/favicon.ico",
              "src/assets"
            ],
            "styles": [
              "node_modules/bootstrap/dist/css/bootstrap.min.css",
              "src/styles.scss",
              "node_modules/lien_utile.css"
            ],
            "scripts": [
              "node_modules/lien_utile.js"
            ]
          },
```
