---
layout: blog
permalink: /:title
title: "El JAM Stack: Javascript, API´s y Markup"
tags:
  - javascript
date: 2020-04-18T21:53:58.381Z
thumbnail: /assets/images/uploads/jekyll-netlify-degradado.png
toc: true
---
{% youtube "https://www.youtube.com/watch?v=DJoGU5xuN_c" %}

Cuando hablamos de un stack normalmente pensamos en un backend, un fronted, bases de datos, etc. pero es solo un conjunto de tecnologías que usamos para llevar a cabo el desarrollo de un proyecto. El JAMStack no es en realidad un conjunto de tecnologías. Es una nueva forma de construir sitios web y apps que deliberen mejor performance, alta seguridad, escalamiento de bajo costo y una mejor experiencia de desarrollo.

![undefined](/assets/images/uploads/JAM.jpg)

## ¿Qué es el JAMstack?

Tu proyecto es construido con el JAMstack si reúne tres criterios clave:

* Javascript
  Cualquier lenguaje dinámico que durante el ciclo  request/response de nuestra aplicación sea manejado por Javascript, corriendo enteramente en el cliente. Esto puede ser cualquier framework, librería o incluso vanilla JavaScript.
* APIs
  Todo el proceso del server-side o acciones de la base de datos son abstraídas dentro de APIs reusables, accesso sobre HTTP con JavaScript. Estas pueden ser custom-build o servicios de terceros.
* Markup
  El template de markup debe ser pre construido en tiempo de despliegue, usualmente se usa un sitio generador de contenido o construido con herramientas para web apps.

## ¿Cuando tu sitio podría no estar construido con el JAMstack?

Cualquier sitio quedependa de un estrecho acoplamientoentre cliente y servidor no está construido con el JAMstack. Estos podrían incluir:

* Un sitio construido con un server-side CMS como Wordpress, Drupal, Joomla, o Squarespace.
* Un monolitico server-run web app que se basa en Ruby, Node, u otro lenguaje de backend.
* Una single page app que use isomorphic rendering para construir vistas en el servidor en tiempo de ejecución.

Esta semana experimente creando varias páginas web con diferentes recursos que encontré en la web, que me ayudaron a realizar el desarrollo más rápido. En este caso probé Jekyll, es un generador de páginas estáticas construido sobre Ruby. Además también lo combine con Netlify que te ayuda a gestionar el contenido de tu sitio generado precisamente con el JAMstack, también tiene hosting gratuito y muchas otras características que te permiten crear sitios web profesionales.

Otra de las herramientas que utilice fue GitHub, dirás oye pero que no Netlify te ofrece el hosting así es, pero para gestionar el contenido necesariamente lo tienes que alojar en GitHub y una vez configurado te tienes que loguear con tu cuenta y ya puedes acceder a un panel muy chulo como este.

![undefined](/assets/images/uploads/NetlifyCMS.JPG)

Lo interesante de usar Netlify es que te ofrece muchas opciones de autenticación de usuarios y de customización, aun no he probado otras alternativas para gestionar el contenido pero si conoces algunas que os han servido no dudes en dejarlas en los comentarios.

## Conclusión

El JAMstack sin duda es una muy buena alternativa para pequeños y grandes negocios que nos ofrece la separación y control de nuestro código en desarrollo y debugging. Es muy versátil ya que podemos usar frameworks como Angular, React o Vue por mencionar los más populares y muchas otras propias del desarrollo web como Sass, Webpack, Gulp, PWA... Y claro no olvidar que el costo es mucho menor ya sea en la cuestión económica como a nivel de desarrollo ya que no tenemos que invertir mucho tiempo en aprender un lenguaje de backend si lo único que quieres es crear un blog o el sitio web de tu empresa y posteriormente si necesitas algo más pulido tienes la ventaja que puedes escalar integrando tu web con API´s y la característica no menos importante la carga mas rapida de las paginas web ya que el contenido no tiene que pasar por un lenguaje de backend simplemente es servido al browser del usuario.

<!--EndFragment-->

<iframe width="560" height="315" src="https://www.youtube.com/embed/DJoGU5xuN_c" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
