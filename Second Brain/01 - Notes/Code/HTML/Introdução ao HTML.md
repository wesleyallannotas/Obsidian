---
title: Introdução 
author: Wesley Silva
url:
book:
type: note
completed: true
aliases:
tags: [html]
description: Introdução a linguagem de marcação HTML.
---
# O que é HTML
HTML é uma acrônimo para *HyperText Markup Language* (Linguagem de Marcação de Hiper Texto).
- Linguagem - Tem suas regras no jeito de escrever, Semântica, Sintaxe.
- HyperText - Textos que tem links que leva a outros textos.


# Comentários
Comentos no HTML são delimitados pelos símbolos `<!--comentario-->`, comentários só aparecem para quem esta desenvolvendo ou acessando o código fonte, independente do que for escrito dentro **não resultara impacto no funcionamento do código.** 
```html
<!--HyperText Markup Language-->


<!--
   HyperText Markup Languagea
   
   HT - HyperText
   M - Markup
   L - language
-->
```

# Anatomia das Tags
Relacionado a parte do Markup do HTML, onde é realizado por meio das tags, onde possui sua anatomia da seguinte forma:
- **Elemento** - `<div>Ola Mundo!</div>`
	- **Abertura da Tag** - `<div>`
	- **Fechamento da Tag** - `</div>`
	- **Conteúdo** - `<tag>CONTEUDO</tag>`
- **Elemento Vazio** - `<meta charset="UTF-8" />`
	- Barra no fechamento  é opcional
	
# Atributos HTML
Elementos HTML possuem atributos, tendo sua funcionalidade baseada em **conter informações extras ou configurações**, possui sua anatomia da seguinte forma:
- Nome do atributo
- Sinal de igual
- Valor/conteúdo entre aspas
	- **Atributos booleanos não precisam de conteúdo/valor**
	- Aspas é possível **omitir** porem pode causar problemas se possuir mais de atributo, **aspas simples** ou **duplas** normalmente é escolhido decorrente do texto, se usar aspas simples no texto interno utilizar duplas para delimitar o valor/conteúdo do atributo.
```html
<img src="./logo.png" alt="Logo do Site" />
<input type="text" disable />
<!--
src - Endereço do arquivo
alt - Texto alternativo
disable - Atributo Booleano
-->
```

# Atributos Globais
Atributos globais como o próprio nome sugeri, são atributos disponíveis em todas as Tags, sendo alguns deles.
- `class` - Muito utilizado para aplicar estilo CSS e localizar no JavaScript
	- `class="content"`
- `contenteditable` - Torna o conteúdo da tag editável.
	- `contenteditable="true"`
- `data-*` - Sinal de `*` informa que podemos adicionar qualquer coisa no lugar, separação por traços
	- `data-id`
- `hidden` - Atributo booleano que esconde a tag quando utilizado
- `id` - Identificação, não se repete por pagina
	- `id="cart1"`
- `style` - Aplica CSS inline
	- `style="color: red"`
- `tabindex` - Ordem da utilização do tab na pagina.
	- `tabindex="1"`
- `title` - Definir um titulo para a tag, aparece quando deixa o mouse descansando sobre o elemento

# Aninhamento de Tags
Criar relação de herança, uma tag dentro da outro.

```html
<div class="content">
	<p>
		Texto de <em>exemplo</em>
	</p>
</div>
```

A `div` que contem a classe `content` é pai da tag `p`, se atentar com o fechamento das tags, a que ==abre por ultimo fecha primeiro==, o fluxo funcionando com cada tag sendo lida na sua ordem a aparição.

# Caracteres Reservados
HTML ignora espaços em branco e quebras de linha, para mudar esse comportamento utilizamos de tags no caso da quebra de linha, e de códigos para que seja exibido o caractere deseja.
- `<br />` - Para quebra de linha (Barra opcional)
- `&npsp;` - Espaço em branco
HTML possui caracteres reservados por exemplo "`<`", caso seja necessário utilizar o mesmo no texto, será necessário utilizar um código, assim como fizemos com o espaço em branco.

## Alguns Exemplo
- `&lt;` - "<" (lower then)
- `$gt;` - ">" (greater then)
- `&amp;` - "&"
- `&quot` - """
- `&apos;` - "'"

# Anatomia do documento
Documento HTML bem escrito possui uma anatomia que deve ser seguida para manter o bom funcionamento e SEO da sua página web
- `<!DOCTYPE html>` - Identificar que estamos trabalhando com HTML 5
- `<html>` - Tags que envolve todo documento HTML, elemento root
- `<head>` - Cabeçalho do documento, não visual, guardamos metadados aqui por exemplo
- `<body>` - Corpo do documento, aqui se concentra o conteúdo que será visualizado pelo usuário

>[!note] Dica
>Utilizando `!` no VS Code o emmet cria uma documento HTML base

# Semântica
Dar significado as coisas, importante para o SEO da página web e o HTML 5 trouxe tags que possibilitando adicionar semântica ao nosso documento, assim o bom uso das mesmas facilita os usuários encontrar sua página através dos buscadores, alguns exemplos de tags semânticas `main`, `article`, `nav`, `footer`, entre outras

# Títulos e Subtítulos
Para criação de títulos e subtítulos temos as tags `h`, seguindo de ordem decrescente de importância, ou seja, a tag mais forte é a `h1`, é recomendado apenas uma tag `h1` por página web.

# Renderização
Cada navegador possuis suas peculiaridades porem em suma de forma simplificada a maioria ocorre assim.
1. O navegador carrega o HTML
2. Converte o HTML para DOM
3. O navegador realização [[HTTP#Request|requisição]] para cada item linkado ao HTML
4. O navegador analisa o [[Introdução ao CSS|CSS]] encontrado e interpreta as diferentes regras, para os diferentes seletores e buckets.
5. A árvore de renderização é organizada na estrutura e deve aparecer depois das regras de estilo serem aplicadas ao documento.
6. O visual de visualização da página é por fim mostrado na tela (este estágio é chamado de _painting_ ou pintura).

![[Desenho_HTML_Renderização|600]]

Por exemplo, Pegue o seguinte código HTML:

```html
<p>
	Let's use:
	<span>Cascading</span>
	<span>Style</span>
	<span>Sheets</span>
</p>
```

No DOM, o node (nó) especifica nosso elementro `<p>` como um elemento pai. Seus filhos são um text node e a árvore de nós que corresponde ao nossos elementos `<span>`. Os nós `SPAN` são também elementos pais, tendo os text nodes (textos dentro de si) como seus filhos:

```
P
├─ "Let's use:"
├─ SPAN
|  └─ "Cascading"
├─ SPAN
|  └─ "Style"
└─ SPAN
   └─ "Sheets"
```

# Outras Tags 

| Elemento | Função                                           |
| -------- | ------------------------------------------------ |
| `time`     | Tempo em horas                                   |
| `sup`      | Numero pequeno conectado ao top, tipo um elevado |