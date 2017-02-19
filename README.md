# Práctica: Primeros pasos en NodeJS

Enlace a la [descripción de la práctica](https://casianorodriguezleon.gitbooks.io/ull-esit-1617/practicas/practicatareasiniciales2.html)

# Desarrollo de Sistemas Informáticos

Enlace al [campus virtual](https://campusvirtual.ull.es/1617/course/view.php?id=1136)

# Versión en IAAS

El concepto de Infraestructura como Servicio (IaaS, Infrastructure as a Service) es uno de los tres modelos fundamentales en el campo del cloud computing, junto con el de Plataforma como Servicio (PaaS, Platform as a Service) y el de Software como Servicio (SaaS, Software as a Service).

Enlace al gitbook desplegado en el [IAAS de la Ull](http://10.6.128.132:8080/)


# Versión HEROKU

[Heroku](https://devcenter.heroku.com/categories/learning) es una plataforma como servicio de computación en la Nube que soporta distintos lenguajes de programación.

Enlace al gitbook desplegdo en [Heroku](http://dsipractica2.herokuapp.com/)

# Funciones de los scripts JS

Hemos hecho un port de los scripts realizados en Shell a JavaScript, con el fin de tener unos scripts más sencillos de comprender y universales.

## contributors.js
Script que tiene como función principal recopilar los contribuyentes (commits) a través de un archivo JSON previamente creado mediante otro script (git-log.js)

```javascript
let exec = require('child_process').exec
let mod = require('fs')
```
Hacemos uso de dos módulos, [Child Process](https://nodejs.org/api/child_process.html) y [FS](https://nodejs.org/api/fs.html), para conseguir recoger la ejecución del comando **git log** por shell, (*inicializado en el script git-log.js*), además de usar operaciones varías con ficheros.

```javascript
child =exec ('node git-log.js',function(error,stdout,stderr){
```
Se realiza la ejecución del script **git-log.js**, el cual realiza la ejecución del comando *git log* en shell, tomando todos los commit de los usuarios contribuyentes en el proyecto.

```javascript
let content = mod.readFileSync("contributors.json");
```
Se accede al fichero **contributors.json*, donde se aloja toda la información de los commit, para más tarde alojar esta información en el archivo MAINTAINERS (si no está creado, lo crea automáticamente) con un *append*

```javascript
mod.appendFile("../MAINTAINERS","<Autor: "+jsonContent[i].author+">\n"+"Last Commit: "+jsonContent[i].date+" ("+jsonContent[i].message+")"+"\n"+" "+"\n", function(err){
```

## deploy-gitbook.js
Script que tiene como función, como su nombre indica, desplegar un libro en gh-pages, formado por los archivos *.html* alojados en la carpeta _book

```javascript
let path = require('path')
let ghpages = require('gh-pages')
```
En este script necesitamos utilizar dos módulos, [path](https://nodejs.org/api/path.html) y [gh-pages](https://www.npmjs.com/package/gh-pages)

```javascript
ghpages.publish(path.join(__dirname,'../_book'),function(err){
```
La parte de codigo anterior se encarga de realizar un *publish* del contenido del directorio **_book**, a la rama *gh-pages*

## deploy-wiki.js
## generate-gitbook.js
## generate-wiki.js
## git-log.js
Este script lo hemos realizado por necesidad, con el fin de convertir lo que devuelve git-log en formato JSON para poder hacer un tratado mas comodo de la información sobre los commits, para posteriormente pasar su resultado al script **contributors.js**

```javascript
let exec = require('child_process').exec
```
Como concretamos anteriormente, se hace uso del módulo [Child Process](https://nodejs.org/api/child_process.html) para permitir la ejecución de comandos por shell.

```javascript
child =exec ('git log --pretty=format:\'{%n  \"commit\": \"%H\",%n  \"author\": \"%aN <%aE>\",%n  \"date\": \"%ad\",%n  \"message\": \"%f\"%n},\' $@ | perl -pe \'BEGIN{print \"[\"}; END{print \"]\n\"}\' | perl -pe \'s/},]/}]/\n\'' ,function(error,stdout,stderr){
```
Se realiza un **exec** con la ejecución del comando *git log*, con un formateo de la salida a JSON para, como comentabamos anteriormente, que nos resulte mas facil tratar con el.


# Autores
* [Aitor Bernal Falcón](https://chinegua.github.io/)
* [Néstor García Moreno](https://nestor-gm.github.io/)
* [Omar Mendo Mesa](https://ozzrocker95.github.io/)


