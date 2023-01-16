---
title: JSX e TSX
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description: Entendendo o que são os arquivos .JSX e .TSX 
---
# Introdução
O JSX e TSX, onde JSX é para JavaScript e TSX é para TypeScript, nada mais é do que uma extensão de sintaxe que possibilita o uso de HTML dentro do JavaScript, continua estando mais próximo do JavaScirpt do que do HTML, traz maior facilidade para o entendimento e organização do código, basicamente por baixo dos panos ele criar elementos React com `React.createElement()`, quem é encarregado de fazer essa conversão é o `Babel`

```jsx
// Usando JSX
const element = <h1 className="greeting">Hell</h1>;

// Elemento React
const element = React.createElement(
	'h1',
	{className: 'greeting'},
	'Hello, world!'
)
```

# Incorporando Valor
Podemos adicionar qualquer código JavaScript para obter valor através do uso de chaves `{ }`, por estar mais próximo do JavaScript usa camelCase, por exemplo para adicionar ao atributo `class` utilizamos `className`

```jsx
const element = <h1>Ola! {person.name}</h1>;
const element = <h1>Ola! {formatName(user)}</h1>;
const element = <img src="https://avatars.githubusercontent.com/u/93749822?v=4" />;
const element = <img src={user.avatarUrl} />;
```

# Previne Ataques de Injeção
O React DOM escapa qualquer valor [[#Incorporando JavaScript|incorporado]] pelo JSX antes de renderiza-los, tudo é convertido para [[Introdução ao JavaScript#String|String]], ajudando a previne ataques XSS (cross-site-scripting).

# Estrutura do JSX/TSX
Normalmente a estrutura se baseia em uma função que retorna  os elementos e é exportada.

```jsx
function Home() {
	return (
		<h1 className="greetings">Bem Vindo!</h1>
	)
}
export default Home;
```

# Fragment
Fragmente nada mais é do que tags vazias `<></>`, normalmente o utilizamos quando ==vamos retornar mais de um elemento em um componente React==, pois, o padrão é aceitar somente um grande elemento, quantidade de filhos não importa, porem com _fragment_ conseguimos contornar essa regra.

```jsx
function Home() {
	return (
		<>
		<h1 className="greetings">Bem Vindo!</h1>
		<button type="button">Obrigado!</button>
		</>
	)
}
export default Home;
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