---
title: Explicando Recursão
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [algoritmo]
description: Entenda o coneito de recursão
---
Recursão no mundo da programação, nada mais é do que uma função que chama ela mesma, se baseia na ideia caso-base e caso-recursivo, onde enquanto o caso-base não é atingido, executa o caso-recursivo que chama a si mesmo, um algoritmo muito famoso que utiliza essa ideia é o [[Quick Sort]], uma recursão deve mudar seus estado, se aproximando cada vez mais do caso-base, caso contrario entrara em _loop_ infinito, existem classificações para as funções recursivas.
- **Recursão Direta** - Ela mesmo se chama novamente.
- **Recursão Indireta** - Chama uma função que chama ela novamente.
- **Função Recursiva em Cauda** - A chamada da recursividade é a ultima instrução a ser executada.
- **Função Non-Tail Recursive** - Função sem cauda, qualquer outro caso que não tenha cauda.

# Caso-Base
Caso base é o que basicamente o que para o _loop_ que a recursão cria, ele é o resultado que esperamos.

# Caso Recursivo
E o que deve ser feita enquanto o [[#Caso-Base]] não for atingido.

# Pilha de Chamadas
Pilha de chamadas do inglês *call [[Stack]]*, basicamente são as chamadas que o computador vai acumulando em um [[Stack]], e como podemos observar recursão chama a si mesmo, ou seja, vai acumulando na [[Stack]] as chamadas mantendo as funções anteriores em estado de parcialmente completa mantendo todos os dados na memoria, e quando chega no caso recursivo todas vem fechando e devolvendo o valor para a anterior.

# Exemplo 
Função recursiva que calcula a fatorial de um número.
```js
const factorial = x => {
	if (x === 1) {
		return 1;
	}
	return x * factorial(x * -1);
}
```