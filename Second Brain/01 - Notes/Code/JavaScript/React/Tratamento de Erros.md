---
title: Tratamento de Erros
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description: Tratando erros utilizando React
---
# Introdução
O tratamento de erros é extremamente importante para o usuário não ser surpreendido com um mau funcionamento sem nenhum aviso ou explicação, sendo até mesmo importante para os desenvolvedores encontrarem o real foco dos erros mais rápido e eficientemente. 

# Error Boundaries
Adicionado na versão 16, basicamente é um componente que colocamos para abraçar toda nossa arvore de componentes e tem como função tratar erros dos componentes "uma espécie de _try...catch_ para os componentes" usado como tratamento de erro global, não deve ser usado para tratar erros específicos, pois, um [[Controle de Fluxo#Throw e try...catch|try..catch]] não funciona para varios componentes de uma vez, porem, _error boundaries_ tem seu uso limitado, por exemplo não tratando.
- Event Handlers - Eventos de botão por exemplo
- Assyncronous Code - [[Timers#Timeout|setTimeout]] por exemplo.
- Server side rendering
- Errors thrown, ou seja, erros gerados pelo próprio _error boundaries_

Por exemplo no exemplo abaixo, com uma tipagem feita de forma irresponsável onde caso utilizado sem passar corretamente as propriedades, pode não ocorrer a renderização do componentes, não resultando em nenhuma informação para o usuário, além de uma interface vazia, onde o erro é apenas exibido no console.

```tsx
const Counter = (props: any) => {
	return <h1>The total counter is {props.counter.toFixed(2)}</h1>
}

function App() {
	return (
		<div className="App">
			<Counter />
		</div>
	)
}
```

Uma ideia comum de quem conhece a linguagem e a utilização do [[Controle de Fluxo#Throw e try...catch|try...chatch]] para a tratativa de erros. funcionara, porem será necessário manter essa abordagem na construção de todos os componentes, sem falar que estamos fugindo da ideia programação declarativa do React.

```tsx
const Counter = (props: any) => {
	try {
		return <h1>The total counter is {props.counter.toFixed(2)}</h1>
	} catch (err) {
		return <h1>Ups, something went wrongs</h1>
	}
}

function App() {
	return (
		<div className="App">
			<Counter />
		</div>
	)
}
```

Uma ideia que pode vir a mente e em vez de ter que construir tal estrutura por componente, abraçar todos dentro de um componentes maior.

```tsx
const Counter = (props: any) => {
	return <h1>The total counter is {props.counter.toFixed(2)}</h1>
}

function App() {
	try {
		return (
			<div className="App">
				<Counter />
			</div>
		)
	} catch (err) {
		return (
			<h1>Ups, something went wrongs</h1>
		)
	}
}
```

Não funcionara, ou seja, podemos concluir que a abordagem do uso de _try...catch_ funciona, caso adotada dentro de cada componentes, não funcionando para abraçar diversos componentes diferentes.
Assim sendo criado o _Error boundaries_ para prevenir tal problema, porem sua construção era baseada em classes, e caso não for de interesse do programador misturar os paradigmas de programação através do uso de [Classes para construção de error boundaries](https://reactjs.org/docs/error-boundaries.html#:~:text=Error%20boundaries%20are%20React%20components,the%20whole%20tree%20below%20them.), o mesmo tem a opção de utilizar uma biblioteca muito interessantes que pode ser instalada facilmente por meio do `npm` [react-error-boundary](https://www.npmjs.com/package/react-error-boundary).

```tsx
import { ErrorBoundary } from 'react-error-boundary';

const Counter = (props: any) => {
	return <h1>The total counter is {props.counter.toFixed(2)}</h1>
}

const ErrorHandler = () => {
return (
	<h1>Ups, something went wrongs</h1>
)
}

function App() {
	return (
		<ErrorBoundary FallbackComponent={ErrorHandler}>
			<div className="App">
				<Counter />
			</div>
		</ErrorBoundary>
	)
}
```

Normalmente é preenchido também um evento para o `onError` onde é capturado os parâmetros possíveis para essa [[Assíncronismo#cal|callback]] e normalmente enviado os dados do erro através de uma API. seja para enviar um e-mail ou armazenar tal informação em outro local.
Podemos também utilizar plataforma especializadas no tratamento de erros como Bugsnag, Sentry, entre outras.