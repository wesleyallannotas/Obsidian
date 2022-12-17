---
title: Imagens com HTML
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [html]
description: Como adicionar imagens através do HTML 
---
# Introdução
Podemos adicionar imagem através do **elemento vazio**  `<img />` que ao contrario de imagens adicionadas via CSS, aqui possuem semântica, como obrigatório temos ao atributo `src` responsável por linkar o conteúdo ao elemento ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/img)), exemplo de declaração simples
```html
<img src="exemplo.jpg" alt="Time da copa" />
```
O atributo `alt` é opcional, sua função é trazer  **acessibilidade** e um **texto alternativo** caso a imagem não consiga ser carregada para o nosso documento HTML

# Atributos
- `src` - Linka conteúdo, Link da web ou path local
- `alt` - Acessibilidade e texto alternativo, frase simples que explica o conteúdo da imagem
- `title` - Texto que aparece quando o mouse repousa sobre a imagem, é um titulo
- `width` - Largura
- `height` - Altura

# Utilizando Estilo
Em alguns casos e utilizado uma elemento genérico para adicionar uma imagem através do atributo `style` utilizando a propriedade CSS `background-image` como no exemplo abaixo:
```html
<div style="backgroun-image: url(imagem.png)" />
```

>[!warning] Atenção
>Adicionar imagem dessa forma funciona, porem não traz semântica alguma ao documento HTML, pós CSS tem seu uso pensando para o visual, design e não para o conteúdo semântico, dessa forma e interpretado como uma imagem para estilização e não como importante para o contexto

# Títulos Visíveis
Uma ideia para adicionar *caption* para imagens era envolver em elementos genéricos com uma classe especifica e adicionar o elemento vazio `<img />` e um `<p>` por exemplo, dentro desse elemento genérico, porem podemos deduzir que esse método não traz semântica alguma a imagem, para resolver essa lacuna foram criados os elementos `<figure>` e `<figcaption>`
```html
<figure>
	<img
		src="exemplo.png"
		alt="Imagem de exemplo"
		title="Imaggem de exemplo"
		width="600px"
	>
	<figcaption>Imagem de exemplo</figcaption>
</figure>
```
Dessa forma juntamos de forma semântica um titulo para imagem e o titulo utilizando o elemento pai `<figura>` e o elemento responsável pelo titulo o `<figcaption>`

# SVG
A utilização de SVG já é amplamente adota e podemos criar dentro do nosso HTML utilizando o elemento `<svg>`, em sua base usa a ideia de imagem **vetorizada** ao invés de imagens **rasterizada**.

## Rasterizadas
Em sua base é construída por pixels possuindo efeitos colaterais quando redimensionada.

## Vetorizada
Imagem vetorizada adotada pelo SVG é construída via código assim não importante as dimensões que desejarmos ela será construída para aquelas dimensões sem impactos de qualidade, por ser escrita via texto possui um **melhor SEO**, e podemos editada em tempo real através de atributos CSS.

## Exemplo
```html
<svg width="100" height="100">
	<circle cx="50" cy="50" r="40" stroke="green" strike-width="4" fill="yellow" />
</svg>
```