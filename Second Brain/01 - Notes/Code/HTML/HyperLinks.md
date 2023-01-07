---
title: HyperLinks
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [html]
description: Como criar hyperlinks 
---
# Introdução
Hyperlinks ou de forma abreviada links são o coração da web, tanto é que esta pressente no nome da nossa linguagem de marcação HTML (Hypertext Markup Language), também chamado de ancora tem como objetivo ligar páginas web facilitando a navegação. ([Doc](https://developer.mozilla.org/pt-BR/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks))

# Anatomia
A base da tag ancora é `<a href=""></a>`, onde o conteúdo guarda o texto que se clicado levara ao link, e o atributo `href` guarda o endereço da página referenciada.
```
<a href="https://google.com">Google</a>
```

## Atributos
A tag ancora tem muitos atributos compatíveis, porem o mais importante e obrigatório é o `href`, de forma mais completa:
- Aceita atributos globais
>[!revisao] Recapitulando
![[Introdução ao HTML#Atributos Globais]]
- href
	- url completa - `http://google.com`
	- fragmento - `#sobre` partes da mesma página web que tiverem o **ID** correspondente
	- email - `mailto:wesley.allansilva@gmail.com`
	- telefone - `tel:+5518997386519`
	- outros
- download
- target
	- \_self - **Padrão**, abre na mesma página 
	- \_blank - Abre um uma nova aba

## Conteúdo
Dentro do conteúdo do hyperlink podemos adicionar qualquer coisa, não estamos limitados somente a textos, por exemplo, podemos adicionar uma imagem entre outras mídias, ate mesmo vários blocos de conteúdo, estamos totalmente livres.

## URLs
URL vem do inglês *Uniform Resource Locator*, em sua essência possui o significado "Sequência de texto que define onde algo está localizado na Web", onde URL usam caminhos para encontrar arquivos.
Dentro do mesmo projeto podemos utilizar caminhos dos arquivos.

### URLs Absolutas e Relativas
Sempre aponta para o mesmo local independente da onde se encontra atualmente, já as URLs relativas tem seu comportamento influenciado pela localização atual
- Absoluto - `https://google.com`
- Relativo - `google.com`