---
title: Cabeçalho
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [html]
description: Como construir um cabeçalho no HTML
---
# Introdução
O cabeçalho do documento HTML se encontra dentro da tag `<head>`, responsável por guardar metadados da página, não tem influencia diretamente no conteúdo visual da página ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/head)), algumas tags interessante para colocar no nossa cabeçalho são:
- `<meta>` - Meta dados como o charset da página normalmente se usa o UTF-8
- `<title>` - Titulo da página, normalmente aprece na aba do navegador
- `<link>` - Normalmente utilizada para importação, por exemplo de estilo CSS, favicon, entre outros ^8e21a4
- `<script>` - Funciona como a tag `<style>`, possibilitando adicionar código JavaScript no conteúdo, porem a forma que é mais utilizada é para importação de documento JavaScript através do atributo `src`, como boa pratica é inserido no final no `<body>` assim forçando sua execução após o carregamento da página, quando utilizado no `<head>` normalmente acompanha o atributo booleano `defer` que obriga o carregamento do HTML antes do Javascript 

# Definindo Linguagem
Não é na dentro do cabeçalho, porem traz o metadado do idioma do conteúdo.

```html
<html lang="pt-BR">
```

Podemos especificar em um elemento especifico quando seu conteúdo for em outra língua.

```html
<p>Exemplo japonês: <span lang="jp">ご飯が熱い。</span>.</p>
```

# Meta
Largamente utilizada, tem como função determinar meta dados da página, exemplo
```html
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<meta name="author" content="Wesley Silva" />
<meta name="description" content="Meu website pessoal" />
<meta name="robots" content="nofllow, noindex"
```
- `charset` - Codificação de caracteres especiais
- `name` - Especificar o que é o meta dado
- `content`- conteúdo do meta dado

>[!tip] Viewport
>A tag `<meta/>` que trata do _viewport_ é de extrema importância para padronizar o tamanho do `pixel` entre os diferentes _hardawares_ de tela, por exemplo, em uma tela retina que sente bastante a diferença.

>[!note] Descrição
>Importante escrever uma boa descrição, pois, ele que aparece como texto abaixo do titulo do site nos buscadores, caso mantenha ela vazia, o buscado pegara um trecho do site para usar no lugar.

>[!example] Robots
>- `NoFollow` - Informa aos robôs que tem como função identificar os sites não seguir os links que se encontra dentro da página, informando apenas `follow` definimos o contrario.
>- `NoIndex` - Não indexar esta página, também tem o contrário que seria `index`.

## Meta Social
Existem algumas tags meta que podemos adicionar que é usado por redes sociais, por exemplo pelo Facebook que criou o *Open Graph*, onde as tags `<meta>` possuem o atributo `property` seguido de um conteudo, segui alguns exemplo:
```html
<!-- Open Graph Facebook -->
<meta property="og:image" content="" /> <!-- Imagem Miniatura quando compartilha link -->
<meta property="og:description" content="" /> <!-- Texto quando compartilha link -->
<meta property="og:title" content="" /> <!-- Titulo quando compartilha link -->

<!-- Twitter -->
<meta name="twitter:title" content="" /> <!-- Titulo quando compartilha link -->k
```

# Adicionando Ícone
Podemos  adicionar um favicon, ícone que fica junto com o titulo da página no cabeçalho, realizamos a inserção através da tag `<link>`
```html
<link rel="icon" href="assets/icon/icone.png" />

<link type="image/x-icon" rel="shortcut icon" href="nosso_icone.ico" />
```
Atributo `rel` mostra o relacionamento, por exemplo para CSS seria `styleshet`, interessante selecionar que é ==possível especificar diferentes ícones para aparelhos diferentes== para melhor funcionamento, encontramos mais no site MDN famoso pela documentação.

## Ícones específicos
Podemos adicionar diferentes ícones ou resoluções do mesmo para diferentes dispositivos, afim de cobrir a maior variedade.

```html
<!-- iPad de terceira geração com tela retina de alta resolução: -->
<link rel="apple-touch-icon-precomposed" sizes="144x144" href="https://developer.mozilla.org/static/img/favicon144.png">
<!-- iPhone com tela retina de alta resolução: -->
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="https://developer.mozilla.org/static/img/favicon114.png">
<!-- iPad de primeira e segunda geração: -->
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="https://developer.mozilla.org/static/img/favicon72.png">
<!-- iPhone não-Retina, iPod Touch e dispositivos Android 2.1+: -->
<link rel="apple-touch-icon-precomposed" href="https://developer.mozilla.org/static/img/favicon57.png">
<!-- favicon básico -->
<link rel="shortcut icon" href="https://developer.mozilla.org/static/img/favicon32.png">

```


>[!note] Curiosidade
>*Favicon* vem de ícone de favoritos.

# Adicionando CSS
Utilizaremos a mesma tag `<link>` porem alterando o atributo `rel` para especificar que é uma folha de estilo, ficando da seguinte forma:
```html
<link rel="stylesheet" href="assets/css/style.css" />
```