---
layout: blog
permalink: /:title
title: Homestead como entorno de desarrollo profesional.
tags:
  - laravel
date: 2019-09-23T21:51:19.684Z
thumbnail: /assets/images/uploads/homestead.jpg
toc: true
---
{% youtube "https://youtube.com/watch?v=lfAtoykp88E" %}

## Introducción
¿Qué es Homestead? Homestead nos provee de un entorno de desarrollo local mediante maquinas virtuales, por medio de Vagrant. 

Cuando trabajas con múltiples proyectos, el hacerlo con tu máquina ya no es tan fácil ya que muchas veces necesitas diferentes versiones de PHP o tu equipo puede tener diferentes sistemas operativos, diferentes versiones de PHP o diferentes versiones de la base de datos lo cual puede ser bastante problemático. Para solucionar esto usamos la virtualización que nos permite crear entornos virtuales dentro de nuestro equipo que nos ayudan a tener un entorno de desarrollo ideal.

Existen dos vertientes principales: **Vagrant** y **Docker**. **Vagrant** genera máquinas virtuales completas en las cuales podemos instalar PHP, bases de datos, Apache, entre otras. La otra vertiente es **Docker** con la cual se generan pequeños contenedores dentro de una máquina virtual los cuales contienen la instalación de PHP o la base de datos, logrando que trabajen en conjunto.

Para comenzar a usar Homestead vamos a seguir los siguientes pasos y configuraciones:

* Descargaremos Vagrant y lo instalaremos <https://www.vagrantup.com/> así como el entorno de virtualización VirtualBox <https://www.virtualbox.org>
* Utilizaremos la imagen de Laravel Homestead siguiendo los pasos que aquí se describen: <https://laravel.com/docs/5.7/homestead>. Las imágenes de Vagrant las llamaremos box o cajas, Homestead es una de ellas.

## Instalando Homestead Vagrant Box

Una vez que tengamos instalado VirtualBox / VMware y Vagrant deberas agregar la box `laravel/homestead` usando el siguiente comando en tu terminal. Esto tomara unos minutos en descargar dependiendo de tu conexión a internet

```php
vagrant box add laravel/homestead
```

Ejecutamos el comando `vagrant` en la terminal y si todo se instalo correctamente nos saldrá la ayuda del comando, también podemos ver la versión que tenemos instalada con el comando `vagrant -v`.

## Instalando Homestead

Ya que haya termino la descarga de la box puedes instalar Homestead clonando el repositorio. Considera clonar el repositorio en la carpeta Homestead dentro de tu directorio "home", así Homestead podra servir como host de todos tus proyectos php.

```
git clone https://github.com/laravel/homestead.git ~/Homestead
```

Una vez clonado el proyecto nos movemos a ese directorio.

```
cd ~/Homestead
```

Ejecutamos el comando que inicializara Homestead el cual crea un nuevo archivo de configuración Homestead.yaml 

```php
// Mac / Linux...
bash init.sh

// Windows...
init.bat
```

* Al editar el archivo “Homestead.yaml”, tenemos información de la ip que no es el localhost por ser máquina virtual. Aquí igualmente ligamos nuestra carpeta de proyecto a la carpeta de la máquina virtual; también podemos añadir bases de datos y diferentes proyectos dentro de la misma máquina o box.

## Configurando carpetas compartidas

Aquí se mapean las carpetas que deseas conpartir con tu entorno de Homestead. Estos se sincronizan entre tu máquina y el entorno Homestead y puedes configurar tantas carpetas creas necesarias:

```php
folders:
    - map: ~/code
      to: /home/vagrant/code
```

Si tu creas pocos sitios, el mapeo generico resulta suficiente. sin embargo si el número de sitio continua creciendo, puedes comenzar a experimentar problemas de rendimiento. Este problema llega a suceder por la gran cantidad de archivos. Si estas experimentando este error, intenta mapear cada proyecto en su propia carpeta Vagrant:

```php
folders:
    - map: ~/code/project1
      to: /home/vagrant/code/project1

    - map: ~/code/project2
      to: /home/vagrant/code/project2
```

## Configurando los Sitios

Los sitios nos permiten mapear facilmente un dominio hacia una carpeta en tu entorno Homestead. De nuevo, puedes agregar tantos sitios a tu entorno como sea necesario para cada proyecto php:

```php
sites:
    - map: homestead.test
      to: /home/vagrant/code/Laravel/public
```

## El archivo Hosts

Tu debes agregar los dominios de tus sitios del servidor en tu máquina. El archivo de hosts redireccionara las peticiones de tus sitios de Homestead dentro de tu máquina. En Mac y Linux el archivo se encuentra en `/etc/hosts`. En Windows esta ubicado en `C:\Windows\System32\drivers\etc\hosts`. Las lineas que agregas a este archivo deberán verse como la siguiente:

```
192.168.10.10 homestead.test
```

* Cuando usas el comando “vagrant up” se creará una máquina virtual vagrant si no existe; si existe se reiniciará la máquina existente. Se ejecutará también el aprovisionamiento que es configurar o instalar cualquier cosa que se necesite.

## Ejecutando Vagrant Box

Una vez que hayas editado  Homestead.yaml, ejecuta el comando `vagrant up` de tu directorio Homested. Vagrant prendera la máquina y automaticamente configurara tus carpetas compartidas y sitios.

Hemos terminado de configurar Homestead  ahora si podremos comenzar a desarrollar nuestros proyectos si preocuparnos de las problemáticas mencionadas al inicio del post, espero que este post te ayude
