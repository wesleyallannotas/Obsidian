---
title: Como criar formularios no HTML
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [html]
description: Como criar formularios e suas configurações
---
# Introdução
Através do elemento `<form>` podemos criar formulários que tem com objetivo capturar dados,  basicamente estão lá quando ocorre a interação com o usuário, por exemplo, em uma calculadora na página, por se tratar de formulário traz consigo alguns atributos únicos sendo os mais necessários `action` e `method`

>[!fail] Não Faça
>Não crie um `<form>` dentro de outro `<form>`, além de totalmente errado, não faz nenhum sentido

## Envio
Através do atributo `action` podemos definir para onde o formulário será submetido, caso deixe vazio será enviado para a mesma página

## Método
Através do atributo `method` podemos definir o método do envio do formulário sendo os mais conhecidos e utilizados `post` e `get`
- `get` é enviado pela URL
- `post` é enviado internamente

# Agrupando Informações
Através do elemento `<fieldset>` podemos agrupar campos que possuem o mesmo proposito trazendo mais semântica e acessibilidade para nosso página Web, além disso conseguimos atributos e elementos que trazer maior controle ao nosso formulário
- **Atributo** `disabled` - Desabilita todos os elementos internos, não sendo enviados as submeter o formulário.
- **Atributo** `form` - Adicionamos o `id` do formulário a qual o `<fieldset>` pertence, assim não tornando obrigatório o mesmo se encontrar dentro do elemento `<form>`.
- **Atributo** `name` - Nome dado ao grupo.
- **Elemento** `<legend>` - Nome do agrupamento agora visual, recomenda-se ser o primeiro elemento do elemento `<fieldset>`.
```html
<form id="cadastro" action="" method="post">
	<fieldset form="cadastro" name="input-contact">
		<legend>Contato</legend>
		<label for="email">E-mail</label>
		<input type="email" id="email" />
	</fieldset>
</form>
```

# Rotulo
Através do elemento `<label>` podemos identificar/rotular nossos elementos de entrada de dados, os ligando através do atributo `for` onde como valor colocaremos o `id` do elemento de entrada de dado, caso ligado corretamente, clicando no `<label>` e redirecionado para a entrada de dado conectada.
```html
<label for="email">E-Mail</label>
<input type="email" id="email" />
```

# Botões
Através do elemento `<button>` podemos criar botões, que podemos utilizar para varias funções como até mesmo enviar formulários, por padrão é estilizado pelo *user agent*

## Atributos Comuns
O elemento `<button>` possui alguns atributos interessante e que com certeza usaremos muito, sendo alguns deles:
- `type`
	- `submit` - Envia o formulário
	- `reset` - Reseta o formulário, caso a entrada de dados possui um atributo `value` voltar para esse valor, caso não tenha o campo ficara limpo
	- `button` - Alguns navegadores entendem como `submit`, recomendado o uso de `submit`
- `autofocus`
- `disabled` - Desabilita o campo, impossibilitando o acionamento
- `name`, `value` - Utilizando os dois em conjunto podemos enviar um valor no acionamento do botão
- `form` - Ligamos o formulário ao botão

```html
<form id="cadastro" action="" method="post">
	<fieldset form="cadastro" name="input-contact">
		<legend>Contato</legend>
		<label for="email">E-mail</label>
		<input type="email" id="email" />
	</fieldset>
	<button form="cadastro" type="submit">Enviar</button>
</form>
```

# Sugestão
Através do elemento `<datalist>` podemos criar uma lista de sugestões adicionando cada sugestão dentro do elemento `<option>` onde podemos conecta-las a uma elemento `<input>` através do atributo `list`, vale ressaltar são sugestões e não valores obrigatórios.
```html
<datalist id="fruitsdata">
	<option>Apple</option>
	<option>Banana</option>
	<option>Mango</option>
	<option>Orange</option>
	<option>Cherry</option>
</datalist>
```
Extrema importância conter o atributo `id`, pois é através dele que conectaremos ao elemento `<input>` utilizando o atributo `list`
```html
<datalist id="cores">
	<option>#ff0000</option>
	<option>#212021</option>
</datalist>
<input type="color" list="cores" />
```
Se o valor do elemento `<option>` não ser aceito pelo tipo do elemento `<input>` ele nem aparecerá como opção

# Entrada de Dados com `<input />`
Um dos elementos vazios mais utilizados em formulário `<input />`, aceita diversos tipos de dados os diferenciando através do atributo `type`.

## Atributos Comuns
O elemento vazio `<input />` é complexo e muito poderoso, existem algumas atributos que são mais utilizados, sendo eles
- `type` - Definimos o tipo de dados aceito pelo `<input />`
- `name` - Uma espécie de titulo/identificação do nosso `<input />`
- `id` - [[01 - Notes/Code/HTML/Introdução#Atributos Globais|atributo global]], que aqui ganha ainda mais força
- `autocomplete` - Possuímos diversas possiblidades de valor para esse atributo, em suma podemos definir de onde pegar valores para servirem de *autocomplete*
- `autofocus` - Será focado após o carregamento da página, atributo booleano que por boa pratica só deve haver um por página
- `disabled` - Desabilita, atributo booleano
- `readonly` - Mantem a aparência normal, porem só pode ser lido, não havendo a possibilidade de editar o conteúdo
- `form` - Conecta o `<input />` ao formulário
	- Quanto o `<input />` se encontra fora do formulário e de extrema importância que contenha o atributo `name` para identificar o dado que esta sendo enviado
- `required` - Atributo booleano que torna o campo obrigatório
- `placeholder` - Valor passado fica dentro ate algo ser escrito, servi para passar informação para o usuário, como por exemplo "Digite sua senha"
	- Não trocar `<label>` por `placeholder`
- `title` - Muito interessante, pois, quando o usuário errar, ele mostra esse texto
- `inputmode` - Poderá altera o tipo de teclado em smartphones
	- Exemplo `inputmode="numeric"`
- `minlength / maxlength` - Número mínimo e máximo de caractere
- `size` - O número aceitado de caracteres
- `patter` - *Regex* (Expressões regulares) para validação
- `muiltiple` - Aceita um ou mais valores separados por virgula
- `spellcheck` - habilita corretor ortográfico para o `<input />`
- `arial-label` - Opção quando não temos o elemento `<label>`, não é visível mas traz a semantica 

>[!warning] Atençào
Nem todo **tipo** de `<input />` aceita todas atributos, vale consultar a documentação

## Tipos
O elemento vazio `<input />` e muito poderoso e possui uma grande flexibilidade que é manipulada através do atributo `type`, onde ==dependendo do tipo escolhido podemos controlar melhor com determinados atributos em conjunto==

### Senha
Adicionando o valor `password` ao atributo `type` temos nosso elemento `<input />` se transformando em uma entrada de senha, trocando o caractere digitado para esconder a senha em conjunto podemos usar alguns atributos interessante:
- `pattern` - Dentro desse atributo podemos adicionar uma expressão regular que validara o campo
	- Exemplo `pattern="{0-9a-fA-F}{4,8}"`, aceitamos valores hexadecimal maiúsculo e minúsculo que tenha entre de 4 a 8 caracteres
- `autocomplete` - Para senhas possui algumas funcionalidades interessante
	- `on` - Permite sugestão consecutivamente de `current-password` e `new-password`
	- `off` - Desabilita auto completar
	- `new-password` - O navegador poderá sugerir uma nova senha

### Arquivo
Adicionando o valor `file` ao atributo `type` temos nosso elemento `<input />` se transformando em uma entrada de um ou mais arquivos para enviar ao servidor
- `accept` - Que tipos de arquivos serão aceitos
	- `accept="image/*"` Aceita todo tipo de imagens
	- `aceept=".png, .jpg"`
	- Podemos separar por virgula, ou tipo barra extensão do arquivo
- `files` - Lista dos arquivos enviados
- `multiple` - Permite mais de um, atributo booleano
Para funcionar o envio de arquivo o nosso elemento `<form>` tem que ser `method="post"` e também `enctype="multipart/form-data"`

### Checkbox
Adicionando o valor `checkboc` ao atributo `type` temos nosso elemento `<input />` se transformando em um *checkbox*.
- `checked` - Atributo booleano que caso utilizado traz o `<input />` marcado como padrão

>[!attention] Atenção
>Por padrão quando **não marcado** não há valor enviado para o servidor ele vai vazio, quando **marcado** é enviado o valor `on`, podemos alterar esse valor quando marcado através do atributo `value`

```html
<label for="noticias">Aceitar receber noticias<label>
<input id="noticias" type="checkbox" name="noticias" value="notificar" checked />
```

#### Múltiplos Valores
Para possibilitar selecionar mais de um valor para a mesma resposta, basta utilizar o mesmo `name`, por exemplo
```html
<fieldset>
	<legend>Escolha os seus interesses</legend>
	<div>
		<input type="checkbox" id="coding" name="interesses" value="coding" />
		<label for="coding">Coding</label>
	</div>
	<div>
		<input type="checkbox" id="music" name="interesses" value="music" />
		<label for="Music">Music</label>
	</div>
</fieldset>
```

### Hidden
Em tradução livre significa escondido e assim será para o visual e até para leitores de tela, é interessante, pois, através deles podemos enviar dados junto com o formulário que não precisa da interação com o usuário
```html
<input type="hidden" name="date" value="19/12/2022" />
```
Normalmente o `value` que é o valor a ser enviado para o identificador encontrado no `name` é alterado pelo `JavaScript`

### Radio
Adicionando o valor `radio` para o atributo `type` no elemento vazio `<input />`, criamos um input do tipo *radio* que em sua essência a ideia de possuir **apenas um selecionado por formulário** muito útil para selecionar o sexo por exemplo:
```html
<fieldset>
	<legend>Sexo:</legend>
	<input type="radio" id="masculino" name="sexo" value="masculino" checked/>
	<label for="masculino">Masculino</label>
	<br />
	<input type="radio" id="feminino" name="sexo" value="feminino" />
	<label for="feminino">Feminino</label>
	<br />
</fieldset>
```

### Pesquisa
Através do valor `search` para o atributo `type` no elemento vazio `<input />` podemos definir o nosso campo como de pesquisa, podendo alterar sua aparência dependendo do *user agent*.
Muito utilizado em conjunto o atributo `list` ligando com um elemento `<datalist>` através do *id*
- `arial-label` - Opção quando não temos o elemento `<label>`, não é visível mas traz a semântica 
- `pattern` - Muito utilizado quando é um campo de pesquisa especifico e utilizaremos expressão regular
```html
<datalist id="sistemas">
	<option>Windows</option>
	<option>iOS</option>
	<option>Linux</option>
</datalist>
<form action="" method="get">
	<input type="search" name="pesquisa" list="sistemas" id="pesquisa"
	placeholder="Digite o termo de pesquisa"
	aria-label="Campo de pesquisa"
	size="28">
	<button>Pesquisar</button>
</form>
```

### Número
Através do valor `number` para o atributo `type` no elemento vazio `<input />` podemos definir o nosso campo como de entrada de números, onde ==Não será aceito letras, apenas números==, trazendo com sigo alguns atributos interessantes como:
- `min` e `max` - Definindo o valor mínimo e máximo de entrada que é aceito
- `step` - Definimos de quanto em quanto ira aumentar o valor
```html
<label for="input-weight">Peso (KG)</label>
<input id="input-weight" type="number" min="1" step="0.1" name="weight" />
```

>[!tip]- Removendo Click
>Podemos remover as "Flechas" responsáveis por aumentar e diminuir o valor através do clique, utilizando a seguinte técnica  ([Link](https://stackoverflow.com/questions/26024771/styling-a-input-type-number)), você pode utilizar a propriedade [-moz-appearance](https://developer.mozilla.org/en-US/docs/Web/CSS/appearance), a qual é utilizada para exibir um elemento usando o estilo nativo da plataforma com base no tema do sistema operacional.
>
>```css
>input[type=number]::-webkit-inner-spin-button { 
>    -webkit-appearance: none;   
>}
>nput[type=number] { 
>   -moz-appearance: textfield;
>   appearance: textfield;
}
>```
> 
>```html
><input type="number" />
>```

### Data
Através do valor `date` para o atributo `type` no elemento vazio `<input />` podemos definir o nosso campo como entrada de data, onde o formato do nosso atributo `value` **yyyy-mm-dd**
```html
<input type="date" value="2022-12-20" name="date" />
```
Utilizando como valor para o atributo `type` o valor `datetime-local` também é possível selecionar o horário
Com `month` seleciona mês e ano, `week` semana e com `time` apenas o horário.

# Entrada de Dados com `<textarea>`
O elemento `<textarea>` é muito útil para entrada de dados com textos grandes, possuindo muitos **atributos interessantes para o controle** deste elemento, assim como no elemento vazio `<input />` ele aceita o elemento `<label>` ligado pelo atributo `for`

## Atributos Comuns
-  **Atributo** `name` - Funciona da mesma forma do `<input />` ele vai como identificador do conteúdo do campo
- **Atributos** `rows` e `cols` - Definem o tamanho deste `<textarea>`
- **Atributos** `maxlength` e `minlength` - Controla os tamanhos de conteúdo aceito
- **Atributo** `wrap` - Controla quebra de linha, caso desabilitando passando o valor `off` ele cria um *scroll* horizontal em vez de quebrara a linha
- Entre outros diversos atributos encontrados para o [[Formulário#Entrada de Dados com `<input />`|input]]

>[!attention] Atenção
>Caso deixe espaço em branco entre a abertura e fechamento do elemento `<textarea>` o cursos pode mudar o posicionamento de inicio.

```html
<label for="descricao">Descrição</label> 
<textarea id="descricao" rows="3" cols="30" maxlength="250"></textarea>
```

# Entrada de Dados com `<select>`
O elemento `<select>` criar uma caixa de seleção também conhecida como *combobox* que traz opções para o campo, diferente da lista de sugestões, o `<select>` traz opções onde uma deles tem que ser escolhida, onde informamos as opções através do elemento `<option>`.
Basicamente o que colocamos de conteúdo no `<option>` é uma espécie de visual, o que realmente é mandado para o servidor é o valor que atribuirmos no atributo `value` do elemento `<option>`.
Assim sendo podemos concluir que o atributo `name` do elemento `<select>` é o identificador, e o atributo `value` do elemento `<option>` é o valor.
```html
<label for="fruta">Fruta preferida</label>
<select name="fruta" id="fruta">
	<option value="apple">Maça<option>
	<option value="pineaple">Abacaxi<option>
</select>
```
Adicionando o atributo booleano `multiple` ao elemento `<select>` abre a possibilidade de selecionar mais de um, mudando o formado deixando de ser um *combobox* padrão, utilizando o atributo `size` em conjunto podemos definir quantas opções iram aparecer, caso tenha mais que o valor atribuído criara um *scroll*

## Grupo de Opções
Através do elemento `<optgroup>` podemos criar grupos de opções, através do atributo `label` podemos deixar uma identificação que será visual
```html
<label for="pets">Please choose one or more pets:</label>
<select name="pets" id="pets" multiple size="8">
	<optgroup label="mamiferos">
		<option value="dog">Dog</option>
		<option value="cat">Cat</option>
		<option value="monkey" disabled>Monkey</option>
	</optgroup>
	<optgroup label="reptil">
		<option value="snake">Snake</option>
		<option value="lizard">Lizard</option>
	</optgroup>
</select>
```