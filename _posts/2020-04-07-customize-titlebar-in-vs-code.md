---
layout: blog
permalink: /:title
title: Personalizar la Barra de Título de Visual Studio Code
tags:
  - vscode
date: 2020-04-07T11:13:16.177Z
thumbnail: /assets/images/uploads/titlebar-customized.png
toc: false
---
Para abrir su configuración de usuario y espacio de trabajo, use el siguiente comando del menú VS Code:

* En Windows/Linux - File > Preferences > Settings
* En macOS - Code > Preferences > Settings

También puede abrir el editor de Configuración desde la Paleta de comandos (Ctrl + Shift + P) con Preferencias: Abra Configuración o use el atajo de teclado (Ctrl +,).

![](/assets/images/uploads/settings.png)

Vaya a "Apariencia" y haga clic en Editar en settings.json ". Agregue la siguiente configuración.

```javascript
{
    "workbench.colorCustomizations": {
        "titleBar.activeBackground": "#ff2c70",
        "titleBar.inactiveBackground": "#ff2c70cc",
        "titleBar.activeForeground": "#fff",
        "titleBar.inactiveForeground": "#fff000cc"
    } 
}
```
Eso es todo, ha personalizado su editor en VS Code.