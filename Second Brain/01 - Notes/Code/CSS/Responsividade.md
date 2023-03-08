---
title: Responsividade
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Criando responsividade.
---
# 🚀 Introdução
Responsavidade é um assunto muito importante que  nada mais é do que garantir o pleno funcionamento da nossa página ou aplicação web, perfeitamente em qualquer dispositivo que seja acessado, seja ele, _desktop_, _mobile_, _tablet_, entre outros.
Podemos conseguir desenvolver de forma responsiva utilizando:
- [[Valores e Unidades de Medidas#Distancias Relativas|Unidades de medida relativa]] e ou [[Valores e Unidades de Medidas#Porcentagem|porcentagem]]
- Propriedades CSS que facilitando o mesmo, como `max-width`, `min-width`, [[Flexbox]], [[Grid]], entre outros
	- Normal definir `width: 100%` e `mix-width: 900px`, por exemplo.
- Definir regras, _breakpoints_ onde a partir de tal condição mudaremos tal CSS, sendo o mesmo feito por meio de _media queries_.

>[!attention] Metadado Importante
>Sabemos que através do elemento [[Cabeçalho#Meta|Meta]] podemos definir metadados que possui amplo uso, desde de definir informações sobre a página ate como ela deve funcionar, um metadado muito  importante para responsividade é
>```css
><meta name="viewport" content="width=device-width, initial-scale=1.0" />
>```
>Através do mesmo definimos o funcionamento de _viewport_.

# 📜 Media Queries
_Media_ é um [[At-Rules]] que possibilita definir propriedades CSS através de condições.

>[!note] Metodologia
>Quando utilizamos a metodologia _Desktop First_ utilizaremos `max-width`, quando utilizarmos _Mobile First_ utilizaremos `min-width`.

```css
.container {
	justify-content: space-between;
}

@media (max-wisth: 768px) {
	.container {
		justify-content: center;
	}
}
```

Ou seja, até o _viewport_ possuir o _width_, ou seja, largura de `768px` o `justify-content` da classe `container` var possuir o valor `center`, acima disso será `space-between`. 

# Imagens
Uma boa ideia para responsividade e de quebrar desempenho, é possuir diferentes tamanhos da mesma imagem, colocar dentro de um elemento `picture` e através do atributo `media` definir as regras.

```html
<picture class="image" alt="images">
	<source media="(min-width: 1280px)" srcset="imgFull.png" />
	<source media="(min-width: 760px)" srcset="imgMedia.png" />
	<source media="(min-width: 500px)" srcset="imgSmall.png" />
</picture>
```

# Menu Hamburguer
Muito utilizado a ideia de possuir um botão que parece um hamburguer para acionar a exibição do  menu em toda a tela, muito utilizado no _mobile_, uma ideia muito utilizada é criar a estrutura e deixar vazia, assim não possuindo impacto visual, e só preencher quando atingir o _viewport_ desejado.

```html
<div class="menu-toggle">
	<div class="one"></div>
	<div class="two"></div>
	<div class="three"></div>
</div>
```

```css
@media (max-width: 560px) {
	.one,
	.two,
	.three {
		background-color: #fff;
		height: 5px;
		width: 100%;
		margin: 6px auto;
	}
	.menu-toggle {
		width: 40px;
		height: 30px;
		margin-right: 20px;
	}
}
```