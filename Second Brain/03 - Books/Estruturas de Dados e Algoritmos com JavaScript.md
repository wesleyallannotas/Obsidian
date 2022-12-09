---
title: Estruturas de Dados e Algoritmos com JavaScript 8ª Edição
author: Loiane Groner
bookImageUrl: '[71KGa1y8eaL.jpg (1500×2091) (media-amazon.com)](https://m.media-amazon.com/images/I/71KGa1y8eaL.jpg)'
type: book
completed: false
aliases:
tags: book
description: Livro que aborda estrutura de dados e algoritmos utilizando javascript
---
# Estruturas de Dados e Algoritmos com JavaScript 8ª Edição
![Capa|120](https://m.media-amazon.com/images/I/71KGa1y8eaL.jpg)

# Capitulo 1: JavaScript - Uma Visão Geral Rápida

# Variáveis
Armazena dados que podem ser definidos, atualizados e recuperados sempre que for necessário, os valores atribuídos a uma variável tem um tipo, por exemplo em JavaScript temos os seguintes tipos:
- **Number** - Qualquer tipo de número `1`, `2`, `3`, `4.5`, `4.7`, `-2`, ...
- **String** - Cadeia de caracteres `"A"`, `"a"`, `"asd"`, `"as87"`, ...
- **Boolean** - Verdadeiro e falso `true`, `false`.
- **Undefined** - Indefinido, ocorri quando é declarado a variável, porem a mesma não tem seu valor atribuido
- **Null** - Variável com valor atribuído igual a nulo
- **Function** - Funções
- **Object** - Objetos, por exemplo, `let carro = {nome: "Saveiro", ano: 2007}`
- **Array** - Espécie de lista, `let pessoas = ["Antonio", "Jose", "Carlos"]`
	- Array é considerado um tipo de objeto.
JavaScript mesmo possuindo tipos diferentes de variáveis ==não é considerada fortemente tipada== como as linguagens C, C++, Java, entre outras, pois, sua ==tipagem ocorre de forma dinâmica== não havendo a declaração do tipo da variável em sua declaração, por exemplo, em Java declarando uma variável  `num` do tipo inteira de valor 2:
```java
int num = 2
```
JavaScript declarando uma variável `num` do tipo `number` de valor 2:
```javascript
var num = 2
```
Em JavaScript não declaramos o tipo da variável, e sim utilizamos a palavra reservada `var` neste caso.

>[!warning] Importante
>A discussões sobre qual declaração deve ser utilizada, pois, impacta diretamente no escopo, para varáveis possuímos `var` e `let`