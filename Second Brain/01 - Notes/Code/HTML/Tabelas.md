---
title: Tabelas
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: note
description: Como criar tabelas no HTML
---
# Introdução
Tabelas são de extrema importância para organização e exibição de dados, porem por falta de ferramentas por muito tempo teve a utilização para criar layouts de sites, porem hoje é algo ultrapassado e que pode causar problemas, tabelas possuem boa visualização de dados e uma boa acessibilidade, porem como ponto negativo traz pouca flexibilidade e a necessidade de estilização via CSS para melhorar sua visualização.

# Estrutura
A estrutura da tabela se encontra dentro de uma tag pai chamada de `<table>`, onde dentro é divida entre:
- Cabeçalho `<thead>`
- Corpo `<tbody>`
- Rodapé `<tfoot>`
Normalmente antes do `<thead>` se encontra a tag `<caption>` onde em seu conteúdo, normalmente se encontra o titulo da tabela.
Sua estrutura se baseia em:
- Linhas Valores `<tr>`
- Colunas de Cabeçalho `<th>`
- Colunas `<td>`

# Exemplo Básico
```html
    <table>
      <caption>Tabela Teste</caption>
      <thead>
        <tr>
          <th>Nome</th>
          <th>Idade</th>
          <th>Sexo</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Carlos</td>
          <td>28</td>
          <td>Masculino</td>f 
        </tr>
      </tbody>
    </table>
```


# Atributos
Através de alguns atributos específicos da tabela conseguimos mudar o seu comportamento, os mais utilizados são:
- `rowspan` - Mudamos o comportamento para quantas linhas ira ocupar.
- `colspan` - Mudamos o comportamento para quantas colunas ira ocupar.

# Técnica Agrupamento
Por consequência melhora o SEO do site, e a acessibilidade de brinde facilita a aplicação de estilos CSS. É adicionado entre o `<caption>` e o `<thead>`
- `<colgroup>` - Tag responsável por agrupar as colunas
- `<col>` - Representa cada coluna da nossa tabela
	- Atributo `span` - Informa quantas colunas a coluna ocupa, funciona como  o `colspan`, porem o nome é apenas `span`

# Definindo Escopo
Podemos definir o escopo dos cabeçalhos, definindo-os em escopo de linha ou coluna, através do atributo `scope`, ou seja, definindo como um cabeçalho da linha ou da coluna.
- `col`
- `colgroup`
- `row`
- `rowgroup`
```html
......
<tr>
	<th scope="col">Produzio</th>
</tr>
.......
<tr>
	<th scope="row">Vassoura </th>
</tr>
```
 
# Exemplo Complexo
```html
    <table>
      <caption style="background-color: gray">
        Produção e Venda por Loja
      </caption>
      <colgroup>
        <col style="background-color: gray" />
        <col span="2" style="background-color: tomato" />
        <col span="2" style="background-color: blueviolet" />
      </colgroup>
      <thead>
        <tr>
          <th rowspan="2"></th>
          <th scope="colgroup" colspan="2">Osvaldo Cruz</th>
          <th scope="colgroup" colspan="2">Salmourão</th>
        </tr>
        <tr>
          <th scope="col">Produzido</th>
          <th scope="col">Vendido</th>
          <th scope="col">Produzido</th>
          <th scope="col">Vendido</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th scope="row">Balde</th>
          <td>17</td>
          <td>10</td>
          <td>20</td>
          <td>7</td>
        </tr>
        <tr>
          <th scope="row">Vassoura</th>
          <td>10</td>
          <td>5</td>
          <td>17</td>
          <td>16</td>
        </tr>
      </tbody>
    </table>
```