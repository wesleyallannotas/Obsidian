---
title: Introdução ao CSS
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Introdução ao CSS para desenvolvimento Web 
---
# CSS
CSS vem do inglês *Cascading Style Sheet*,  ou seja, folha de estilo em cascata, sua ==função e estilizar o HTML==, não é considerada uma linguagem de programação e sim como o próprio nome diz *Style Sheet*

>[!note] DOM
>Compreender o DOM ajuda você organizar, debugar e manter seu CSS porque o DOM é onde seu CSS e o conteúdo do documento são combinados. Quando você começa a trabalhar com as DevTools do browser você estará navegando os elementos do DOM como itens ordenados selecionáveis para assim decidir quais regras de estilização aplicar.

# Comentários
Assim como em todo linguagem de programação ou ate mesmo no HTML, CSS tem comentários, que tem a função de auxiliar quem esta lendo o código, ele é totalmente ignorado, apenas quem tem acesso ao código pode ler.
```css
/* Comentário no CSS */
```
>[!tip] Dica
>Comentários no munda da programação é muito utilizado para desabilitar um trecho de código

# Anatomia
A anatomia do CSS se baseia na ideia de **seletor** (Quem recebera o estilo), **propriedade** (O que ira alterar), **valor** (Qual estilo será aplicado), por exemplo:
```css
h1 {
	background-color: black;
}
/*
seletor {
	propriedade: valor;
}
*/
```
- **Selector** - `h1`
- **Declaration** - `{background-color: black;}`
- **Propertie** - `background-color`
- **Value** - `black`

# Seletores
Sua função é conectar elementos com estilo CSS, possuímos alguns tipos de seletores sendo eles:
- **Global** - `*`
- **Tag/Elemento** - `h1, h2, div, p, entre outros`
- **ID** - `#container, #box`
- **Classe** - `.notificacao, .cart`
- **Attribute Selector, Pseudo-Class, Pseudo-Element, entre outros**

#  Adicionando CSS
Possuímos quatro formas de adicionar CSS sendo elas
- **Em Linha** - Adicionando CSS diretamente no elemento através do atributo global `style`, é o CSS com mais força
- **Interno** - Adicionando a tag  `<style>` no cabeçalho, onde dentro da tag podemos adicionar código CSS
- **Externo** - Adicionando a tag `<link>` com o atributo `rel` especificando ser uma folha de estilo `stylesheet` é adicionando o caminho do arquivo no atributo `href`
- **Externo (Importação)** - Importação de arquivo CSS dentro do arquivo CSS através do [[At-Rules|at-rule]] `@import`, por convenção as importações ocorrem no inicio do arquivo CSS, muito utilizado para fontes, por exemplo `@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@100&display=swap');`, é possível importar arquivos CSS internos também, **não é recomendado esse medo, pois, pode causar lentidão**

# Comportamento de Cascata
Qual caminho o browser tomo, caso haja varias regras para o mesmo estilo, o comportamento base, segui a ideia de uma ==cascata lendo de cima pra baixo e prevalecendo os estilos aplicados até o fim do documento==, ou seja, uma fonte de uma mesma `<div>` sendo alterada no inicio e no fim, valera a do fim do documento, além deste comportamento base é levado em conta 3 fatores:
1. **Origem do Estilo** - A origem do CSS define a força dele, definindo qual ira prevalecer
	- **Ordem de força** - inline > interno > externo
2. **Especificidade** - Calculo matemático, onde, cada tipo de seletor e origem de estilo, possuem valores a serem considerados.

| Valor | Seletor                                                               |
| ----- | --------------------------------------------------------------------- |
| 0     | Universal selector(`*`), Combinators e Negation Pseudo-class (`:not()`) |
| 1     | Element Type Selector (`<h1>`) e Pseudo-Elements (`::before`, `::after`)       |
| 10    | Classes (`.container`) e Attribute Selectors (`[type="radio"]`)                      |
| 100   | ID Selector (`#container`)                                                           |
| 1000  | Inline                                                                |
Possível somar valores `h1.title#my-title` pega especificamente a tag `<h1>` com a `class` "container" que possui um id "my-title", outro exemplo, `body h1` pega todos as tags `<h1>` dentro da tag `<body>`
3. **Importância** - Regra `!important` deve ser usado com muita cautela é deve ter seu uso evitado, pois, não é considerado uma boa pratica, pois, quebra o fluxo natural da cascata, ele sobrescreve qualquer estilo aplicado anteriormente, independente de origem ou especificidade

>[!warning] Importante
>O navegador por padrão já aplica alguns estilos padrões, que normalmente são retirados por arquivos CSS conhecidos como Resets CSS

# Shorthand
Shorthand ou declaração simplificada, basicamente é juntar propriedades de forma resumida, que por consequência traz maior legibilidade e facilidade na manutenção, por exemplo em fonte em vem de declarar separadamente:
```css
h1 {
	font-style: italic;
	font-weight: bold;
	font-size: .8em;
	line-height: 1.2;
	font-family: Arial, sans-serif;
}
```
Podemos utilizar shorthand simplificando a declaração
```css
h1 {
	font: italic bold .8em/1.2 Arial, sans-serif;
}
```
>[!warning] Cuidado
>Shorthand zera as declarações anteriores, levando tudo para o padrão e modificando os valores apenas os valores atribuidos, por exemplo:
>```css
>p {
>	font-weight: bold;
>	font: italic .8em/1.2 Arian, sans-serif;
>}
>```
>A declaração anterior de peso (weight), será totalmente ignorada, pois, o que o shorthand não defini ele altera para valor padrão.
>
>Outro ponto que deve se atentar e caso declare valores parecidos no mesmo shorthand, pode ocorrer conflitos, com o CSS identificando de forma incorreta, é raro, mas pode ocorrer.

# Funções
Funções também existem no CSS e tem um amplo uso desempenhando papeis importantíssimos, pois, possibilita o reaproveitamento de código, alguns exemplos de funções no CSS
```css
@import url("http://urlAqui.com/style.css")
p {
	color: rgb(255, 0, 100);
	width: calc(100% - 10px);
}
```
Segue a mesma sintaxe das linguagens de programação, o nome da função e entre parênteses os parâmetros, `calc(100% - 10px)`