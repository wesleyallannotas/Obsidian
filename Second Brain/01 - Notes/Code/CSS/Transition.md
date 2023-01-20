---
title: Transition
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Como criar e manipular a proprieade transition
---
# Introdução
Através da propriedade `transition` eu consigo manipulara transição de valores de propriedades que são **codificáveis**, por exemplo:

```css
button {
  padding: 40px;
  background-color: #575457;
  color: white;
  filter: brightness(0.7);
  border-radius: 15px;
  transition-property: filter;
  transition-duration: 2s;
}

button:hover {
  filter: brightness(1);
  transition-property: filter;
  transition-duration: 2s;
}
```

Adicionamos as propriedades `transition` no elemento `<button>` para que a transição das propriedades ocorra para a [[Seletores, Combinadores, Pseudo-classes e  Pseudo-Elements#Pseudo-Classes|Pseudo-Classe]]  `:hover`. E adicionamos as propriedades na _Pseudo-Classe_ `:hover` para que ocorra a transição, contraria, ou seja, quando tirar o mouse de cima.

>[!tip] Shothand
>Assim como muitas propriedades que possuem "sub-proprieades", temos o [[Introdução ao CSS#Shorthand|Shorthand]] para encurtar nossa declaração.
>```css
>transition: width 2s ease-in-out 0s;
>```

# Property
Através da propriedade  `transition-property` podemos definir em qual propriedade nossa transição será criada.

```css
transition-property: width;
```

>[!tip] Todos
>Podemos realizar a transição de uma propriedade, ou de todas a propriedades através do valor `all` 
>```css
>button:hover {
>	  filter: brightness(1);
>	  width: 500px;
>	  transition-property: all;
>	  transition-duration: 2s;
>}
>```

# Duration
Através da propriedade `transitiion-duration` podemos definir o tempo de duração da nossa transição através de um [[Valores e Unidades de Medidas#Unidades Comuns|valor do tipo]] `<time>`.

```css
transition-duration: 2s;
```

# Timing Function
Podemos controlar o comportamento da nossa transição dentro do tempo previsto em `duration`

```css
transition-timing-function: ease;
transition-timing-function: cubic-bezier(0.29, 1.01, 1, -0.68);
```

-   `ease` - Início lento, rápido e final lento (este é o padrão)
-   `linear` - Mesma velocidade do início ao fim
-   `easy-in` - Início lento
-   `easy-out` - Final lento
-   `easy-in-out` - Início e fim lentos
-   `cubic-bezier(n,n,n,n)` - Permite definir seus próprios valores em uma função cubic-bezier (Como um elástico)

# Delay
Basicamente definimos um Timeout para começar a transição, ou seja, se definirmos como `5s` demorara os cinco segundo para iniciar a transição.

```css
transition-delay: 1s;
```