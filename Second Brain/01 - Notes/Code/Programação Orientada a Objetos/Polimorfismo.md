---
title: Entendo polimorfismo em POO
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [poo]
description: Entenda o conceito de polimorfismo. 
---
# Conceito
Quando um objeto estende de outro (**Herança**) talvez haja a necessidade reescrever uma ou mais características (**Atributos e Métodos**) nesse novo objeto. Recriando então um método (ou mais) da classe herdada (Polimorfismo significa muitas formas), para maior entendimento podemos criar uma analogia, a classe pai ave tem o método `voar()` porem, esse método será diferente nos seus filhos galinha, pato e gavião por exemplo.

# Polimorfismo com JavaScript
Criaremos uma classe Atleta, onde ocorrera um polimorfismo na classe `definirCategoria()`

```js
class Atleta {
  peso;
  categoria;
  constructor(peso) {
    this.peso = peso;
  }
  definirCategoria() {
    if (this.peso <= 50) {
      this.categoria = 'Infantil';
    } else if (this.peso <= 65) {
      this.categoria = 'Juvenil';
    } else {
      this.categoria = 'Adulto';
    }
  }
}
  
class Lutador extends Atleta {
  constructor(peso) {
    super(peso);
  }
  definirCategoria() {
    if (this.peso <= 54) {
      this.categoria = 'Pluma';
    } else if (this.peso <= 60) {
      this.categoria = 'Leve';
    } else if (this.peso <= 75) {
      this.categoria = 'Meio-Leve';
    } else {
      this.categoria = 'Pesado';
    }
  }
}

let antonio = new Atleta(67);
let carlos = new Lutador(67);

console.log(antonio.categoria);
antonio.definirCategoria();
console.log(antonio.categoria);
console.log(carlos.categoria);
carlos.definirCategoria();
console.log(carlos.categoria);
```