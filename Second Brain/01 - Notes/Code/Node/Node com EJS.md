---
title: Utilziando node com ejs
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags:
description: Criando páginas com node e ejs
---
# Introdução
ESJ é uma linguagem de modelagem para criação de páginas HTML usando JavaScript, ou seja, dentro do node conseguiremos criar o nosso Front-End, que será renderizado pelo JavaScript.

# Instalação
Para que o EJS funcione é necessário instalar o pacote `ejs` através do comando

```sh
npm install ejs
```

Também é necessário a instalação do `express` para criação de um servidor para mostrar tudo que esta construindo dentro do navegador

```sh
npm install express
```


# Criando Servidor
1. Será necessário criar um arquivo para ser o servidor por exemplo com o nome `server`.
2. **importaremos o modulo do `express`**  e o instanciaremos.
3. Configurar o `express` através do método `set()` para utilizar como motor para renderização do visual o `ejs`
4. Criaremos as rotas para renderizar a página com o método `get()` passando na resposta da requisição a renderização da página
5. Configurar a porta para rodar o servidor através do método `listen()`

```js
const express = required('express');
const app = express();

app.set('view engine', 'ejs');

app.get('/', (req, res) => {
	res.render('index');
});

app.listen(8080);
```

>[!attention] Atenção necessidade de diretório
>Para o funcionamento do `ejs` é necessários que os arquivos do mesmo se encontrem dentro de um diretório com o nome `views`

# Sintaxe EJS
Entre `<%-  %>` damos comandos EJS.
```ejs
<%- includes('menu'); %>
```

# Importando EJS
Podemos quebrar o nossos arquivos em pedações que julgamos que serão reutilizadas por exemplo, onde para chama-los em outro arquivo `EJS` basta utilizar o comando `includes()` passando o nome do arquivo

```ejs
<!-- Exemplo com arquivo EJS contendo todo o HEAD -->
<!DOCTYPE html>
<html lang="pt-bt">
<%- includes('head'); %>
<body>
	<h1>Exemplo</h1>
</body>
</html>
```

# Separando Arquivos
É uma pratica dentro do nosso diretório `views` que contem nossos arquivos `EJS` separa os páginas para um subdiretório chamado `pages` e as partes de layout em um subdiretório chamado `partials`

# Enviando Objeto
1. Adicionamos outro parâmetro ao includes, um objeto com os dados.
2. Trocamos o sinal após o porcento por um igual para informar que é algo enviado dinamicamente.

Exemplo com um arquivo _partial_ de nome _footer_ é uma página que inclui ele passando o objeto e outra que omiti.

```ejs
<!-- footer partial -->
<p> <%= typeof pagina != 'undefined' ? pagina : 'Home' %> </p>

<!-- Page Home onde não passará o objeto -->
<%- include('../partials/footer'); %>

<!-- Page About onde passará o objeto -->
<%- include('../partials/footer', {pagina: 'About'}); %>
```

# Enviando Dados do Back-End
Como vimos acima, EJS aceita objeto, então basta enviar junto com o `render` adicionado no servidor, outro parâmetro contendo um objeto, porem dentro do código do `EJS` deve se atender a tudo que for JavaScript, proteger com `<% %>`, tudo que for dados `<%= %>`, segui um exemplo abaixo

```ejs
    <ul>
    <% posts.forEach((post) => { %>
      <li>
        <strong><%= post.title %></strong> - <%= post.message %>
      </li>
    <% }) %>
  </ul>
```