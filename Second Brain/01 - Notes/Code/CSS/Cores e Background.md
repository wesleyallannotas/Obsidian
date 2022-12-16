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
# Cores
Manipulação de cor e algo muito recorrente quando estamos utilizando CSS, dominar as formas de se fazer e muito interessante para se tornar um profissional completo, segui alguns tipos de aplicação de cor utilizando CSS
- `background-color`
- `color`
- `border-color`
- entre outros...

## Valores
Os valores aceito para o *data-type* `<color>` são:
- Palavras-chave
	- *Keyword Values* - `currentcolor`
	- `<named-color>` - `blue`, `tomato`, `transparent`, entre outros...
- Hexadecimal - `#ffffff`, `#202120`, entre outros...
- Funções - `hsl()`, `hsla()`, `rgb()` e `rgba()`
- *Global Values* - `inherit`, `initial`, `unset`

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

##  RGB (`rgb()`)
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

## HSL (`hsl()`)
HSL que do inglês significa *Hue Saturation Lumiance*, possui uma complexidade maior do que os outros modos de atribuir valor do tipo *data-type* `<color>` apresentados anteriormente, seu funcionamento é o seguinte:
![[HSL.png|center]]

## *Global Values*
- `inherit` - Vem de herança, herda do elemento anteiro, ou seja, o elemento pai
- `initial` - Volta a cor inicial
- `unset` - Não defini cor, acaba pegando do contexto

# Background
Background é o fundo, ou seja, qual o estilo aplicado ao fundo do nosso elemento, existem diversas possibilidades desde de cores solidas a até mesmo imagens e formas de posiciona-las, o objetivo e destrinchar pelo menos as propriedades mais importantes e utilizadas

## Cores
Para aplicar uma cor solida no fundo do nosso elemento, podemos utilizar a propriedade `background-color` onde a mesma aceita *data-type* do tipo `<color>`, por exemplo:
```css
div {
	background-color: rgb(55, 100, 50);
}
```

## Imagens
Podemos adicionar imagem ao fundo do nosso elemento utilizando `background-image`, onde atrelado a função `url()` podemos passar o endereço da imagem, adicionar imagem via CSS é recomendado apenas para fins de estilização, segue um exemplo de uso:
```css
body {
	background-color: url(https://www.google.com/logos/doodles/2022/celebrating-claudio-kano-6753651837109785-l.webp);
}
```
>[!warning] Atenção
 Não é recomendado adicionar imagens importante para o conteúdo via CSS, pois, ocorre perda semântica

### Repetição
Por padrão quando adicionamos uma imagem, a propriedade que controla a repetição vem configura para repetir ate que complete todo o espaço do elemento, podemos alterar esse comportamento através do elemento `background-repeat`, por exemplo:
>[!tip] Dica
>Suporta mais que um valor atribuído, pois, podemos adicionar mais de uma imagem no `background-image`.
```css
bodu {
	background-color: url(https://www.google.com/logos/doodles/2022/celebrating-claudio-kano-6753651837109785-l.webp);
	background-repeat: no-repeat;
}
```
Também é uma opção controlar a repetição:
- `repeat-y` - Repete a imagem apenas no eixo Y
- `repeat-x` - Repete a imagem apenas no eixo X

### Posição
Podemos controlar a posição da imagem do nosso fundo através da propriedade `background-position`, por exemplo:
```css
body {
	background-color: url(https://www.google.com/logos/doodles/2022/celebrating-claudio-kano-6753651837109785-l.webp);
	background-repeat: no-repeat;
	background-position: center; /* XY */
	background-position: center center; /* X Y */
}
```
Aplicamos um *data-type* do tipo `<position>` para o eixo X e eixo Y respectivamente, caso informarmos apenas um valor esse assume o mesmo para ambos.

### Tamanho
Podemos controlar o tamanho da nossa imagem de fundo através da propriedade `background-size`, onde podemos passar os seguintes *data-types* como valor:
- `contain` - Aumenta o máximo possível mantendo a proporção da imagem e se mantendo dentro do elemento, o que importa e se manter inteiramente visível.
- `cover` - Aumenta a imagem o máximo possível para cobrir todo o elemento, porem mantendo a proporção, não se importa em manter dentro, pode aumentar muito, o que importa e cobrir inteiro o elemento.
- `auto` -  Ajusta a imagem de fundo para tal direção de modo que mantenha a proporção da imagem inalterada.
- `<length>` - Valores de tamanho, pode atribuir um ou dois valores que será para `width` e `height`, caso informe apenas um, assumira `auto` para o outro
- `<porcentage>` - Valores de porcentagem, pode atribuir um ou dois valores que será para `width` e `height`, caso informe apenas um, assumira `auto` para o outro
```css
body {
	background-color: url(https://www.google.com/logos/doodles/2022/celebrating-claudio-kano-6753651837109785-l.webp);
	background-repeat: no-repeat;
	background-size: cover;
	background-size: 50% 30%; /* width heigth */
	background-size: 50%; 
}
```

### Origem
Podemos mudar a origem da imagem, ou seja, do ponto em que ela se inicia, por padrão ela é iniciada depois da borda, ou seja, caso utilizarmos uma borda larga com estilo `dashed` podemos observar que a imagem só vai iniciar após o fim da borda, pois essa é o valor para `background-origin` padrão, porem podemos alterar
```css
body {
	background-color: url(https://www.google.com/logos/doodles/2022/celebrating-claudio-kano-6753651837109785-l.webp);
	background-repeat: no-repeat;
	background-size: cover;
	background-origin: border-box;
}
```
Os valores aceitos são os mesmo do [[Box Model#Box-Sizing|box sizing]], porem diferente do `box-sizing`, seu valor padrão não é `content-box` e sim `padding-box`

### *Clip*
A propriedade `background-clip` controla uma "caixa" anterior a propriedade `background-origin`, ele controla tudo desde a imagem e a cor de fundo, pode ocorrer ate mistura das duas propriedades para alcançar o resultado desejado
```css
body {
	background-color: url(https://www.google.com/logos/doodles/2022/celebrating-claudio-kano-6753651837109785-l.webp);
	background-repeat: no-repeat;
	background-size: cover;
	background-origin: border-box;
	background-clip: padding-box;
}
```
Assim como a propriedade `background-orign` aceita os mesmo valores do [[Box Model#Box-Sizing|box sizing]].
>[!warning] Atenção
>Caso a origem seja maior que o *clip* como no exemplo a abaixo:
>```css
>body {
>	background-color: url(https://www.google.com/logos/doodles/2022/celebrating-claudio-kano-6753651837109785-l.webp);
>	background-repeat: no-repeat;
>	background-size: cover;
>	background-origin: border-box;
>	background-clip: content-box;
>}
>```
>A imagem será cortada!

### *Attacment*
A propriedade `background-attachment` é responsável por controlar o comportamento do fundo do elemento quando utilizamos o scroll, caso exista, valores aceitos:
- `scroll` - Valor padrão, background é fixo em relação ao elemento em si e não rola com seu conteúdo. (É efetivamente ligado à borda do elemento.)
- `fixed` - Background é fixo em relação ao *viewport*. Mesmo que um elemento tenha um mecanismo de rolar, o background `fixed` não movimenta com o elemento.
- `local` - Background é fixo em relação ao conteúdo do elemento: ise ele tem um mecanismo de rolar, o background rola com o conteúdo do elemento, e a área pintada e o posicionamento do background são relativos à área de rolagem do elemento ao invés da borda de fronteira deles.
>[!tip] Dica
>Suporta mais que um valor atribuído, pois, podemos adicionar mais de uma imagem no `background-image`.
```css
body {
  background-image: url("starsolid.gif"), url("startransparent.gif");
  background-attachment: fixed, scroll;
  background-repeat: no-repeat, repeat-y;
}
```

## Shorthand
Background assim como outras muitas propriedades possui seu [[01 - Notes/Code/CSS/Introdução#Shorthand|shorthand]] que com sua utilização traz diversos benefícios. 
```css
body {
	background: rgb(55, 100, 50) url("starsolid.gif") no-repeat center top / contain border-box content-box scroll;
}
```
Utilizando essa declaração caso especificarmos um valor para o `background-origin` e ira utilizar o mesmo para o `background-clip` caso queira que seja diferente, é necessário especificar começando pelo valor aplicado ao `background-origin`.

>[!warning] Atenção
>Para o bom funcionamento e recomendado seguir essa ordem e a utilização da barra (`/`) para uma boa identificação dos valores para as propriedades corretas.

É possível declarar mais de um background, separando por virgulas, por exemplo
```css
body {
	background: lienar-gradient(rgba(255, 255, 255, 0), rgba(255, 0, 0, 0.2)), url("starsolid.jpg") no-repeat right top / 50px border-box content-box fixed;
}
```
Assim podem criar background incríveis com as misturar possíveis, podendo misturar ate o funcionamento do scroll e outras propriedades.

## Gradiente
Para aplicarmos um efeito gradiente no nosso fundo do elemento, ou seja, no background, podemos utilizar as seguintes funções
- `linear-gradient()` - Gradiente comum criando uma variação de cores de uma lada para o outro
- `radial-gradient()` - Gradiente em forma de circulo se iniciando do meio
```css
body {
	background: linear-gradient(red, yellow);
	background: radial-gradient(red, yellow);
}
```
Podemos atribuir mais valores a essa função para um resultado mais interessante, por exemplo podemos alterar o ângulo do gradiente, pela logica só podemos adicionar ângulo em um gradiente linear
```css
body {
	background: linear-gradient(45deg, red, yellow);
}
```
Para um gradiente básico utilizamos duas cores, porem nada nos impede de adicionar mais cores
```css
body {
	background: linear-gradient(45deg, red, yellow, red);
	background: radial-gradient(red, yellow, red);
}
```
Para as cores é aceito o *data-type* `<color>`, ou seja, todas os tipos de [[#Valores|declaração de cores]] são aceitas.