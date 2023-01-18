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