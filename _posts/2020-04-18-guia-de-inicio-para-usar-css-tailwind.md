---
layout: blog
permalink: /:title
title: Guía de inicio para usar CSS Tailwind
tags:
  - css
date: 2020-03-21T17:33:13.261Z
thumbnail: /assets/images/uploads/comenzando-con-tailwind-css-youtube-thumbnail.png
toc: true
---
{% youtube "https://www.youtube.com/watch?v=x6gDb7HVo1Q" %}

## Instalación y configuración del proyecto
Iniciamos un nuevo proyecto npm e instalamos las líbrerias que vamos a utilizar.
``` bat
mkdir tailwind-css-project
cd tailwind-css-project
npm init -y
npm i tailwindcss autoprefixer postcss-cli
```
Creamos los archivos de configuración de tailwind css.
``` bat
npx tailwindcss init
```
Creamos un archivo para las configuraciones de post css.
``` console
touch postcss.config.js
```
Abrimos el proyecto con Visual Studio Code (VS Code).
``` console
code .
```
Puedes utilizar la siguiente extensión para tu editor de código que te ayudara al escribir las clases de tailwind css.
> Extensión recomendada para VS Code.
[Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)

Configuramos en archivo __postcss.config.js__
``` javascript
module.exports = {
  plugins: [
    require('tailwindcss'),
    require('autoprefixer')
  ]
}
```
Vamos a crear el archivo base de tailwind que hará que funcione agregue los componentes que necesita para funcionar. A este archivo lo llamaremos css/__tailwind-base.css__
``` css
@tailwind base;

@tailwind components;

@tailwind utilities;
```
Ahora creamos un nuestro archivo __index.html__ en una carpeta que nombraremos public, entonces la ruta serías __public/index.html__
``` html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <h1>Hello world</h1>
</body>
</html>
```
Ahora vamos a crear el archivo de salida __style.css__ que importamos en el __index.html__, para ello creamos un comando en la sección de scripts del __package.json__
``` javascript
"build": "postcss css/tailwind-base.css -o public/css/style.css"
```
Para finalizar en la terminal ejecutamos el siguiente comando que construirá el archivo de __styles.css__.
```bat
npm run build
```
> Aquí me surgio un problema y es que no me permitía la ejecución del script y tuve que ejecutar el siguiente comando en mi configuración de node.
``` console
npm config set ignore-scripts false
```
Si alguien tiene el mismo problema espero le sirva. Continuemos.

## Principios de Tailwind
+ Responsive Design
+ Mobile First
+ Utility First

## Colores
Los elementos a los que se les puede cambiar el color son:
+ Fondo
+ Texto
+ Bordes
+ Placeholder

Actualmente tenemos un archivo de configuración vacío pero ahora queremos agregar la configuración que tailwind tiene por defecto para ello vamos a ejecutar el siguiente comando que nos creará dicho archivo.
``` console
npx tailwindcss init tailwind.config.full.js --full
```
Ahora aprendamos a usarlo. Vamos al archivo __index.html__ y en la etiqueta __h1__ le agregamos las siguientes clases.
``` html
  <h1 class="bg-yellow-500 text-white">Hello world</h1>
  <input class="border-2 border-blue-500 placeholder-green-500" type="text" placeholder="Ingresa texto">
```
Como pueder ver todas estás clases existen gracias a que agregamos la configuración anterior de tailwind.

## Dimensiones y espacios
Tailwind tiene un sistema configurable de espacios y tamaños, regresando a nuestro archivo de configuración __tailwind.config.js__ aquí hau un atributo llamado spacing.
Como dato 1rem equivale a 16px;
``` javascript
spacing: {
      px: '1px',
      '0': '0',
      '1': '0.25rem',
      '2': '0.5rem',
      '3': '0.75rem',
      '4': '1rem',
      '5': '1.25rem',
      '6': '1.5rem',
      '8': '2rem',
      '10': '2.5rem',
      '12': '3rem',
      '16': '4rem',
      '20': '5rem',
      '24': '6rem',
      '32': '8rem',
      '40': '10rem',
      '48': '12rem',
      '56': '14rem',
      '64': '16rem',
    },
```
Estas propiedades pueden controlar las dimensiones o espacios.
+ Height
+ Width
+ Margin
+ Padding

Veamos como modificar estás propiedades.
``` html
<h1 class=" h-16 w-32 bg-yellow-500 text-white">Hello world</h1>
```
Tailwind también nos permite usar porcentajes y estos los maneja en fracciones.
``` html
<h1 class=" h-16 w-1/2 bg-yellow-500 text-white">Hello world</h1>
```
Ahora veamos como modificariamos las propiedades de margin y padding.
``` html
  <h1 class=" h-32 w-1/5  pt-8 pl-4 ml-8 mt-16 mb-16 bg-yellow-500 text-white">Hello world</h1>
```
También podemos cambiar las propiedades respecto al eje x, y. Esto nos permite agregar en ambos lados la misma cantidad de unidades.
``` html
<h1 class=" h-32 w-1/5 my-8 bg-yellow-500 text-white">Hello world</h1>

<!-- mx-auto nos permite centrarlo-->
<h1 class=" h-32 w-1/5 my-8 mx-auto bg-yellow-500 text-white">Hello world</h1>
```
Para el padding podemos aplicarlo en nuestro input de la siguiente manera.
``` html
<input class="py-1 px-4 border-2 border-blue-500 placeholder-green-500" type="text" placeholder="Ingresa texto">
```
## Recursos
Aqui te dejo los enlaces de la documentación oficial para que la repases más a fondo y otros recursos donde hay mucha más información donde puedas seguir aprendiendo y buscando inspiración.

[https://tailwindcss.com/docs](https://tailwindcss.com/docs)
[https://github.com/aniftyco/awesome-tailwindcss](https://github.com/aniftyco/awesome-tailwindcss)
[https://refactoringui.com/book](https://refactoringui.com/book/)