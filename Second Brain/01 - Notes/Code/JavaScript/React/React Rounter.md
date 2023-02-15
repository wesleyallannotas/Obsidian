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

## Match de Rotas
Por padrão React Rounter realiza o _match_ de rotas, por exemplo um rota `/` e uma rota `/post`, quando acessarmos `/post`, obteremos como resultado o que contem dentro de `/` e de `/post`, comportamento interessantíssimo para sub-rotas, porem para a raiz não é nem um pouco interessante.
Podemos evitar esse comportamento utilizando a propriedade booleana `exact`

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
	- `path` - O primordial é o `path`, onde especificamos o caminho da nossa rota.
	- `exact` - Devolve o conteúdo apenas quando acessada exatamente, evitando [[#Match de Rotas]]
- `Switch` - Garante que somente uma rota seja renderizada por vez, ou seja, quando der _match_, renderiza a primeira e para por exemplo com `/post`, seria renderizado o `/` e pararia, para conseguir o efeito desejado seria necessário adicionar o `exact` no `/` assim não ocorrendo o `match` e chegando ate o `/post`
- `Link` - Basicamente é uma ancora que se conecta ao _Raact Router_, realiza a mudança de conteúdo sem a necessidade de outras _requests_, ou seja, não recarrega a página e todo seu HTML e conteúdo.
	- `to` - Propriedade para especificar para qual rota será enviado.

# Redirecionamento
Através do componente `Redirection` podemos criar redirecionamentos para determinadas rotas.

```tsx
<Route exact path="/">
	<Redirecton to="/production" />
</Route>
```

Muito útil quando queremos definir caminhos diferentes para o usuário dependendo do seu estado.
# Atualização 6.0
Na versão6.0 do ReactRouterDOM houveram algumas modificações em suas definições:
- `Switch` - Passou a ser chamado de Routes
- `Route` - A propriedade para renderizar elementos agora se chama `element`
Para exemplificar a utilização do “AS” renomeie o BrowserRouter para Router.
- `Redirection` - E feito através da renderização do elemento `Navigation`
	- `replace` - Para manter o histórico limpo, você deve definir replace prop. Isso evitará redirecionamentos extras depois que o usuário clicar novamente.
```tsx
<Route path="/" element={<Navigation to="/produciton" replace />} />
```