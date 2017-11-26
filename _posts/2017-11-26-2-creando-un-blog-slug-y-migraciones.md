---
layout: post
title: '#2 Creando un BLOG | SLUG y Migraciones'
tags: Laravel
thumbnail: /assets/images/uploads/laravel-blog.png
permalink: '/:year/:month/:day/:title'
---
```
Vamos a continuar, en esté punto necesitamos configurar la base de datos lo hacemos en el archivo .env, aquí tenemos un parametro para configurar el puerto en este caso lo haremos con Homestead, para conectar tu base de datos MySQL o PostgreSQL de la base de datos cliente de tu máquina, debes conectar a 127.0.0,1 y al puerto 33060(MySQL) o 54320(PostgreSQL). El username y password para ambas bases de datos es homestead/secret. Por lo tanto debes tener la siguiente configuración con los siguientes datos:
```

```php
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=33060
DB_DATABASE=blog-laravel
DB_USERNAME=homestead
DB_PASSWORD=secret
```

Además dentro de tu archivo `homestead.yml` debes agregar el nombre de tu base de datos en la sección de database, por supuesto esto si haces uso de Homestead.

```php
databases:
    - homestead
    - blog-laravel
```

Antes de continuar con el temas de la configuración y las migraciones, vamos a ver un error. Por ejemplo si escribo `php artisan migrate` nos lanza un error que igualmente aparece en Laravel 5.4, sin embargo la solución e este caso es diferente aunque también funcionaria, basicamente dice que la columna unica no tiene una longitud establecida asi que simplemente lo que debemos hacer es darle una longitud fija :

Entonces vamos al editor de código, buscamos las migraciones dentro del directorio `database`/`migrations`, por su puesto las que creamos anteriormente no tienen este problema pero si que la de `create_users`. Tenemos que el campo email aparece como `unique` y no tiene una longitud, así que lo tenemos que cambiar:

Una vez hecho esto podemos ejecutar sin problemas la migración con el siguiente comando de artisan:

```
php artisan migrate
```

Ahora vamos a modificar el archivo de las migraciones de Category en el cual vamos a agregar los campos que necesites.

```php
public function up()
{
    Schema::create('categories', function (Blueprint $table) {
        $table->increments('id');
        $table->string('name', 64);
        $table->string('slug', 128);
        $table->mediumText('body')->nullable();
        $table->timestamps();
    });
}
```

Enseguida refrescamos la migración con el siguiente comando de artisan:

```
php artisan migrate:refresh
```

En el siguiente post continuaremos con las demás migraciones así que nos vemos en el próximo post hasta pronto.
