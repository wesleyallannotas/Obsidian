---
title: Diferença entre imperativa e declarativa
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [pf]
description: Entenda a diferença entre programação imperativa e declarativa
---
# Imperativa
Temos todo o controle sobre, dando instruções de **como deve ser feito.**
- O código é pensado e gerado em sequência
- O código é pensado como um passo-a passo, como uma receita de bolo
- Uma coisa depende da outra
- O estado e um dado é alterado constantemente causando mutações nas variáveis
- [[Introdução a POO|Orientação a objeto]] é um tipo de paradigma imperativo

```js
let resultado = [];
function dobrar(array) {
	for (let i = 0; i < array.length; i++) {
		resultado.push(array[i] * 2);
	}
	return resultado;
}

dobrar([1, 2, 3, 4, 5]);

console.log(resultado);
```

# Declarativa
Temos menor controle sobre, dando instruções de o **que fazer e não como.**
- O código é gerado para fazer algo, não importa como
- O que fazer e não como fazer
- Não há necessidade de um passo a passo no código
- [[Introdução a Programação Funcional|Programação Funcional]] é um tipo de paradigma declarativo

```js
const dobrar = array => array.map((item) => item * 2);
console.log(dobrar([1, 2, 3, 4, 5]));
```

# Traçando Paralelo
Podemos concluir que a diferença é que na programação imperativa estamos dando todas as instruções sobre o que deve ser feito, assim possuindo total controle nas nossas mãos, já na declarativa, estamos declarando o que deve ser feito, não possuindo controle sobre como será feito, uma analogia interessante para consolidar é
- **Imperativa** - Pegar o carro, ligar, procurar no mapa, controlar o carro para chegar até o destino.
- **Declarativa** - Chama o taxi fala onde quer ir, chegar até o destino.

Um exemplo real que pode ser percebido no dia a dia trabalhando com o _React_, utilizando JSX

```jsx
const app = document.getElementById('app');
ReactDOM.render(<h1>Resultado</h1>, app);
```

Estamos declarando que queremos renderizar uma elemento `<h1>` com conteúdo `Resultado`, dentro do nosso elemento `app`, onde ele se encarrega de utilizando a API DOM, criar o elemento, adicionar o conteúdo e adicionar ao elemento `app`.