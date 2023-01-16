---
title: Componentes
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description: Como utilizar componentes no React 
---
# Estrutura do Componente
Normalmente é uma função que retorna um _React Elements_, seja por meio da notação padrão ou com o uso de extensão de sintaxe com `jsx`/`tsx`, e essa função é exportada, possuindo duas formas de exportar.

## Utilizando default
Estamos especificando que por padrão quando importar esse "modulo" ou melhor no contexto React Componente, será exportado a `Home`, ou seja, quando acontecer a importação comum, é importado a `Home`

```jsx
function Home() {
	return (
		<h1 className="greetings">Bem Vindo!</h1>
	)
}
export default Home;
```

```js
import Home from './pages/Home';
```

## Exportando na declaração
Deste modo não terá um _default_ para importar, assim sendo necessário especificar na importação.

```jsx
export function Home() {
	return (
		<h1 className="greetings">Bem Vindo!</h1>
	)
}
```

```js
import { Home } from './pages/Home';
```

# Utilizando Componente
Normalmente nomeamos nossos componentes utilizando Letras Maiúsculas no inicio de cada palavra, para diferenciar de Tags nativas do HTML, ficando da seguinte forma.
Arquivos `.JSX` ou `.TSX` temos a liberdade de omitir a extensão.

>[!attention] Padrão de Importação
>Caso nosso importação bate em um diretório, o React possui a expertise de procurar pelo `index` dentro desse diretorio.

```jsx
import Comment from './Comment';

function Home() {
	return (
		<>
		<h1>Comentarios</h1>
		<Comment />
		</>
	)
}
```

# Propriedades
Podemos definir propriedades para o nosso componente a fim de o deixar dinâmico e possibilitar o reuso, a sintaxe é igual de atributos no JavaScript `propriedade="valor"`

```jsx
// Utilizando nosso componente
<Card name="Wesley Silva" time="10:45:24" />
```

Assim o nosso componente tem valores para as propriedades `name` e `time`.
Agora precisamos utiliza-las dentro do componente, obtemos as propriedades através de um parâmetro/argumento na nossa função que retorna o componente, casó ache interessante podemos utilizar a técnica que [[Expressões e Operadores#Operadores de Desestruturação|Desestruturação]].

```jsx
export function Cart(props) {
	return (
		<strong>{props.name}</strong>
		<small>{props.time}<small>
	)
}

// Desestruturação
export function Cart({name, time}) {
	return (
		<div>
			<strong>{name}</strong>
			<small>{time}<small>
		</div>
	)
}
```