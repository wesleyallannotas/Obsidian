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
React é uma **biblioteca** JavaScript para construção de interfaces, ou seja, front-end, não é exclusivo da Web, possui um uso amplo como construção de aplicativos desktop, mobile, smartTvs, realidade virtual entre outros.

# Criando Projeto
Normalmente utilizamos um _template_ base com React já configura que pode ser obtido através dos gerenciadores de pacotes JavaScript como [[NPM]],  Yarn, entre muitos outros disponíveis, entre os _templates_ mais famosos estão:
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
Uma ideia de organização de projetos e dentro de `src` onde possui os códigos, criar um diretório `pages` para as páginas, um `styles` para os `CSSs` padrões que normalmente contendo um _Reset CSS_ e um CSS global do projeto.
Uma boa ideia é criar um pasta dentro de `pages` para cada pagina e dentro nomear o arquivo principal como  `index` com a extensão que estiver usando, seja puro `js`/`ts` ou com extensão de sintaxe `jsx`/`tsx` e criar um `style.css` e importar a nossa página.
Para os componentes criamos um diretório chamada `components` e usamos a mesma ideia para cada componente, criando um diretório com `index` e `style`

