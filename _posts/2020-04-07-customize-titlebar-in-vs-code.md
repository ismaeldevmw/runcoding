---
layout: blog
permalink: '/:title'
title: Customize titleBar in VS Code
tags:
  - vscode
date: 2020-04-07T11:13:16.177Z
thumbnail: /assets/images/uploads/titlebar-customized.png
toc: 'false'
---
To open your user and workspace settings, use the following VS Code menu command:

* On Windows/Linux - File > Preferences > Settings
* On macOS - Code > Preferences > Settings

You can also open the Settings editor from the Command Palette (Ctrl+Shift+P) with Preferences: Open Settings or use the keyboard shortcut (Ctrl+,).

![](/assets/images/uploads/settings.png)

Go to "Appearance" and clic on Edit in settings.json". Add the next settings.

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
Thats all, you have customized your editor on VS Code.