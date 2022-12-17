---
title: Manipulando fontes com CSS
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Como manipular as fontes com diversar propriedades no CSs 
---
# Introdução
Manipulação de fontes é muito importante para a construção de uma boa página web, existem diversas propriedades que podemos manipular através do CSS, também é possível a utilização de [[01 - Notes/Code/CSS/Introdução#Shorthand|shorthand]] na declaração da fonte. ([Doc](https://www.w3.org/TR/css-fonts-3/))

>[!warning] Atenção
>Nem todas as fontes aceitam todas as propriedades

# Tipo
Definimos o tipo da fonte através da propriedade `font-family`, listamos em ordem de prioridade, incluindo um *fallback* que será utilizado quando as fonte não der certo seguindo a lista de prioridade declarada anteriormente
```css
p {
	font-family: "Times New Roman", Times, serif;
}
```

# Peso
Através da propriedade `font-weight` definimos o peso da fonte, a grossura da letra.
```css
p {
	font-weight: bold;
}
```

# Estilo
Através da propriedade `font-style` definimos o estilo da fonte
```css
p {
	font-style: italic;
}
```

# Tamanho
Através da propriedade `font-size` podemos manipular o tamanho da fonte
```css
p {
	font-size: 50px;
}
```

# Importando
Podemos importar fontes através da Web, não sendo necessário o usuário possuir a fonte instalada em sua maquina,  sendo possível a importação através das [[At-Rules]] `@import` e `@font-face`, ou até mesmo utilizando o elemento HTML [[Cabeçalho#^8e21a4|<link>]]
```css
<head>
	<link rel="preconnect" href="https://fonts.googleapis.com">  
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>  
	<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@100&display=swap" rel="stylesheet">
</head>
```
Utilizando o elemento HTML e a forma mais conhecida entre todas.

# Variação
Através da da propriedade `font-variant` podemos traz variação na apresentação das fontes
```css
p {
	font-variant: small-caps;
}
```

# Alargamento e Encolhimento
Através da propriedade `font-stretch` podemos alterar a fonte a alargando e a encolhendo
```css
p {
	font-stretch: expaded;
}
```

# Espaço Entre Caracteres
Através da propriedade `letter-spacing` podemos alterar os espaços entre os caracteres
```css
p {
	letter-spacing: 0.7em;
}
```

# Espaço Entre Palavras
Através da propriedade `word-spacing` podemos alterar o espaço entre as palavras
```css
p {
	word-spacing: 1em;
}
```

# Espaço Entre Linhas
Através da propriedade `line-height` podemos alterar o espaço entra as linhas, pode ser com ou sem unidades de medidas
```css
p {
	line-height: 1.5;
}
```

# Transformando
Através da propriedade `text-transform` podemos transformar o nosso texto
```css
p {
	text-transform: uppercase;
}
```
Ignorando a forma como digitamos e transformando todo o texto para o valor especificado
- `uppercase` - Caixa alta
- `lowercase` - Caixa baixa
- `capitalize` - Letras iniciais maiúsculas
- `none` - Mantem a forma digitada

# Decoração
Através da propriedade `text-decoration` podemos atribuir uma aparência decorativa ao nosso texto, lembrando que `text-decoration` é um [[01 - Notes/Code/CSS/Introdução#Shorthand|shorthand]] para as seguintes propriedades `text-decoration-line`, `text-decoration-color`, `text-decoration-style` e `text-decoration-thickness` ([Doc](https://developer.mozilla.org/en-US/docs/Web/CSS/text-decoration))
```css
p {
	text-decoration: underline wave tomato;
}
```

# Alinhamento
Através da propriedade `text-align` podem alterar o alinhamento do nosso texto
```css
p {
	text-align: center;
}
```

# Sombras
Através da propriedade `text-shadow` podemos adicionar uma sombra ao nosso texto
```css
p {
	text-shadow: 1px 1px 1px red; /* offset-x ofsse-y blur-radius color */
}
```
 Podemos declarar mais de um
```css
p {
	text-shadow: 1px 1px 1px red,
	             2px 2px 1px green;
}
```