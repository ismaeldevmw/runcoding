---
layout: blog
permalink: '/:title'
title: '#1 Creando un BLOG | Instalación de Laravel 5.5 y migraciones.'
tags: laravel
thumbnail: /assets/images/uploads/miniatura-laravel-1.png
toc: true
---
Bienvenido a este nuevo post en en que vamos a comenzar el proyecto de crear un blog en Laravel 5.5, Laravel utiliza Composer para manejar sus dependencias, así que antes de comenzar debes asegurarte de tenerlo instalado en tu máquina.

## Vía Laravel Installer

Primero, descarga el instalador de Laravel usando Composer:

```php
composer global require "laravel/installer"
```

Asegurate de agregar el directorio vendor bin en tu `$PATH` así podrá ser ejecutado localmente en tu sistema. Este directorio existe en diferentes localizaciones basadas en tu sistema operativo; sin embarg, algunas localizaciones comunes incluyen: 

* MacOS:`$HOME/.composer/vendor/bin`
* GNU / Linux Distributions:`$HOME/.config/composer/vendor/bin`

Una vez instalado, el comando `laravel new` creara una instalación limpia de Laravel en el directorio que tu especifiques, por ejemplo `laravel new blog` creara  un directorio llamado blog que contiene una instalación limpia de Laravel con todas las dependencias de Laravel ahora instaladas:

```php
laravel new blog
```

## Vía Composer Create-Project

Alternativamente, puedes también instalar Laravel por medio del comando Composer `create-project` en tu terminal:

```php
composer create-project --prefer-dist laravel/laravel blog
```

## Creando migraciones

Una vez creado nuestro proyecto Laravel vamos a crear nuestras entidades necesarias junto a las migraciones, vamos al terminal y nos movemos al directorio de nuestro proyecto `cd blog`, vamos a crear el modelo junto a la migración con el flag `-m`, creamos el modelo `Category` observa que lo escribo en Inglés y singular esto es un estándar; si trabajamos de esta manera en el futuro cualquiera puede leer tu código porque nos estamos basando en estándares internacionales es decir el modelo está en inglés y en singular y la tabla en plural y también está en inglés, vamos a crear el modelo:

```php
php artisan make:model Category -m
```

Y se crea de forma satisfactoria, el siguiente paso es crear el modelo que vamos a utilizar para los posts:

```php
php artisan make:model Post -m
```

Asimismo creo el modelo de los Tags:

```php
php artisan make:model Tag -m
```

Todo bien hasta aquí, hace falta una migración para el tema de muchos a muchos de los posts y los tags, ya los crearemos pero primero te voy a enseñar que tenemos hasta ahora:

![undefined](/assets/images/uploads/modelos-app.JPG)

Observa que dentro del directorio `app` se crearon las entidades `Category`, `Post` y `Tag` con los comandos anteriores y la de `User` ya viene creada por defecto. Ahora observemos que dentro del directorio `database/migrations` se encuentra la migración para usuarios que ya viene creada por defecto, para resetear las contraseñas también ya viene creada. y debajo aparecen las migraciones que creamos:

![undefined](/assets/images/uploads/migrations-created.JPG)

## Relaciones muchos  a muchos

Nos hace falta una ultima migración para relacionar muchos a muchos los posts con los tags, en este caso el comando es diferente no vamos a crear un modelo vamos a crear directamente una migración, si algún comando se te olvida puedes usar el comando `php artisan` y tendrás todos los comandos, el que vamos a usar es `make:migration`:

```php
php artisan make:migration create_post_tag_table
```

Toma en cuenta lo siguiente, el nombre de la migración comienza con create y las tablas relacionadas van en singular ordenadas alfabéticamente y al final la palabra table, siempre que vas hacer una relación muchos a muchos tienes que seguir esté orden alfabético por ejemplo si vas a relacionar la tabla user y category tienes que colocar primero category.  

Con esto terminamos esta lección, espero que te haya gustado este comienzo, recuerda como siempre compartir este post, dejarme tus comentarios y sobre todas las cosas no olvides suscribirte al canal de [YouTube](https://www.youtube.com/Runcoding) estoy seguro que vas aprender mucho y en definitiva te va encantar, que sigas estando bien nos vemos en la siguiente lección.
