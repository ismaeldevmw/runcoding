---
layout: blog
permalink: '/:title'
title: ¿Cómo usar npm y publicar un paquete?
tags: 
    - javascript
thumbnail: /assets/images/uploads/npm-miniatura.jpg
toc: true
---
npm (node package manager)  es el registro de software más grande del mundo. Los desarrolladores de código abierto de todos los continentes usan npm para compartir y tomar prestados paquetes, y muchas organizaciones también usan npm para administrar el desarrollo privado. 

## Iniciar un proyecto
Antes de crear un proyecto nuevo lo correcto es tener las últimas versiones de node y npm actualizadas con el fin de evitar conflictos por bugs o errores, además así evitamos fallos de seguridad que pudieran haber dentro de nuestras aplicaciones.
```bash
node -v 
npm -v 
npm install -g npm@latest 
```
Para iniciar un proyecto de node podemos hacer con el asistente o indicarle si a todo y que este se cree con los valores por defecto.
```bash
npm init
npm init -y
```
Para no establecer algunos valores cada que nos los pida el asistente de proyecto npm podemos establecer valores globales dentro en la configuración. 
```bash
npm set init.author.email "ismael@mail.com" 
npm set init.author.name "Ismael López" 
npm set init.license "MIT" 
```

## Instalación de dependencias
Cuando instalamos dependencias se nos crea una carpeta llamada ***node_modules*** esta carpeta es importante para que tu proyecto funcione, pero no debe incluirse en tu repositorio. Para omitirlo se crea un archivo .gitignore y dentro le indicamos el directorio ***node_modules/***
```bash
node_modules/
```
Para instalar dependencias debemos tener en cuenta si van a ser dependencias del proyecto, dependencias de desarrollo o son dependencias opcionales.
```bash
npm install moment  --save // instalacion como dependencia del proyecto
npm i moment -S // metodo corto de instalacion como dependencia del proyecto
npm install date-fns --save-dev // intalacion como dependencia de desarrollo
npm i date-fns -D // metodo corto de instalacion como dependencia de desarrollo
npm install eslint -O // instala una dependencia de forma opcional
npm install -g nodemon // instala una dependencia de forma global
npm fund // este comando permite ver que paquetes buscan formas de fincanciar su trabajo
npm install react --dry-run // simula la instalacion y nos retorna todo lo que se instalaria
npm install webpack -f // el flag -f forza la instalacion independientemente de que ocurran errores
npm install json-server@0.15.0 // instala una version en especifico del paquete
```
## Actualizar paquetes
Revisar que paquetes disponen de nuevas versiones
```bash
npm outdate
```
Para ver un ouput mas detallado
```bash
npm outdate --dd
```
Actualizar los paquetes que no estan en la ultima version
```bash
npm update
```
Actualizar un paquete especifico
```bash
npm install json-server@latest
```
## Eliminar paquetes
Eliminar un paquete de ***node_modules*** y del archivo ***package.json***
```bash
npm uninstall json-server
```
Desinstalar un paquete de todo ***node_modules*** pero no del archivo ***package.json***
```bash
npm uninstall webpack --no-save
```
## Package lock y uso de los simbolos ***^*** y ***~***
El archivo package.lock nos sirve como control de versiones de los paquetes que hemos instalado, pero es opcional mantenerlo dentro de tu repositorio.
A la hora de establecer versiones debemos tener en cuenta si las modificacione que realizaste son un cambio mayor(major), cambio menor(minor) o el cambio fue solo un parche(patch)
![Versionado](https://dev-to-uploads.s3.amazonaws.com/i/s4naxx0dkmpo9az3o3bs.jpg)

Dentro de la configuracion del package.json en cada dependencia existen dos simbolos que nos permiten controlar como vamos a recibir esas actualizaciones hacia nuestro proyecto.
***^***
Si mantenemos el caret dentro de la configuracion de nuestro package.json estamos garantizando que cuando realizemos una actualizacion o tengamos un cambio que tengamos que realizar, va hacer una actualizacion de los cambios menores y de los parches o bug fixes.
***~*** 
Establece que vamos a recibir actualizaciones o cambios solamente de los parches o bug fixes.

## Solución de problemas
Uno de los problemas que llegan a suceder cuando estamos trabajando entre branchs con otros desarrolladores, es que nuestros archivos almacenados en un módulo no estén correctamente instalados o tengamos una versión anterior para esto vamos a ejecutar un comando que nos va a dar la seguridad de que estamos limpiando la caché que pueda existir y que nos este causando conflictos.
```bash
npm cache clean --force
```
para verificar que se haya eliminado ejecutamos...
```bash
npm cache verify
```
Una herramienta que puedes utilizar para eliminar carpetas con el mismo comando en cualquier sistema operativo donde la instales es ***rimraf***.
```bash
sudo npm install -g rimraf
```
y el comando para eliminar una carpeta con está librería es...
```bash
rimraf node_modules
```
## Seguridad
Para verificar si no existe alguna vulnerabilidad o conflicto en alguna de las librerías de nuestro proyecto ejecutamos el siguente comando.
```bash
npm audit
```
Para resolver los conflictos encontrados podemos usar los siguientes comandos.
```bash
npm audit --json //nos da un detalle de las vulnerabilidades
npm update eslint-utils --depth 2 // intenta actualizar librerías de segundo nivel que nos den conflictos con eslint-utils
npm audit fix //nos garantiza que los detalles del conflicto sean resueltos
```
Como recomendación puedes utilizar [Snyk](https://snyk.io), está herramienta te permite verificar y estart al día de los conflictos de tu proyecto.

## Crear un paquete
Creamos una función
```javascript
const names = [
    'camilo',
    'andres',
    'luisa',
    'ahmed',
    'sandra',
    'antonio',
    'carlos'
]
const randomNames = () => {
    const name = names[Math.floor(Math.random() * name.length )];
    console.log(name)
}
module.exports = { randomNames }
```
Creamos la  configuración de bin para asegurarnos que es un paquete instalable ***global.js***
```javascript
#! /usr/bin/env node
let random = require('../src/index')
random.randomNames();
```
Agregamos la configuración de bin al packages.json
```javascript
"bin": {
    "random-names": "./bin/global.js"
  },
  "preferGlobal": true
```
Para probar nuestro paquete, creamos una referencia de forma global de nuestro paquete, tenemos que estar en la carpeta del proyecto.
```bash
sudo npm link
sudo npm i -g /home/rulo/PlaziMaster/cursos/npm/random-name
```
## Publicar el paquete en npmjs.com
Para publicar un paquete primero debemos registrarnos en la páginal [npmjs.com](https://www.npmjs.com/). Una vez lo tengas creado vamos a ejecutar los siguientes comandos.
Crear el usuario de npm que nos pedira las credenciales que acabamos de registrar en la página.
```bash
npm adduser
```
Publicar el paquete es el paso final para mandarlo a los servidores de npm.
```bash
npm publish
```
Cuando realizemos cambios al proyecto debemos indicarle a npm que tipo de cambio hemos hecho para que actialize nuestra versión y pueda volver a publicar los cambios.
```bash
npm version patch
npm version minor
npm version major
```
Genial, has aprendido ha configurar tu archivo package.json, gestionar tus dependencias, descargar versiones específicas de librerías y publicar tus propias librerías para NPM.

Si quieres aprender más acerca de desarrollo web suscribete a [mi canal](https://youtube.com/runcoding) estoy subiendo contenido cada semana, espero que te sirva el contenido que estoy creando, gracias por leerme. Nos vemos hasta la proxima. 😀