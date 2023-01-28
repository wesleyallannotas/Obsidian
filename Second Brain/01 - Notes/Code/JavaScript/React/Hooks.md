---
title: Hooks
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description: Entenda os hooks no react. 
---
# Introdução
Normalmente os Hooks iniciam com `use`, ou seja, `useState` que vimos para [[Estados e useState|tratar estados]] é um Hook, em suma Hooks são funções que permitem ligar/conectar os recursos de estado e ciclo de vida do React a partir de componentes totalmente funcionais.
Um tempo atras era comum desenvolver aplicações React utilizando classes, ou seja, forçando o [[Introdução a POO|Paradigma de Programação Orientado a Objeto]], porem a equipe do React resolveu intensificar o uso do [[Introdução a Programação Funcional|Paradigma de Programação Funcional]] que sempre foi a ideia base da biblioteca, assim orientado o uso e criando os Hooks.

# useState
O estado diferente da variável comum, influencia na renderização da página, quando seu valor é alterado, dispara uma nova renderização utilizando o algoritmo de reconciliação que percebe onde ouve mudança e altera apenas o local de forma performática.
Primeiro é necessário importar um modulo da biblioteca React, que permita tratar o estado, utilizaremos `useState` que nada mais é do que um [[Hooks|Hook]].

```js
import React, { useState } from 'react';
```

Agora com `useState` importado, temos que armazenar o nossos estado, com o nome que desejarmos.

```js
const [name, setName] = useState('Padrão');
```

Note que utilizamos [[Expressões e Operadores#Operadores de Desestruturação|desestruturação]] para separar o estado e a função utilizada para manipular seu valor, o valor passada como parâmetro é opcional, e caso usado, servira de valor inicial para o estado.

```jsx
export function Home() {
	const [title, setTitle] = useState('Padrão')
	return (
		<input
			type="text"
			placeholder="Digite o nome..."
			onChange={e => setTitle(e.target.value)}
		/>
		<h1>{title}<h1>
	)
}
```

Agora podemos perceber que quando digitamos no `<input />` o valor é alterado refletindo a interface.

## Assincronismo
A função para manipulação do estado é [[Assíncronismo|Assíncrona]], ou seja, dependendo de vários fatores, a atualização pode não ser instantânea, assim podendo ocorrer incongruências com o valor armazenado no estado atualmente, para resolver esse problema, podemos capturar o valor anterior real que é disponibilizado, através de um parâmetro e utiliza-lo para realizar a alteração através de [[Assíncronismo#Callback Function|Callback]].

```tsx
export const Counter = () => {
  const [counter, setCounter] = useState<number>(0);
  function add() {
    setCounter(prevState => prevState + 1);
  }
  function subtract() {
    setCounter(prevState => prevState - 1);
  }
  return (
    <>
      <h3>{counter}</h3>
      <button onClick={add}>Add</button>
      <button onClick={subtract}>Remove</button>
    </>
  );
};
```

# useEffect
Sintaxe base do `useEffect` consiste em um passar como parâmetro/argumento uma _[[Funções#*Arrow Function*|Arrow Function]]_ e uma _[[Introdução ao JavaScript#Array|Array]]_  de dependências. 

```jsx
useEffect(() => {
	// Corpo do useEffect
}, []);
```

Dentro do corpo da função anônima, que no caso a escolhida foi a _Arrow Funciton_ pela simplicidade e a limpeza que traz ao código,  será informado as ações que queremos executar, já no _array_, informamos os estados que o nosso `useEffect` depende, ou seja, toda vez que tal estado for atualizado é executado o `useEffect` novamente.
`useEffect` é ==executado automaticamente assim que a interface for renderizada== e caso a _array_ de dependências estiver vazias essa será sua única execução.

```jsx
useEffetc(() => {
	console.log("useEffect foi chamado!");
}, [students]);
```

Quando carrega a página executa, e toda vez que atualizar o estado `students`, executa novamente.
Muito utilizado para consumir APIs

```jsx
  useEffect(() => {
    fetch('https://api.github.com/users/wesleyallan')
      .then( response => response.json())
      .then( data => {
        setUser({
          name: data.name,
          avatar: data.avatar_url
        })
      })
  }, [])
```

## Utilizando sintaxe Async/Await
Caso a sintaxe do _[[Assíncronismo#Async/Await|Async/Await]]_ for a desejado pelo programador responsável, podemos utiliza-la cirando uma função assíncrona e a executando, dentro do corpo da _Arrow Function_ ficando da seguinte forma.


```jsx
  useEffect(() => {
    async function getUser() {
      try {
        const user = await fetch('https://api.github.com/users/wesleyallan').then( response => response.json());
        setUser({
          name: user.name,
          avatar: user.avatar_url
        });
      } catch (err) {
        console.error(err.message);
      }
    };
    getUser();
  }, [])
```

Possuímos total liberdade para ==declarar a função assíncrona dentro ou fora do corpo da _arrow function_ do useEffets==, normalmente mantemos dentro quando é algo que desrespeito a apenas o `useEffect`, caso é algo reutilizável é interessante manter fora.