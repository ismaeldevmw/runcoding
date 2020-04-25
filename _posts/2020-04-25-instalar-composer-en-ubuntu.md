---
layout: blog
permalink: /:title
title: "Instalar Composer en Ubuntu "
tags:
  - php
date: 2020-04-24T00:58:08.441Z
thumbnail: /assets/images/uploads/instalar-composer.png
toc: true
---
1. Nos logueamos como root.
```bash
sudo su
```
2. Nos movemos a “/usr/local/bin” para que composer sea ejecutable desde cualquier lugar.
```bash
cd /usr/local/bin
```
3. Descargamos e instalamos composer.
```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'e0012edf3e80b6978849f5eff0d4b4e4c79ff1609dd1e613307e16318854d24ae64f26d17af3ef0bf7cfb710ca74755a') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```
4. Cambiamos el nombre de composer.phar a composer (opcional).
```bash
mv composer.phar composer
```

Listo ya puedes ejecutar el comando ***composer*** desde tu terminal.
