---
title: Entenda a estrutura de dados Matrix
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [estruturaDados]
description: Entenda a estrutura de dados matrix com JavaScript
---
>[!attention] Atenção
>A linguagem utilizada para os exemplo é o **_JavaScript_**

Matrix basicamente é uma [[Array]] multidimensional, ou seja, para atingirmos essa característica basta adicionar _arrays_ dentro de uma _array_, ficando da seguinte forma.

```js
let matrix = [
	[1 , 2, 3],
	[4, 5, 6],
	[7, 8, 9]
]

matrix[2][1]  // Resultado: 5
```