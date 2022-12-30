---
title: Manipulando o DOM
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [js]
description: Como manipular o DOM com o JavaScript 
---
# Introdução
DOM é uma sigla para *Document Object Model*, basicamente é um **HTML convertido** para um **objeto JavaScript**. É uma **API** (Ajuda você a interagir com alguma pessoa) que **representa e interage** com o HTML, **Estrutura de dados** do tipo **Árvore**, criada pelo browser, por se tratar de um objeto obviamente contem propriedades e métodos.
Diante disse concluímos que JavaScript usa o DOM para se conectar e manipular o HTML, assim sendo o grande responsável pela possibilitando da programação Web.
```html
<!DOCTYPE html>
<html lang="pt-BR">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Exemplo de DOM</title>
	</head>
	<body>
		<h1>DOM</h1>
	</body>
</html>
```
![[Desenho_JS_DOM|500center]]
Ocorre a relação de pai e filho, por exemplo `document` sendo pai de `body` e assim sucessivamente, 