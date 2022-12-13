---
title: Citação
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [html]
description: Como cirar citação no HTML 
---
# Tipos
Utilizado para citações, ou seja, trazer algo escrito por outra pessoa, existem 3 formas de criar uma citação no documento HTML
- `blockquote` - Citação grande envolvida em aspas, elementos em bloco
	- Atributo `cite` utilizando para referenciar de onde veio
- `cite` - Citação que muda o texto para itálico, elemento em linha
- `q` - Citação que envolve o texto em aspas, elemento em linhas

# Exemplo
```html
  <body>
    <blockquote cite="http://imcDark.netlify.app">Exemplo blockquote</blockquote>
    <cite>Exemplo Cite</cite>
    <q>Exemplo q</q>
  </body>
```