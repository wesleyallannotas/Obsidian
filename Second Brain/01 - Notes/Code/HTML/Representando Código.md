---
title: Representando código
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [html] 
description: Como criar bloco de códigos no HTML
---
# Introdução
Como representar código de linguagens de programação de forma nativa no HTML, utilizaremos as seguintes tags:
- `code` - Para código em linha, pequeno trecho ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/code))
- `pre` - Para código em bloco, trechos mais longos ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/pre))

# Exemplo
```html
<!-- Linha -->
Exemplo de pedaço de códigoem linha <code>apt update</code>
    
<!-- Bloco -->
<pre>
	while (count &lt; total) {
	  count ++
	  }
</pre>
```