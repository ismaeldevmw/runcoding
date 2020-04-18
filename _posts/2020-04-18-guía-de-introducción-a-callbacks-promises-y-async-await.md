---
layout: blog
permalink: /:title
title: Guía de introducción a Callbacks, Promises y Async/Await
tags:
  - javascript
date: 2020-03-14T17:37:47.853Z
thumbnail: /assets/images/uploads/miniatura-post-async-await.png
toc: "true"
---
Esta es una guía de encontrarás conceptos básicos de asincronismo en JavaScript que nos permitirán tener aplicaciones mantenibles con código simple y fácil de leer como si de una receta de cocina se tratara, verás ejemplos prácticos. También puedes ver la [lista de reproducción](https://www.youtube.com/playlist?list=PL9U8K1aoRM6xt2_WkUxvqeogVeJwGJjn6) dedicada a estos temas en el canal de YouTube.

## Callbacks
Es una función "X" que se usa como argumento de otra función "Y". Cuando se llama a "Y", está ejecuta "X".

Para conseguirlo, usualmente lo que se pasa a "Y" es el puntero de "X". Veamos como funciona. 

### Ejemplo
Normalmente el ejemplo más sencillo de representar un *callback* es usando la función setTimeout(function, time, arg?) que los que hace es recibir una función a la cual se le conoce como *callback*, como segundo parámetro recibe el tiempo en mili segundos, opcional mente puede o no recibir argumentos.

```javascript
setTimeout(function() {
  console.log('Hello world')
}, 2000)
```
Si aún no queda claro vamos a ver más ejemplos y así lo vemos más a profundidad.

Supongamos que tenemos una función calculate y necesita dos argumentos y adicionalmente va recibir una function que sera el *callback* que me devolvera.

```javascript
function calculate(n1, n2, operation) {
  return operation(n1, n2);
}
```
La funcion operation podria ser una función llamada add que lo que va hacer es solo sumar los dos argumentos recibidos y nos devolverá el resultado.

```javascript
function add(n1, n2) {
  return n1 + n2;
}
```

Entonces a la hora de ejecutar nuestra función calculate lo que va hacer es pasar el puntero de estos dos argumentos a la function add que nos devolverá la suma de estos dos valores, independientemente de si hayamos hecho otras acciones antes.

```javascript
const result = calculate(2, 9, add);
console.log(result); // 11
```

### Ventajas
+ __Simple:__ son conceptual mente simples. Pasas una función que quieras que se ejecute después.
+ __Universal:__ corren donde sea. No requiere de un *transpilador*.

### Desventajas
+ __Flujo poco intuitivo:__ requieren que te muevas dentro del código para comprender el flujo del mismo.

> __Consejo:__ Uso de callbacks
Muchas de las funciones del core de *Node.js* están basadas en *callbacks*, no obstante, a partir de la versión de *ECMASCRIPT 6 (ES6)* se ha simplificado el código con el uso de las *promises*. Usa los *callbacks* lo menos posible para mantener un código limpio.

### Ejemplo practico callbacks
```javascript
const booksDb = [
  {
    id: 1,
    title: 'Clean Code'
  },
  {
    id: 2,
    title: 'The pragmatic programmer'
  },
  {
    id: 3,
    title: 'Web Development with Node.js'
  }
];

function getBookById(id, callback) {
  // dentro de booksDb va a buscar el objeto que tenga como book.id el mismo que le paso como parámetro id
  const book = booksDb.find(book => book.id === id);
  if (!book) {
    const error = new Error();
    error.message = 'Book not found!'
    // el primer paŕametro de un callback siempre es un error
    return callback(error)
  }

  callback(null, book);
}

// Ejecutemos la función
getBookById(2, (err, book) => {
  if (err) {
    return console.log(err.message);
  }

  return console.log(book);
})
```
Todo bien hasta aquí, pero como podemos ver cada que yo tenga que pasar un *callback* a mi función tengo que controlar los errores haciendo validaciones, lo cuál le agrega más complejidad e incluso llegaremos a caer en el *callback hell* y nuestras aplicaciones resultaran muy difíciles de mantener.

## Callback Hell
Cuando se hace un uso masivo de los *callbacks* podemos caer muy fácil en el *callback hell*, veamos que es esto, que problemática nos trae.

```javascript
// vamos a agregar una propiedad authorId
const booksDb = [
  {
    id: 1,
    title: 'Clean Code',
    authorId: 1
  },
  {
    id: 2,
    title: 'The pragmatic programmer',
    authorId: 2
  },
  {
    id: 3,
    title: 'Web Development with Node.js',
    authorId: 3
  }
];

// y creamos también otra nueva base de datos en memoria
const authorsDb = [
  {
    id: 1,
    name: 'Robert C. Martin'
  },
  {
    id: 2,
    name: 'Steve Forest'
  }
];

function getBookById(id, callback) {
  const book = booksDb.find(book => book.id === id);
  if (!book) {
    const error = new Error();
    error.message = 'Book not found!'
    return callback(error)
  }

  callback(null, book);
}

// vamos a crear una función que se encargue de buscar el autor
function getAuthorById(id, callback) {
  const author = authorsDb.find(author => author.id === id);
  if (!author) {
    const error = new Error();
    error.message = 'Author not found!'
    return callback(error)
  }

  callback(null, author);
}
// ¿Dónde ocurre el callback hell?
getBookById(2, (err, book) => {
  if (err) {
    return console.log(err.message);
  }
  console.log(book);

  // una vez que ya conseguí un book vamos a conseguir el author con el authorId
  getAuthorById(book.authorId, (error, message) => {
    // estar validando errores se vuelve tedioso
    if(error) {
      return console.log(error.message)
    }
    
    // si encontro el author muestralo
    console.log(`This book ${book.title} was written by ${author.name}`);
  });
});
```
Como vemos se incrementa la complejidad entre más vamos anidando el llamado a otras funciones, pero veamos como resolver esto con ayuda de las promesas.

## Promises
Las *promesas* son una forma de manejar la sincronía en javascript que surgío a partir de la versión de *ES6* pero ¿Qué son en realidad?

__Promesa:__ Es un objeto que representa la terminación o el fracaso eventual de una operación asíncrona.

Esencialmente, una promesa es un objeto devuelto al cual se adjuntan funciones *callback*, en lugar de pasar *callbacks* a una función.

Todo surge a partir de un objeto primitivo *Promise* que recibe como constructor un callback.
```javascript
const promise = new Promise(callback);
```
Esté constructor tiene que corresponder a una función de este tipo.
```javascript
function executor(resolve, reject) {
  //si funciona
  resolve();

  // si falló
  reject();
}
```
Recuerda cuando se le pasa son argumentos, cuando se reciben son parámetros. Y ¿Quién le pasa estos argumentos a está función?, pues el constructor automáticamente lo hace por nosotros y nos provee de estas dos funciones. Estos nombres pueden ser lo que les plazca pero por convención se suelen llamar *__resolve__* y *__reject__* para referirse a ellos.

Entonces el uso sería de esta forma.
```javascript
const promise = new Promise(executor);
```
Una vez que creemos nuestro objeto *promise* y le hallamos pasado nuestra función de *callback*, inmediatamente este objeto va disponer de tres métodos __(promise.then().catch().finally())__.

Estos métodos son bastante útiles por ejemplo en el __then__ va a venir la data siempre y cuando el método __resolve()__ se haya invocado.

En el __catch__ va a venir el error o el mensaje que hayamos puesto en el __reject()__ siempre y cuando haya ocurrido un error.

Y el método __finally__ siempre se va ejecutar no importa si haya ocurrido un error o no.

### Ventajas
+ __Fácilmente enlazable:__ se pueden enlazar fácilmente para manejar flujos asíncronos complejos sin tener que recurrir a más anidaciones como se requiere en *callbacks*.
+ __Poderoso:__ proporciona una capacidad excepcional para componer operaciones asíncronas complejas.

### Desventajas
+ __Excepciones que desaparecen:__ Se debe declarar *catch()* para manejar errorres en lugar del tradicional *try/catch*.

> __Consejo:__ Promesas
Usa promesas en vez de *callbacks* para mantener el *standard*, ten cuidado en caer en el *promise hell* por la excesiva anidación.

### Ejemplo practico *promises*
```javascript
const booksDb = [
  {
    id: 1,
    title: 'Clean Code',
    authorId: 1
  },
  {
    id: 2,
    title: 'The pragmatic programmer',
    authorId: 2
  },
  {
    id: 3,
    title: 'Web Development with Node.js',
    authorId: 3
  }
];

const authorsDb = [
  {
    id: 1,
    name: 'Robert C. Martin'
  },
  {
    id: 2,
    name: 'Steve Forest'
  }
];

// refactorizemos la función a promesa
function getBookById(id) {
  return new Promise ((resolve, reject) => {
    const book = booksDb.find(book => book.id === id);
    if (!book) {
      const error = new Error();
      error.message = 'Book not found!';
      reject(error);
    }

    resolve(book);
  });
}

function getAuthorById(id) {
  return new Promise(() => {
    const author = authorsDb.find(author => author.id === id);
    if (!author) {
      const error = new Error();
      error.message = 'Author not found!';
      reject(error);
    }

    resolve(author);
  });
}

// Ejecutamos las promesas
getBookById(1).then(book => {
  return getAuthorById(book.id);
}).then(author => {
  console.log(author);
}).catch(error => {
  console.log(error.message)
});
```
Y este sería el uso de las promesas vamos a ver ahora como simplificar esto todavía más usando *async/awai*t.

## Async/Await
__Async:__ cuando se llama a una función *async* esta devuelve un elemento *Promise*. Cuando la función *async* devuelve un valor, *Promise* se resolverá con el valor devuelto. Si la función *async* genera una excepción o algún valor, *Promise* se rechazará con el valor generado.

__Await:__ la expresión *await* provoca que la ejecución de una función *async* sea pausada hasta que una *Promise* sea terminada o rechazada, y regresa a la ejecución de la función *async* después del término. Al regreso de la ejecución, el valor de la expresión *await* es la regresada por una *Promise* terminada.

> __Consejo:__ async / await
Cuando utilizas *async* y *await* tienes un código mucho más limpio y sobre todo un mejor control de las excepciones. De ser posible, siempre utiliza *async* y *await*.

### Ejemplo practico async / await
```javascript
// al usar *async* en las funciones automáticamente devuelve una promesa
async function getBookById(id) {
    const book = booksDb.find(book => book.id === id);
    if (!book) {
      const error = new Error();
      error.message = 'Book not found!';
      throw error;
    }

    return book;
}

async function getAuthorById(id) {
    const author = authorsDb.find(author => author.id === id);
    if (!author) {
      const error = new Error();
      error.message = 'Author not found!';
      throw error;
    }

    return author;
}

// await va permitir que se resuelva cada promesa
async function main() {
  try {
    const book = await getBookById(1);
    const author = await getAuthorById(book.authorId);
    console.log(`This books ${book.title} was written by ${author.name}`);
  } catch (exception) {
    console.log(exception.message);
  } 
}

// ejecutamos el llamado a las funciones
main();
```
Generamos el mismo resultado que con los *callbacks* y lo hicimos con mucho menos líneas de código, además es mucho más claro y tenemos más control de los errores. 

Esto ha sido todo acerca de los *async / await* espero que te haya servido si quieres aprender más puedes ver vídeos de mi canal de [YouTube](https://youtube.com/runcoding) 