---
title: Entendo estrutura de dados Queue
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [estruturaDados]
description: Funcionamento de Queue sendo exemplificado com JavaScript
---
>[!attention] Atenção
>A linguagem utilizada para os exemplo é o **_JavaScript_**

_Queue_ ou como é mais conhecido em português por **Fila**. Podemos a entender facilmente com uma analogia, imaginando uma fila de caixa (ou de qualquer outra coisa), ou seja, cada elemento que entra fica no final um em atrás do outro, possuindo a característica de linearidade, onde também possui a característica denominada **_FIFO** _first in, first out_, ou seja,  o primeiro elemento a entrar em um _queue o primeiro a sair.

![[Desenho_EsturuaDados_Queue|600center]]


# Criando
Utilizaremos classe no JavaScript para criar a estrutura, vamos seguir os passos vistos na [[Introdução a Estrutura de  Dados|Introdução]]

```js
class Stack {
  constructor() {
    this.data = [];
    this.top = -1;
  }
  push(value) {
    this.top++;
    this.data[this.top] = value;
    return this.data;
  }
  pop() {
    if (this.top < 0) return undefined;
    const poppedTop = this.data[this.top];
    delete this.data[this.top];
    this.top--;
    return poppedTop;
  }
  peek() {
    return this.top >= 0 ? this.data[this.top] : undefined;
  }
}
```