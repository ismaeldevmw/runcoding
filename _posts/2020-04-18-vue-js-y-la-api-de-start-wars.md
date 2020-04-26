---
layout: blog
permalink: /:title
title: Vue.js y la API de Start Wars
tags:
  - vue
date: 2020-03-07T17:41:58.851Z
thumbnail: /assets/images/uploads/start-wars-api.png
toc: true
---
La forma más fácil de trabajar con una API y tu sitio de JAMStack es directamente accediendo desde JavaScript. En este ejemplo, simplemente harás una petición HTTP al recurso y este se desplegara en pantalla. Vamos a ver como consumir la API de Start Wars con ayuda de Vue.js

## Primeros pasos
Vamos a crear el template HTML que donde vamos a desplegar el contenido.

``` html
<div id="app">
   <h1>Star Wars Films</h1>
   <table> 
      <thead>
         <tr>
            <th>Título</th>            
            <th>Director</th>
            <th>Productor</th>
            <th>Fecha de lanzamiento</th>
         </tr>
      </thead>
      <tbody>              
         <tr v-for="film in films">         
            <td>Attack of the Clones</td>            
            <td>George Lucas</td>
            <td>Rick McCallum</td>
            <td>2002-05-16</td>
         </tr> 
      </tbody>
   </table>    
</div>
```

## Request HTTP
Para realizar la petición podriamos apoyarnos de axios pero en realidad no hace falta, vamos a usar fetch la API nativa del navegador que nos viene bien para hacer peticiones simples.

``` javascript

const app = new Vue({
    el:'#app',
    data: {
        films:[]
    },
    created() {
        fetch('https://swapi.co/api/films')
        .then(res => res.json())
        .then(res => {
            this.films = res.results;
        });
    }
});
```

## Render Response
Perfecto, ya que tenemos los datos con la directiva v-for vamos a iterar cada elemento dentro de la vista, puedes revisar la API y ver que nodos tenemos a nuestra disposición o bien puedes examinar en consola la respuesta.

``` html
<div id="app">
   <h1>Star Wars Films</h1>
   <table> 
      <thead>
         <tr>
            <th>Title</th>            
            <th>Director</th>
            <th>Producer</th>
            <th>Release date</th>
         </tr>
      </thead>
      <tbody>              
         <tr v-for="film in films">         
            <td>{{ film.title }}</td>            
            <td>{{ film.director}}</td>
            <td>{{ film.producer}} </td>
            <td>{{ film.release_date}} </td>            
         </tr> 
      </tbody>
   </table>    
</div>
```

De esta forma podemos traer datos a nuestras vistas de diferentes APIs.