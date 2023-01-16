---
title: Estados no React
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description: Entenda com funciona e como manipular estados
---
# Introdução
Quando queremos transportar valores entre componentes e queremos que cause impactando na nossa interface, variáveis comuns não tem esse poder, por exemplo.

```jsx
export function Home() {
	function handleNameChange(name) {
		console.log(name);
	}
	return (
		<input
			type="text"
			placeholder="Digite o nome..."
			onChange={e => handleNameChange(e.target.value)}
		/>
	)
}
```

No código acima criamos uma função `handleNameChange` que recebe uma propriedade `name` e a imprime no _console_, já no nosso [[Introdução ao HTML#Anatomia das Tags|elemento vazio]] `<input />`, adicionamos um evento via HTML que é executa toda vez que ocorre uma mudança `onChange`, onde passamos uma referencia de função ou função anônimas, optamos por _arrow function_ um tipo de função anônima, onde capturamos o evento através do parâmetro `e`, e pegamos o valor do _target_ que nesse caso é o `<input />`.
Seu funcionamento será perfeito, com cada caractere novo sendo digitado, todo o valor contido no `<input />` sendo impresso, então que tal adicionar esse valor a um `<h1>` por exemplo.

```jsx
export function Home() {
	let title = '';
	function handleNameChange(name) {
		title = name;
	}
	return (
		<input
			type="text"
			placeholder="Digite o nome..."
			onChange={e => handleNameChange(e.target.value)}
		/>
		<h1>{title}<h1>
	)
}
```

O valor do `<h1>` contendo `title` não será alterado a cada acionar do evento `onChange`,  isso ocorre, pois, o valor da variável esta sim sendo altera, porem não esta acontecendo nenhum nova renderização, simplesmente a variável esta sendo atualizada, mas uma variável comum não impacta na interface, seu valor e jogada na primeira renderização e pronto.
Para conseguirmos impactar na interface, teremos que utilizar estados.

# Criando Estados
O estado diferente da variável comum, influencia na renderização da página, quando seu valor é alterado, dispara uma nova renderização utilizando o algoritmo de reconciliação que percebe onde ouve mudança e altera apenas o local de forma performática.
Primeiro é necessário importar o estado da biblioteca React.

```js
import React, { useState } from 'react';
```

Agora com `useState` importado, temos que criar o nossos estado, com o nome que desejarmos.

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

# Imutabilidade
Os estados do React respeitam o conceito de [[Introdução a Programação Funcional#Imutabilidade|imutabilidade]] do paradigma [[Introdução a Programação Funcional|programação funcional]], o conteúdo não deve ser alterado e sim substituído, o que traz mais performance por consequência.

```jsx
export function Home() {
  const [studentName, setStudentName] = useState('');
  const [students, setStudents] = useState ([]);
  
  function handleAddStudent() {
    const newStudent = {
      name: studentName,
      time: new Date().toLocaleTimeString("pt-br", {
        hour: '2-digit',
        minute: '2-digit',
        second: '2-digit'
      })
    };
    setStudents([newStudent]);
  }
  
  return (
    <div className='container'>
      <h1>Lista de Presença</h1>
      <input
        type='text'
        placeholder='Digite o nome...'
        onChange={ e => setStudentName(e.target.value)}
      />
      <button type='button' onClick={handleAddStudent}>
        Adicionar
      </button>
  
      {
        students.map( student => <Card name={student.name} time={student.time}/>)
      }
    </div>
  )
}
```

>[!note] Porque dos Parênteses
>Como foi visto, quando queremos utilizar uma variável dentro da sintaxe do `JSX`, ou seja, [[JSX e TSX#Incorporando Valor|incorporar valor]] no retorno da função, temos que utilizar parênteses, neste caso utilizamos o método interno `map()` da variável.

No código acima criamos 2 estados, um guardando uma [[Introdução ao JavaScript#Array|array]] de _students_ e outro estado guardando uma [[Introdução ao JavaScript#String|string]] contendo o nome do estudando _student name_, também criamos uma função com o nome `handleAddStudent()` para adicionar o _student_ dentro da _array_ de _students_, onde a mesma grava um objeto na _array_ de _students_ contendo o valor dentro do estado `studentName` e o horário atual, realizando uma formatação.
Porem quando adicionamos vamos adicionar mais um `student`, percebemos que o anterior some, ai esta o conceito de **imutabilidade**, a _array_ anterior foi destruída e foi criado uma nova.
Para resolver esse problema ==temos que recuperar os valores anteriores, e adicionar os  novos==, podemos utilizar funções de copia, ou utilizar simplesmente o [[Expressões e Operadores#Operador Spread|operador spread]].

```js
// --- Conteudo anteior mantem ---
    setStudents([...students, newStudent]); // Operador Spread
    setStudents(prevStudent => [...prevStudent, newStudent]); // Arrow Function com Spread
// --- Conteúdo posterior mantem
```

Assim por meio do [[Expressões e Operadores#Operador Spread|operador spread]], copiamos os antigos valores contidos no estado `students` e adicionamos o novo, ou se preferir podemos utilizar uma _[[Funções#*Arrow Function*|arrow funciton]]_, pegando como parâmetro o valor antigo e criando uma nova _array_ porem ainda será necessário o _spread_ para espalhar os valores.

# Key Prop
Quando geramos [[Componentes]] através de estruturas de repetição, ou seja, dinamicamente como nesse exemplo.

```jsx
{
	students.map( student => <Card name={student.name} time={student.time}/>)
}
```

E exibido uma mensagem no _console_ pedindo para que seja especificado uma `key`, isso é importante para manter nosso React mais performático, com o algoritmo de conseguindo facilmente distinguir os componentes para realizar a atualização de forma mais rápida, a `key` tem sua ideia parecida com uma [[Projeto de Banco de Dados#Tipos Chave|chave primeira]] em um [[Introdução Banco de Dados|banco de dados]], onde seu valor deve ser único (Caso se repita exibira um erro no console).
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