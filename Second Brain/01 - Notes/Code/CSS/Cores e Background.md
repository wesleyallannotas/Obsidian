---
title: Cores e Background no CSS
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Como manipular cores e o background utilizando CSS 
---
# Introdução
Manipulação de cor e algo muito recorrente quando estamos utilizando CSS, dominar as formas de se fazer e muito interessante para se tornar um profissional completo, segui alguns tipos de aplicação de cor utilizando CSS
- `background-color`
- `color`
- `border-color`
- entre outros...

# Valores
Os valores aceito para o *data-type* `<color>` são:
- palavras-chave
	- *Keyword Values* - `currentcolor`
	- `<named-color>` - `blue`, `tomato`, `transparent`, entre outros...
- hexadecimal - `#ffffff`, `#202120`, entre outros...
- funções - `hsl()`, `hsla()`, `rgb()` e `rgba()`

## Hexadecimal (`<hex-color>`)
Basicamente declaramos valores para as cores vermelho (*red*), verde (*green*), azul (*blue*) e transparência sendo essa opcional , que são as cores primarias, através do mix de valores para elas geramos outras cores, podemos declarar um `<hex-color>` de diversas formas, sendo elas:
```css
p {
	color: #090;
	color: #009900;
	color: #090a;
	color: #009900aa;
}
```
Os valores aceitas estão entre `0` e `f` totalizando 16 possibilidades para cada casa do valor, quando mais valores podemos especificar melhor a cor que desejamos.
![[Desenho_HTMLCSS_Cores_Hexadecimal|center]]

#  RGB (`rgb()`)
Por meio da função `rgb()` que temos no CSS podemos atribuir valores para as cores vermelho (*red*), verde (*green*) , azul (*blue*) e transparência sendo esta opcional, podemos para as cores atribuir valores entre `0` e `255`, para o canal alfa que é o responsável pela transparência podemos atribuir valores entre `0` e `1`, ou porcentagem, por exemplo, `50%`., segui exemplo de declaração:
```css
p {
	color: rgb(30, 12, 64);
	color: rgb(30, 12, 64, 0.6);
	color: rgb(30, 12, 64, 60%);
	color: rgb(30 12 64);
	color: rgb(30 12 64 / 0.6);
	color: rgb(30 12 64 / 60%);
}
```

# HSL (`hsl()`)
HSL que do inglês significa *Hue Saturation Lumiance*, possui uma complexidade maior do que os outrs modos de atribuir valor do tipo *data-type* `<color>` apresentados anteriormente