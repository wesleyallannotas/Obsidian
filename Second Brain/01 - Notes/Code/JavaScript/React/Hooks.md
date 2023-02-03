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
Normalmente os Hooks iniciam com `use`, ou seja, `useState` que vimos para [[Introdução ao React#Estados|tratar estados]] é um Hook, em suma Hooks são funções que permitem ligar/conectar os recursos de estado e ciclo de vida do React a partir de componentes totalmente funcionais.
Um tempo atras era comum desenvolver aplicações React utilizando classes, ou seja, forçando o [[Introdução a POO|Paradigma de Programação Orientado a Objeto]], porem a equipe do React resolveu intensificar o uso do [[Introdução a Programação Funcional|Paradigma de Programação Funcional]] que sempre foi a ideia base da biblioteca, assim orientado o uso e criando os Hooks.

# Hook Flow
Quando montamos (_mount_) um componente, inicializamos os estados (_run lazy intializers_), renderiza os componentes no Virtual DOM, renderiza os componentes no DOM real, executa o _layoutEffects_, desenha no Browser, Executa o `useEffects`.
Quando atualizamos (_update_) um componentes, renderizamos no virtual DOM, renderizamos no DOM real, executamos o _cleanup_ do _layouteffects_, executamos o _layoutEffects_, desenhamos no browser, executamos o [[Hooks#Clean up Effect|cleanup do useEffects]] e executamos o [[#useEffect]].
Quando desmontamos um componente é executado o _clenup_ do _layoutEffects_ e o do _useEffects_

>[!attention] Atenção
>Não confundir os _Hooks_ e seu _flow_ com o que era praticado quando se usava classes com a ideia de _Life Cycle_

![[Desenho_React_Hook_Flow|600]]

## Mount
- Quando o componentes e Exibido em tela

## Update
- Componentes "pais" renderizam
- Recebe novas props
- Alteração de estados
- Alteração nos contextos

## Unmount
- Componente sai de tela

## Render Betching
Quando ocorre alterações de um mesmo estado de uma mesma forma dentro de um ciclo ele agrupa as execuções executado apenas a ultima

```js
setState(state + 1)  // Ciclo 1
setState(state + 2)  // Ciclo 1

const data  = await fetchData();  // Ciclo 2

setState(state + 3);  // Ciclo 3
setState(state + 4);  // Ciclo 3
```

A forma contornar esse problema e ocorrer as operações corretamente é passar uma [[Assíncronismo#Callback Function|Callback]] pegando o [[#Assincronismo|valor antigo]].

```js
setState((currentState) => currentState + 1)  // Ciclo 1
setState((currentState) => currentState + 2)  // Ciclo 1

const data  = await fetchData();  // Ciclo 2

setState((currentState) => currentState + 3)  // Ciclo 1
setState((currentState) => currentState + 4)  // Ciclo 1
```

# useState
O estado diferente da variável comum, influencia na renderização da página, quando seu valor é alterado, dispara uma nova renderização utilizando o algoritmo de reconciliação que percebe onde ouve mudança e altera apenas o local de forma performática.
Primeiro é necessário importar um modulo da biblioteca React, que permita tratar o estado, utilizaremos `useState` que nada mais é do que um [[Hooks|Hook]].

>[!attention] Sobre Estados
>Os estados do pai podem ser passados para os filhos, porem nunca o contrairo.

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
Sintaxe base do `useEffect` consiste em um passar como parâmetro/argumento uma _[[Funções#*Arrow Function*|Arrow Function]]_ e uma _[[Introdução ao JavaScript#Array|Array]]_  de dependências que defina quando a nossa função será executada, caso vazia só será executada na montagem e na desmontagem do componente.

>[!attention] Atenção
>Caso não informado a _array_ de dependências como vazia, ou seja, não seja passado o segundo parâmetro
>```tsx
>useEffect(() => {
>	console.log('Executou');
>})
>```
>Todo e qualquer estado que for atualizado executara esse `useEffect`

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

## Clean up Effect
Quando informamos um `return` na nossa função do `useEffect` ela é executada quando o componente e desmontado, ==caso o _array_ de dependências esteja vazia==, essa técnica é muito utilizada quando temos que desconectar de uma [[Dicionario do Programador#API|API]], atualizar um texto em determinado local da página, entre diversas outas ideias.

>[!attention] Atenção
>Quando criamos um retorno, e nosso `useEffects` que possui uma dependência, toda vez que o estado atualizar a função é executada totalmente, assim executando o retorno toda hora, e no exemplo abaixa a cada atualização iria desconectar e conectar

```tsx
useEfect( () => {
	ChatApi.coneect();
	return () => {
		ChatApi.disconnect();
	}
}, []);
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