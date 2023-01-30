---
title: Introdução ao React
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description: Conhecendo a biblioteca front-end react.
---
# Introdução
React é uma **biblioteca** JavaScript para construção de interfaces, ou seja, front-end, não é exclusivo da Web, possui um uso amplo como construção de aplicativos desktop, mobile, smartTvs, realidade virtual entre outros, _React_ trouxe como vantagens
- Reutilização
- Componentes
- Compartilhamento de Estado
	- Por exemplo o estado do seu nível de permissão no sistema, assim podendo renderizar coisas especificas para você.
- Progressive Web Applications (PWA)
	- Por exemplo acesso a câmera, microfone, localização, desenvolvimento um software completo.

# Criando Projeto
React nada mais é do que um _script_ de JavaScript, podemos adicionar o react, ou seja, seu modulo com suas funcionalidades em um projeto puro por exemplo, através do _link_ encontrado no site do React basicamente um _raw_ que cotem todo o código, caso adicionarmos o _raw_ do Babel, podemos ate escrever [[JSX e TSX|JSX]]
Porem normalmente utilizamos um _template_ base com React já configura que pode ser obtido através dos gerenciadores de pacotes JavaScript como [[NPM]],  Yarn, entre muitos outros disponíveis, entre os _templates_ mais famosos estão:
- [Create React App](https://create-react-app.dev/)
- [Vite](https://vitejs.dev/)
Entre os diversas opções ocorrem diferenças como ferramentas inclusas e performance.

```bash
npm create vite@latest reactapp --template react
```

Assim criamos um projeto React que foi informado após a _flag_ `--template` (Pois o vite possui _templates_ para outras tecnologias também) utilizando o Vite, com o nome "reactapp", sem seguida basta entrar no diretório do nosso projeto e baixar as dependências com

```bash
npm install
```

# Estrutura do Projeto
Por o React ser uma lib (biblioteca) não possui restrições como um framework como por exemplo o `Next` que é um _framework_ React que possui diversas regras para o bom funcionamento e a melhor extração de benefícios do framework, uma delas é a estrutura, de como deve ser dividido e ate mesmo o nome dos diretórios, já o React não possui.
Uma ideia de organização é deixar no `public`, os `assets`/conteúdos que vão ficar disponíveis no front-end, como por exemplo os ícones, entre outros. 
O código do projetos e dentro de `src` onde possui os códigos, criar um diretório `pages` para as páginas, um `styles` para os `CSSs` padrões que normalmente contendo um _Reset CSS_ e um CSS global do projeto.
Uma boa ideia é criar um pasta dentro de `pages` para cada pagina e dentro nomear o arquivo principal como  `index` com a extensão que estiver usando, seja puro `js`/`ts` ou com extensão de sintaxe `jsx`/`tsx` e criar um `style.css` e importar a nossa página.
Para os componentes criamos um diretório chamada `components` e usamos a mesma ideia para cada componente, criando um diretório com `index` e `style`
![[Estrutura-React.png|300]]

# Estados 
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
Para conseguirmos impactar na interface, teremos que utilizar estados que criaremos através do [[Hooks|Hook]] [[Hooks#useState|useState]], pois, ==componentes são renderizados quando o estado atualiza.==

## Imutabilidade
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

// RECOMENDADO
setStudents(prevStudent => [...prevStudent, newStudent]); // Arrow Function com Spread
// --- Conteúdo posterior mantem
```

Assim por meio do [[Expressões e Operadores#Operador Spread|operador spread]], copiamos os antigos valores contidos no estado `students` e adicionamos o novo, ou se preferir podemos utilizar uma _[[Funções#*Arrow Function*|arrow funciton]]_, pegando como parâmetro o valor antigo e criando uma nova _array_ porem ainda será necessário o _spread_ para espalhar os valores.

# Virtual DOM
Diante do fato do navegador ser mais lento, custando mais a atualização do DOM, a equipe do React teve a ideia de criar o Virtual DOM, que nada mais é do uma copia do DOM em memoria, ou seja, possuindo alta velocidade no fluxo dos dados, assim quando ocorre a alteração ela é feita no virtual DOM que notifica a atualização, onde a partir do mesmo é executado o algoritmo de conciliação para alterar somente o necessário no DOM real.