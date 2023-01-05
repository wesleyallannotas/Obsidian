---
title: Introdução ao Node.js
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [javascript, node]
description: Introdução ao node.js, javascript no back-end
---
# Introdução
Node.js é um **interpretador** JavaScript (*JS Runtime Enviroment*) que utiliza o [motor V8](https://dev.to/_staticvoid/node-js-por-baixo-dos-panos-4-vamos-falar-do-v8-4pai) que é *open-source* de alta desempenho da google, podemos instalar na nossa maquina e  rodar JavaScript nativamente **sem a necessidade de um navegador**, ele é muito utilizado para desenvolvimento de Backend, Frontend, micro serviços, API, Scripts, Automação, Machine learning, entre outras.
Utilizar o Node traz algumas facilidades e vantagens, como **rápida execução** e **prototipação**, possui uma **alta escalabilidade**, **Utilização de JS** facilita para especialista do Front-End Web, Ecossistema gigante desde de comunidade a disponibilização de bibliotecas.
==Node possui [[#Event Loop]] que proporciona seu funcionamento ***singles-threaded***, ***non-blocking***, e ***Asynchronous***===
>[!Tip] Curiosidade
>No navegador tudo é armazenado dentro de um objeto global `window`, no *node* é no `process`

# Motor V8
Motor *open-source* de JavaScript e WebAssembly de alto desempenho desenvolvido pela Google, escrito em C++, possui as ultimas *features* do JavaScript, não possui [[DOM]] (*Document Object Model*), *console* ou *File System*
>[!attention] Atenção
>V8 não possui *console* nem *File System*, porem no ambiente node tem, ou seja, não é ele que proporciona essa interação diretamente.

# Event Loop
O [[#Motor V8]] junto com o Node como um todo, se comunica com uma biblioteca chamada libuv, que trabalha de forma assíncrona e conversa direto com o sistema operacional, na libuv temos o *Event Loop*, uma espécie de *loop* infinito que pega os eventos na fila (*Event Queue*) que podem bloquear a execução do código, joga para *Worker Threads*, onde quando finalizado executa o *callback* retornando a resposta da execução.

![[Desenho_JS_Node|600center]]

```js
function c() {
	setTimeout(() => {console.log('c')}, 0);
	return;
}
function b() {
	console.log('b');
	return c();
}
function a() {
 b();
 console.log('a');
 return;
}
```

Mesmo o `setTimeout()` possuindo um tempo de espera de 0 segundo, por se tratar de uma operação de bloqueio (*Blocking Operation*), ele joga para o *Worker Threads*, finaliza a execução e volta para o *Event Queue* (*callback*), assim indo para o final da fila, por isso o `c` é o ultimo valor a ser imprimido no *console*.

# Variáveis Globais
Assim como no JavaScript para navegador temos acesso ao objeto `window` que é um objeto global que guardo por exemplo nosso `document`, no Node temos o `global`, responsável por guardar o  `console`, `process` por exemplo, ou seja, são objetos globais que guardam informações e métodos importantes, como `__dirname` que guarda o caminho do diretório. ([Doc](https://devdocs.io/node~18_lts-global-objects/))

## Processo
Através do objeto global `process` obtemos os dados do processo do Node em execução, por exemplo através da *Array* `argv` podemos acessar os argumentos/parâmetros que passamos na execução, ou seja, executando Node da seguinte forma

```sh
node arquivo Wesley Silva
```

```js
console.log(process.argv);
/*
Resultado: [
	caminho-do-node,
	caminho-do-arquivo,
	'Wesley',
	'Silva'
]
*/
```

# Importando Módulos
Através da função global `require()` podemos importar modelos nativos ou externos do Node, seja criados por nós ou baixados via `npm` (*Node Package Manager*).
```js
const path = require('path');
console.log(path.basename(__filename));
```

# Criando Módulo
Através do objeto global  `module` podemos utilizar o método `exports` onde podemos atribuir o que desejarmos Array, Object, String, Number...

```js
// Arquivo que realizara a exportação
module.exports = "Testando exportação";
```

```js
const myModule = require('./path/arquivo.js');
const myModule = require('./path/arquivo'); // Pode omitir o ".js"
```
