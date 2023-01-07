---
title: Entendo estrutura de dados Stack
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [estruturaDados]
description: Funcionamento de Stack sendo exemplificado com JavaScript
---
>[!attention] Atenção
>A linguagem utilizada para os exemplo é o **_JavaScript_**

_Stack_ ou como é mais conhecido em português por **Pilha**. Podemos a entender facilmente com uma analogia, imaginando uma pilha de livros, ou seja, cada elemento que entra é empilhado um em cima do outro, possuindo a característica de linearidade, onde também possui a característica denominada **_LIFO_** _last in, first out_, ou seja,  o ultimo elemento a entrar em um _stack_  é o primeiro a sair.

![[Desenho_EstruturaDados_Stack|600center]]

# Criando
Utilizaremos classe no JavaScript para criar a estrutura, vamos seguir os passos vistos na [[Introdução a Estrutura de  Dados|Introdução]]

```js
// Passo 1: Modelando
class Stack {
  constructor() {
    this.data = [];
    this.top = -1;
  }
  // Passo 3 Funcionalidades
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

// Passo 2: Utilziando
const stack = new Stack();

stack.push('Elemento 1');
stack.push('Elemento 2');
console.log(stack.pop())
cosnole.log(stack.peek())
```