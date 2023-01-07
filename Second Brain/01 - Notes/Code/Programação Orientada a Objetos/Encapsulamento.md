---
title: Entendo encapsulamento em POO
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [poo]
description: Entenda o conceito de encapsulamento. 
---
# Conceito
Podemos entender com uma analogia simples, ""**Você pode dirigir um carro, sem conhecer o funcionamento ou como foi feito o motor do carro**", basicamente é o agrupamento de variáveis e funções, escondendo detalhes de implantação, adicionando uma camada de segurança para os atributos e métodos, por exemplo quando você da a partida no carro, tudo que é necessário fazer, e que ocorre dentro do motor é encapsulado, você só usa a função `partida()`

# Encapsulamento no JavaScript
Vamos transformar um programa estrutural que calcula a área de um polígono em uma classe utilizando as técnicas de encapsulamento.

```js
// Estrutural
let altura = 50;
let largula = 50;

function calculaArea() {
	return altura * largura;
};

let area = calculaArea();
```

Aplicando os conceitos, fica da seguinte forma.

```js
class Poligono {
  constructor(largura, altura) {
    this.largura = largura;
    this.altura = altura;
  }
  get area() {
    return this.#calcularArea();
  }
  #calcularArea() {
    return this.largura * this.altura;
  }
}
```

- `#` - Quando utilizamos o caractere `#` estamos informando que não queremos que esse método seja visível, uma espécie de `private`.