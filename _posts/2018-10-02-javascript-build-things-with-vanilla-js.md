---
layout: post
title: JavaScript - Build things with vanilla JS
tags: javascript
thumbnail: /assets/images/uploads/js.png
permalink: '/:year/:month/:day/:title'
---
## Toogle function

Función que oculta y muestra un elemento.

```javascript
function toogle(identificador) {if(document.getElementById(identificador).style.display == 'none') {  document.getElementById(identificador).style.display = 'block';  }else {    document.getElementById(identificador).style.display = 'none';  }}
```
{% gist fa55f6958a779e690d852b99c46cd3d0 %}
