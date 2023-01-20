---
title: Animation
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Conheça a ferramenta CSS animation
---
# Introdução
Através da ferramenta `animation` podemos criar animações utilizando CSS.

# Criando a Animação
Para trabalhar com animações utilizamos a [[At-Rules]] `keyframes`, informamos um nome para nossa animação e dentro criarmos nosso animação, seja por palavras chaves (`from`, `to`), ou porcentagem.

```css
@keyframes arrow {
	from {
		top: 0;
	}
	to {
		top: 30px;
	}
}

@keyframes arrow {
	o% {
		top: 0;
	}
	50% {
		top: 30px;
	}
	
	100% {
		top: 35px;
	}
}
```

# Name
Através da propriedade `animation-name` atribuímos como valor o nome da animação que queremos utilizar, propriedade **obrigatória** para o funcionamento da animação.

```css
animation-name: arrow;
```

# Duration
Através da propriedade `animation-duration` atribuímos como [[Valores e Unidades de Medidas#Unidades Comuns|valor do tipo]] `<time>` a duração da animação, propriedade **obrigatória** para o funcionamento da animação.

```css
animation-duration: 1s;
```

>[!attention] Atenção
>Quando definimos um valor padrão para uma propriedade, e utilizamos outras valores para a mesma propriedade durante a animação, quando a duração acabar, voltara ao valor padrão.,
>```css
>@keyframes ColorChange {
>	from {color: red;}
>	to {color: white;}
>}
>.text {
>	color: green;
>	animation-name: ColorChange;
>	animation-duration: 1s;
>}
>```
>Quando acabar o `1s` da animação entre `red` e `white` ele voltara a `green`

# Delay
Basicamente definimos um Timeout para começar a animação, ou seja, se definirmos como `5s` demorara os cinco segundo para iniciar a animação.

```css
animation-delay: 1s;
```

# Iteration Count
Através da propriedade `animation-iteration-count` podemos definir quantas iterações iram ocorrer, ou seja, quantas vezes a animação ira se repetir, podemos niver um numero, `infinite` caso for se repetir eternamente, entre outras.

```css
animation-iteration-count: infinite;
```

# Direction
Através da propriedade `animation-direction` podemos controlar a direção da nossa animação definida na declaração da animação seja por meio de palavras-chave (`to`, `from`) como porcentagem.
- `reverse` - Inverte a ordem normal
- `alternate` - Alternando entre as alterações, só faz sentido se houver uma [[#Iteration Count|iteração]].

```css
animation-direction: alternate;
```

# Timing Function
Podemos controlar o comportamento da nossa animação dentro do tempo previsto em `duration`

```css
animation-timing-function: ease;
animation-timing-function: cubic-bezier(0.29, 1.01, 1, -0.68);
```

-   `ease` - Início lento, rápido e final lento (este é o padrão)
-   `linear` - Mesma velocidade do início ao fim
-   `easy-in` - Início lento
-   `easy-out` - Final lento
-   `easy-in-out` - Início e fim lentos
-   `cubic-bezier(n,n,n,n)` - Permite definir seus próprios valores em uma função cubic-bezier (Como um elástico)

# Fill Mode
Através da propriedade `animation-fill-mode` podemos definir o uso das propriedades da animação, como padrão do nosso elemento.
- `forward` - Final incorporado no elemento
- `backfwards` - Inicial incorporado, afeta o [[#Delay]], ou seja, invés de enquanto estiver no _delay_ usar as propriedades do elemento, usa as inicias da animação.
- `both` - Durante  _delay_ pega inicio da animação, após o final, pega do final da animação.

```css
animation-fill-mode: backwards;
```