---
title: Posicionamento através de propriedade CSS
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Como alterar o posicionamento natural através da proprieade `position` 
---
# Introdução
Através da propriedade CSS `position` podemos controlar onde nosso ==elemento HTML ira se posicionar==, alterando o fluxo normal dos elementos que por padrão de encontra posicionando elementos um abaixo do outro.([Doc](https://developer.mozilla.org/pt-BR/docs/Web/CSS/position))

# Valores
Os valores aceitos pela propriedade `position` são
- `static` - Valor padrão da propriedade, significa que seguira o fluxo padrão
- `relative` - Se posiciona relativo a si mesmo em sua posição original, porem se mantem ocupando o seu posicionamento original
- `absolute` - Se posiciona relativo ao elemento ancestral que possui um posicionamento, ou seja, um valor diferente de `static` para propriedade `position`, deixa de ocupar sua posição original, é como se fosse para uma camada a cima
- `fixed` - Se posiciona relativo a página, deixa de ocupar sua posição original, se torna fixo a *viewport*, ou seja, mesmo rolando o scroll ele se mantem visível. 

# Propriedades
Quando utilizamos um ==valor diferente de `static`== para nossa propriedade `position` se ==abre no cinco novas propriedades== que podemos manipular sendo elas `top`, `left`, `right`, `bottom` e `z-index`.
- `top`, `left`, `right` e `bottom` - Quando utilizamos estas propriedades estamos informando quando de distancia ele deve adicionar desse lado, por exemplo `top: 50px` vai colar no top e depois se distancia `50px`
- `z-index` - Se refere ao eixo Z, assim podemos controlar e posicionar um elementos a frente do outro, ==criando camadas==, quando maior o valor mais acima

# Exemplo
```css
.box1 {
	position: absolute;
	top: 5px;
	left: 5px;
	z-index: 3;
}
.box2 {
	position: absolute;
	top: 10px;
	left: 10px;
	z-index: 2;
}
.box1 {
	position: absolute;
	top: 15px;
	left: 15px;
	z-index: 1;
}
```