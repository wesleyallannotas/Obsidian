---
title: At-Rules do CSS
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: note
description: As at-rules e seus funcionamentos
---
# Introdução
Relacionado a comportamento do CSS iniciando com um símbolo de `@` seguindo do identificar e valor exatamente o nome traduzido At (`@`) Rules (Regras), exemplos comuns de at-rules:
- `@important` - Incluir um CSS externo
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

