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

Assim criamos um projeto React que foi informado após a _flag_ `--template` (Pois o vite possui _templates_ para outras tecnologias também) utilizando o Vite, com o nome "reactapp".