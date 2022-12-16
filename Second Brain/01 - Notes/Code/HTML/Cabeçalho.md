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
O cabeçalho do documento HTML se encontra dentro da tag `<head>`, responsável por guardar metadados da página, não tem influencia diretamente no conteúdo visual da página, algumas tags interessante para colocar no nossa cabeçalho são:
- `<meta>` - Meta dados como o charset da página normalmente se usa o UTF-8
- `<title>` - Titulo da página, normalmente aprece na aba do navegador
- `<link>` - Normalmente utilizada para importação, por exemplo de estilo CSS, favicon, entre outros
- `<script>` - Funciona como a tag `<style>`, possibilitando adicionar código JavaScript no conteúdo, porem a forma que é mais utilizada é para importação de documento JavaScript através do atributo `src`, como boa pratica é inserido no final no `<body>` assim forçando sua execução após o carregamento da página, quando utilizado no `<head>` normalmente acompanha o atributo booleano `defer` que obriga o carregamento do HTML antes do Javascript 

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
```
Atributo `rel` mostra o relacionamento, por exemplo para CSS seria `styleshet`, interessante selecionar que é ==possível especificar diferentes ícones para aparelhos diferentes== para melhor funcionamento, encontramos mais no site MDN famoso pela documentação.

>[!note] Curiosidade
>*Favicon* vem de ícone de favoritos.

# Adicionando CSS
Utilizaremos a mesma tag `<link>` porem alterando o atributo `rel` para especificar que é uma folha de estilo, ficando da seguinte forma:
```html
<link rel="stylesheet" href="assets/css/style.css" />
```