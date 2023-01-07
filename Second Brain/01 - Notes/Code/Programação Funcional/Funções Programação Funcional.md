---
title: Funções na Programação Funcional
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [pf]
description: Entenda as caracteristicas das funções na programação funcional. 
---
# Introdução
Intender as diferenças e as caracteres das diferenças funções na programação funcional
- Função Independentes  (Qual a diferença da Pura?)
- Funções Puras  (Qual a diferença da independente?)
- First-class Functions
- Higher-order Functions
- Composição de Funções


# Funções Independentes
- Deverá ter ao menos 1 **argumento**, não deverá depender de nenhum dado externo
- Deverá **retornar** algo, e sempre o mesmo valor para os mesmos argumentos
- Não pode ser afetado por fatores externos
	- Dados imutáveis
	- Não guardar estados
- Não usa _loops_, caso haja necessidade deve usar recursividade.

```js
const random = (number, Math) => Math.floor(Math.random() * number);
```

Acima exercemos a ideia de **independência** onde sendo necessário a API do JavaScript `Math`, a pedimos como argumento invés de acessa-la de dentro da função.

```js
const factorial = x => {
	if (x === 0) {
		return 1;
	}
	return x * factorial(x - 1);
}
```

Para o calculo da fatorial é necessário um _loop_, pois, para calcular a fatorial de 5 é necessário realizar a operação `1 * 2 * 3 * 4 * 5`, onde para seguir a ideia de função independente usamos **recursão**, uma função chamando ela mesma.

# Funções Pura
- Não deverá depender de nenhum dado externo, apenas dos passados como argumento
- Sempre o mesmo valor para os mesmos argumentos
- Não pode ser afetado por fatores externos
	- Dados imutáveis
	- Não guardar estados
- Não terá nenhum efeito colateral no seu código

```js
const changePersonName = {person, name} => ({...person, name})
```

# First-Class Function
- Podem estar em qualquer lugar, inclusive como parâmetro de outras funções
- A função poderá ser entendi como uma variável

```js
const sayMyName = () => console.log('Wesley'); // First-Class Function
const runFunction = fn => fn();

runFunction(sayMyName)
runFunction(() => console.log('Discover'));

console.log(runFunction(Math.random))
```

Vale lembrar que por ser uma [[Funções#*Arrow Function*|Arrow Function]] de uma linha, já esta retornando o valor, mesmo com o comando `return` omitido.

# Higher-Order Function
- Funções que recebe funções como argumentos
- Funções que poderão retornar outras funções

```js
// Exemplo com .map() JS
const numbers = [2, 4, 8, 16];
const square = n => n * n;
const squaredNumber = numbers.map(square);
```

# Currying
Em português aplicação parcial de funções.

```js
const pause = wait => fn => setTimeout(fn, wait);

pause(600)(() => console.log('Waiting 600ms'))  // Executando tudo de uma vez

const wait200 = pause(200);  // Currying
const wait1000 = pause(100);  // Currying

wait200(() => console.log('waiting 200ms'));
wait1000(() => console.log('Waiting 1s'));
```

Vale lembrar que por ser uma [[Funções#*Arrow Function*|Arrow Function]] de uma linha, já esta retornando o valor, mesmo com o comando `return` omitido.
# Composição de Funções
Basicamente é um encadeamento de funções onde, uma função retorna um dado que vai para outra função, isso se repetindo quantas vezes for necessário.

```js
const people = ['Rafa', 'Diego', 'Dani', 'Rod'];
const upperCasePeopleThatStartsWithD = people
                                       .filter(person => person.startsWith('D'))
                                       .map(dperson => dperson.ToUpperCase())
```

Método de _arrays_ `filter()`, pega a _array_ e monta outra através do que for retornar pela função passada como parâmetro (_Higher-Order Function_), onde, o método de _array_ `map()` percorre essa _array_ executando executando uma função que é passada como parâmetro (_Higher-Order Function_).
Vale lembrar que por ser uma [[Funções#*Arrow Function*|Arrow Function]] de uma linha, já esta retornando o valor, mesmo com o comando `return` omitido.