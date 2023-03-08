---
title: At-Rules do CSS
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: As at-rules e seus funcionamentos
---
# Introdução
Relacionado a comportamento do CSS iniciando com um símbolo de `@` seguindo do identificar e valor exatamente o nome traduzido At (`@`) Rules (Regras) ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/CSS/At-rule)), exemplos comuns de at-rules:
- `@import` - Incluir um CSS externo
- `@media` - Regras condicionais para dispositivos
- `@font-face` - Fontes Externas
- `@keyframes` - Animações
```css
@import url("http://local.com/style.css")

@media (min-width: 500px) {
	h1 {
		background-color: tomato;
	}
}

@font-face {
	/* rules (regras) aqui */
}

/* From to */
@keyframes widthChange {
	from {
		width: 200px;
	}
	to {
		width: 300px;
	}
}
/* Porcentagem da execução */
@keyframes identifier {
  0% { top: 0; left: 0; }
  30% { top: 50px; }
  68%, 72% { left: 50px; }
  100% { top: 100px; left: 100%; }
}
/* Misturado */
@keyframes important1 {
  from { margin-top: 50px; }
  50%  { margin-top: 150px !important; } /* ignored */
  to   { margin-top: 100px; }
}
```


# Media Queries (Melhorar)
_Media_ é um [[At-Rules]] que possibilita definir propriedades CSS através de condições, utilizando operadores  como `and`, `or`, aplicar regras para tela (_screen_) para impressão (_print_)
Também é possui definir a média no _link_ do CSS

```html
<link rel"stylesheet" href="respobnsive.css" media="screen and (max-width: 768px)" />
<link rel="stylesheet" href="print.css" media="print" />
```