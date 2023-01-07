---
title: Entendo abstração em POO
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [poo]
description: Entenda o conceito de abstração. 
---
# Conceito
O conceito de abstração se baseia na ideia de criar uma espécie de _template_ (Identidade), que será construída no futuro, ou seja, atributos e métodos podem ser criados na classe de **Abstração** (**Superclasse**), mas a implementação de métodos e atributos, só poderá ser feita na classe que irá herdar essa **Abstração**, por exemplo o classe pai que será a classe abstrata (**superclasse**) criou o método `gravar()`, porem não implementou, os filhos então implementam o `gravar()` da sua maneira.

# Abstração com JavaScript
Criaremos uma classe parafuso utilizando o conceitos de abstração

```js
class Parafuso {
  constructor() {
    if (this.constructor === Parafuso) {  // Caso tente instanciar parafuso
      throw new Error('Classe abstrata não pode ser instânciada');
    }
  }
  get tipo() {
    throw new Error('Método "get tipo()" precisa ser implementado');
  }
}
  
class Fenda extends Parafuso {
  constructor() {
    super();
  }
  get tipo() {
    return 'fenda';
  }
}
  
class Philips extends Parafuso {
  constructor() {
    super();
  }
  get tipo() {
    return 'philips';
  }
}
 
class Allen extends Parafuso {}
  
let fenda = new Fenda();
let philips = new Philips();
let allen = new Allen();
  
console.log(fenda.tipo, philips.tipo);
console.log(allen.tipo);
```