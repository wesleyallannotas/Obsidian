---
title: React Rounter
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [react]
description:  Trabalhando com Rotas no React
---
# Introdução
E de extrema utilidade o uso de rotas dentro de nossa aplicação, pois assim podemos gerar URLs que quando acessadas acessaram determinada página com determinado componentes carregando de tal forma, assim possibilitando o acesso direto a tal funcionalidade ou dados especifico.
Utilizaremos da biblioteca [React Router](https://reactrouter.com/en/main) para tal objetivo, sendo possível seu uso tanto na web quanto no mobile.

![[Desenho_React_ReactRounter|600]]

Utilizando as rotas podemos acessar os [[Dados via URL#Parâmetro|parâmetros]] e as [[Dados via URL#Query|pesquisas]], assim podendo carregar dentro do nosso componente, modificando o resultado que pode ser acessado via URL.

# Instalando Biblioteca
Basta instalar a biblioteca `react-rounter-dom` para utilizar o _React Rounter_ para Web.

```bash
npm install react-rounter-dom

yarn add react-rounter-dom
```

Caso esteja utilizando TypeScript é importante adicionar os tipos.

```bash
npm install -D @types/react-rounter-dom

yarn add -D @types/react-rounter-dom
```

# Estrutura Básica
Uma estrutura básica utilizando React Rounter necessita dos seguintes componentes
- `BrowserRouter` - Container que deve abraçar toda aplicação para o funcionamento do React Rounter
- `Route` - A rota em si, 
	- `parh` - a primordial é a `path`, onde especificamos o caminho da nossa rota.