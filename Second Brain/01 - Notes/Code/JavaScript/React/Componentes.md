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
Podemos definir propriedades para o nosso componente a fim de o deixar dinâmico e possibilitar o reuso, a sintaxe é igual de atributos no HTML `propriedade="valor"`

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

# Adicionando Eventos
Podemos adicionar eventos ano nosso componente de diferentes forma, seja internamente criando a função dentro do arquivo do componente, ou ate mesmo externamente, recebendo como [[#Propriedades]] e utilizando dentro do componente.

```jsx
export function ButtonInterno() {
  function showMessage() {
    window.alert('clicou!')
  }
  
  return (
    <button onClick={showMessage}>Clique!</button>
 )
}
  
export function ButtonProp(props: ButtonProps) {
  return (
    <button onClick={props.click}>Clique aqui!</button>
  )
}
```

# Key Prop
Quando geramos [[Componentes]] através de estruturas de repetição, ou seja, dinamicamente como nesse exemplo.

```jsx
{
	students.map( student => <Card name={student.name} time={student.time}/>)
}
```

E exibido uma mensagem no _console_ pedindo para que seja especificado uma `key`, isso é importante para manter nosso React mais performático, com o algoritmo do React conseguindo facilmente distinguir os componentes para realizar a atualização de forma mais rápida, a `key` tem sua ideia parecida com uma [[Projeto de Banco de Dados#Tipos Chave|chave primeira]] em um [[Introdução Banco de Dados|banco de dados]], onde seu valor deve ser único (Caso se repita exibira um erro no console).
Criamos a `key` por meio do atributo `key`, ficando da seguinte forma.

```jsx
{
	students.map( student => (
		<Card 
			key={student.time}
			name={student.name} 
			time={student.time}
		/>
	)
}
```

Não é obrigatório essa formatação, a utilizei para uma melhor visualização, criei a propriedade `key` e como valor escolhi usar o `time` contido dentro do `student`, ou seja, caso demore pelo menos um segundo entre uma adição e outra não terá problema, pois, esse time for formatado para conter, `HH:MM:SS`.