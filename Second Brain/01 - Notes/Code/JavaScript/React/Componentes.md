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
Normalmente é uma função (No passado se usava classes) que retorna um _React Elements_, seja por meio da notação padrão ou com o uso de extensão de sintaxe com `jsx`/`tsx`, e essa função é exportada, possuindo duas formas de exportar.

>[!tip] Retorno Direto
>Alguns projetos optam por não usar chaves quando o componente possui apenas um [[Funções#Retorno|return]] e esta utilizando sintaxe de [[Funções#Arrow Function|arrow function]]
>```tsx
>export const App = () => (
>	<div className={styles.container}>
>		<Component />
>	</div>
>);
>```

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

## Estendendo Propriedades Padrão
Quando queremos que o nosso componente mantenhas as propriedades de um elemento HTML, podemos estender nossas _props_ do componente recebendo as do elemento

```tsx
import React, { InputHMTMLAttributes } from 'react';

interface InputProps extends InputHTMLAttributes<HTMLInputElement> {
	name: string;
	label: string;
}
```

E para tratar todas as propriedades possíveis e poder adicionar ao elemento interno do nosso componente, podemos utilizar o [[Expressões e Operadores#Operador Spread|operados spread]] e o [[Funções#Parâmetro Rest|parâmetro rest]].

```tsx
const Input: React.FC<InputProps> = ({ name, label, ...rest}) => {
	return (
		<div className="input-block">
			<label htmlFor={name}</label>
			<input
				{...rest}
		</div>
	)
}
```

## children
Através da propriedade `children` que é uma propriedade reservada, podemos capturar o conteúdo de um componente, assim podendo utiliza-lo internamente, por exemplo, passando outro componente, um conteúdo de texto, entre outros.
Tudo que é passando como conteúdo para um elemento será enviado para o mesmo dentro da propriedade `children`

```tsx
<Title>Conteúdo, children</Title>
```

### Tipando
Normalmente o tipamos como um `ReactNode`, ou seja, como visto sobre a [[DOM]] e o [[DOM#Diferença entre `Node` e `Element`|Node]], aqui possui a mesma ideia, ou seja, tipando dessa forma aceitara qualquer tipo de conteúdo, podemos limitar a um especifico se desejar.

```tsx
interface ComponentProps {
	children: React.ReactNode;
}
```


# Componentes com Conteúdo
Como pode ser percebido, a maioria dos nossos componentes até o momento são [[Introdução ao HTML#Anatomia das Tags|elementos vazios]], ou seja, não possuindo conteúdo, porem podemos criar componentes que aceitam conteúdo, ou seja, elementos comuns, através da propriedade (_props_) `children`

```tsx
type ButtonProps = {
	type: string;
	children: React.ReactNode;
}

export conts Botao = ({ type, children }: ButtonProps) => {
	<button type={type}>{children}</button>
}

// ---- Utilizando Componente ---
<Botao type="submit">Adicionar</Botao>
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

>[!tip] Ultima Alternativa
>A função interna de [[Introdução ao JavaScript#Array|Arrays]] [[Manipulando Dados#map|map]] tem como uns dos possíveis parâmetros para o nossa [[Assíncronismo#Callback Function|callback]] o index do item, assim podendo ser utilizando para a `key`, porem é recomendado ter algo único de fato, pois em _arrays_ que podem ser dinâmicas pode haver troca de index a todo momento.

# Renderização Condicional
Podemos renderizar um componente através de uma condição, possuindo diversas formas te realizar a mesma.

## Ternário
Usando [[Expressões e Operadores#Operador Condicional (Ternário)|operador ternário]] para através de um [[Introdução ao JavaScript#Boolean|Boolean]] executar um ou outro, repare na utilização do [[Falsy e Truthy|operador para forçar]] a necessidade de um Booleano, passando pelo [[Falsy e Truthy]].

>[!attention] Atenção com Ternário
>Quando utilizamos ternários temos que se atentar ao fato de que quando ambos são o mesmo componente ele não ==desmonta e remonta o componente== e sim realiza as alterações, o que pode causar problemas em determinadas situações
>==Nunca aninhe ternários, pois, resultara em uma leitura difícil e pode causar problemas==

```tsx
export function Card() {
	let userName = '';

	return (
		{
			!!userName ? (<p>Nome Informado</p>) : (<p>Nome não informado</p>)
		}
	)
}
```

## Early Return
Podemos utilizar a técnica de [[Funções#Early Return|early return]] para renderização do componente.

```tsx
export function Card() {
	let userName = '';
	
	if (userName) {
		return (<p>Nome Informado</p>);
	}
	return (<p>Nome não informado</p>);
}
```

## Operadores Lógicos
Podemos utilizar dos [[Expressões e Operadores#Operadores Lógicos (Logical Operators)|operadores lógicos]] para definir uma renderização, repare na utilização do [[Falsy e Truthy|operador para forçar]] a necessidade de um Booleano, passando pelo [[Falsy e Truthy]], tal pratica pode evitar erros futuros.

```tsx
export function Card() {
    let userName = 'a';
    let comment = 'a';
    
    return (
        <>
        {!!userName && <p>Nome Informado</p>}
        {!(!userName) && <p>Nome não Informado</p>}
        {!!comment && <p>Comentario Informado</p>}
        {!(!!comment) && <p>Comentario não Informado</p>}
        {(!!userName || !!comment) && <p>Parcial ou totalmente preenchido!!</p>}
        </>
    )
}
```

```jsx
{ Object.entries(obj) > 0 && <p>Tem conteúdo</p>}
```

# Classe Condicional
Podemos adicionar classes ao nosso elemento de forma condicional, utilizando de estados, por exemplo

```tsx
<button className={`red ${selected === "red" ? "selected" : "" }`}></button>  
```

Se o estado `select` possuir o valor de `"red"`, adicionara a classe `selected`, se não não possuirá a classe.