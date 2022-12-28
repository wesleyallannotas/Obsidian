---
title: Elementos Genéricos
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [html]
description: Elementos genéricos
---
# Introdução
São elementos sem alguma semântica, normalmente utilizado para aplicação de estilos CSS ou quando não encontrado uma forma de adicionar semântica, assim sendo interessante usar atributos globais como `id` e `class` para trazer maior significado, possuímos duas tags genéricas sendo uma delas para conteúdo em bloco e outra em linha
- `div` - Em bloco ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/div))
- `span` - Em linha ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/span))

```html
<div>
	<h1>Lista de produtos</h1>
	<h2>Valor: <span>R$ 20,00</span></h2>
</div>
```

`<div>` é muito usado para criar o carrinho de compras por exemplo, pois, `<section>` não tem esse semântica global, do site todo e sim para a página atual, por isso muitos profissionais preferem utilizar o elemento genérico.