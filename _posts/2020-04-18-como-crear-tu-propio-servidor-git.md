---
layout: blog
permalink: /:title
title: Cómo crear tu propio servidor Git
tags:
  - git
date: 2020-03-28T18:18:48.857Z
thumbnail: /assets/images/uploads/git-server.jpg
toc: true
---
Usar un control de versiones es muy importante en el mundo del desarrollo, independientemente de si tu empresa es una consultoria de software o si solo tiene un departamento de desarrollo interno es crucial tenerlo. Una de las problematicas a las que me enfrente fué implementar un servidor propio que permitiera tener el control de accesos y permisos de forma interna en la empresa ya que hacerse de un servicio tipo GitHub o GitLab no está dentro de sus políticas por x razón de tener control de todo, me parece algo exagerado pero en lo personal me sirvio para profundizar más en como funciona en core de git en un entorno productivo. Ya no me enrrollo más y aqí te comparto los pasos a seguir para crear tu propio servidor git.

## Configuración e instalación de git
Antes de comenzar quisiera aclarar que la instalación se hizo en un servidor virtualizado con CentOS 8, dicho esto lo primero que vamos hacer es actualizar el sistema e instalar algunas librerías estándar.

```shell
yum update -y && yum upgrade -y
yum -y install nano
```
Instalar Git y habilitar Git Shell
```shell
yum install -y git
echo "/bin/git-shell" >> /etc/shells
```
>Para controlar los accesos y los permisos utilize la herramienta Gitolite que si quieres saber más al final tienes los enlaces a la documentación oficial.

A continuación se muestra un esquema de configuración de Gitolite con Git en el Servidor.

![Gitolite admin](https://gitolite.com/gitolite/ba01.png)

## Crear un usuario para Gitolite
Vamos a crear el usuario que nos va servir para clonar los repositorios a las distintas máquinas de nuestros usuarios finales.
```shell
adduser git
passwd git
```
## Crear llave publica SSH y copiarla al usuario git
Vamos a generar las llaves ssh para realizar la autenticación por clave pública y no por password
```shell
ssh-keygen
cp .ssh/id_rsa.pub sk.pub
```
Ahora vamos a copiarla al directorio de usuario git.
```shell
cp sk.pub /home/git
```
Puedes verificar que se haya copiado correctamente.
```shell
ls /home/git/
```
Corre el siguiente comando para actualizar el Bash.
```shell
source .bash_profile
```
Perfecto hasta aquí ya tendriamos listo el servidor git ahora hace falta la instalación de la configuración de la herramienta Gitolite.

## Instalar Gitolite
Iniciamos sesión con usuario git.
```shell
su - git
```
Creeamos un directorio bin.
```shell
mkdir ~/bin
```
Ahora, clonemos la última versión de gitolite.
```shell
git clone git://github.com/sitaramc/gitolite
```
Crea el símbolo de gitolite al directorio bin.
```shell
gitolite/install -ln ~/bin
```
Finalmente, corre el siguiente comando para instalar Gitolite con la llave SSH publica.
```shell
gitolite setup -pk sk.pub
```
### Probar Gitolite
Ahora, vamos a verificar que Gitolite está trabajando de forma correcta, cambiémonos a la cuenta con la que creamos la clave ssh.
```shell
git clone git@192.168.1.150:gitolite-admin
```
Verifica el contenido del repositorio gitolite-admin.
```shell
ls gitolite-admin/
```Con esto hemos terminado de verificar que Gitolite funciona correctamente.

## Crear nuestro primer repositorio
Vamos a crear primero una carpeta con el nombre del repositorio y extensión .git dentro de directorio /home/git/repositories
```shell
mkdir /home/git/repositories/mi-repositorio.git
cd /home/git/repositories/mi-repositorio.git 
git init --bare --shared=group
```
Ahora cambiamos el propietario del repositorio para que sea el usuario git.
```shell
chown -R git /home/git/repositories/mi-repositorio.git
```
## Creación de llave ssh del lado del cliente.
Tenemos que crear la llave ssh publica que nos va permitir clonar los proyectos a los distintos usuarios, para ello ejecutamos el siguiente comando dentro de la máquina local donde va trabajar el usuario.
```shell
ssh-keygen -t rsa
```
Ahora obten las llaves públicas de cada usuario ya sea por correo electrónico, USB, cualquier método que desees. Copia el contenido de la llave pública id_rsa.pub a un nuevo fichero con el nombre del usuario y extensión .pub por ejemplo ismael.pub.
```shell
usersPubKey='contents_of_your_public_key_file'
```
Dentro del directorio donde clonamos el proyecto deber crear el archivo con la llave publica ssh del usuario que quieres añadir en este caso el ejemplo es ismael.pub
```shell
echo $usersPubKey > /home/intercomm/gitolite-admin/keydir/ismael.pub
```
Cambia el nombre de cada archivo recibido al nombre del usuario, agregue un ".pub" al final, cópielo en keydir/ en el repositorio de gitolite-admin que clonó. 
```shell
git add keydir
git commit
git push
```
También debemos de darle permisos al usuario creado modificando el archivo gitolite.conf que se encuentra en el directorio `/home/username/gitolite-admin/conf/gitolite.conf`

```yml
@admin = git ismael
@engineers = ricardo eibar liz ismael
@productmanagers = gilberto, rodrigo

repo gitolite-admin
    RW+ = @admin

repo testing
    RW+ = @all

repo links
    RW+ master = ismael
    RW+ develop@engineers
    R develop@productmanagers
```

Por último debes confirmar los cambios hechos al repositorio con el usuario que tenga privilegios, en nuestro caso ya sea con el usuario git o ismael. 
```shell
git add -A 
git commit -m “message to commit”
git push origin
```

### Verificar el acceso al repositorio creado
Una vez creado el repositorio y agregado los permisos a la configuración de Gitolite vamos a clonar el proyecto en nuestra máquina.

git clone git@myserver.com:links 

Si todo está correcto se creará la carpeta con los archivos en el directorio donde le indicaste.

## Agregar ramas al repositorio
Cuando creamos el proyecto también es necesario añadir las ramas(branchs) que necesitemos para para organizar nuestro flujo de trabajo en nuestro caso solo crearemos dos ramas la rama develop y testing.
```shell
git branch desarrollo
git checkout desarrollo
git branch --set-upstream-to=origin/master develop 
git push origin desarrollo
```
```shell
git branch pruebas
git checkout pruebas
git branch --set-upstream-to=origin/desarrollo testing
git push origin pruebas
```

## WorkFlow
Hemos terminado de configurarlo todo pero ahora te toca decidir con tu equipo que forma de trabajo va a usar, aquí te dejo una propuesta que puedes usar, es una metodología llamada Workflow.

### Propuesta de flujo de trabajo con Git
![Workflow](https://nvie.com/img/git-model@2x.png)

Llegamos al final de este post, sin duda ha sido bastante largo este tutorial y aún nos queda mucho por aprender. Te quiero invitar a [mi canal de YouTube](https://youtube.com/runcoding) donde comparto videotutoriales del grandioso mundo de la programación.

## Referencias
[https://gitolite.com/gitolite/install.html](https://gitolite.com/gitolite/install.html)
[https://git-scm.com/book/en/v1/Git-on-the-Server-Gitolite](https://git-scm.com/book/en/v1/Git-on-the-Server-Gitolite)
[https://nvie.com/posts/a-successful-git-branching-model/](https://nvie.com/posts/a-successful-git-branching-model/)