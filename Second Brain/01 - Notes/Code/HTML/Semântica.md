---
title: Adicionando Semântica
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [html]
description: Adicionando semântica para nossa Web Page 
---
# Introdução
Semântica foi adicionada no HTML5, tendo como objetivo facilitar o SEO, ou seja, os buscadores indexar de forma mais eficiente os sites e trazendo até uma melhor leitura do documento HTML, facilitando a identificação e a função de cada elemento em suma dar significado ao conteúdo.

# Seções Comuns em Documentos HTML
Existem diversos elementos semânticos hoje em dia, porem nem todos usaremos em todas as páginas, porem alguns sempre marcaram presença, obviamente adequando sua posição ao nosso layout.
- **Cabeçalho** - `<header>`
- **Navegação** - `<nav>`
- **Conteúdo Principal** - `<main>`
- **Barra Lateral** - `<aside>`
- **rodapé** - `<footer>`

# Header
*Header* em tradução livre para o português é cabeçalho, quando usado ==no início da página é visto como o cabeçalho global==, porem também tem seu ==uso dentro de elementos como `article`, `section`==, ou seja, é comum até existir múltiplos elementos `<header>` dentro de uma página, ele não possui atributos específicos.

>[!fail] Não faça
>- `<header>` dentro de `<header>`
>- `<header>` dentro de `<footer>`

# Nav
O elemento `<nav>` é utilizado na navegação da página, ou seja, no menu, utilizamos o elemento `<nav>` para navegações importante, pode existir mais de um, mas deve ser bem pensado, não possui atributos específicos.

# Main
O elemento `<main>` é utilizado para abrigar o conteúdo principal da página, **existindo apenas um por página, e tendo como elemento pai o `<body>`**, não possuí atributo específico.

```html
<body>
    <main>
        <h1>Receitas</h1>
        <p>Essa é uma página de receitas</p>
        <article>
            <h2>Receita de torta de maçã</h2>
            <p>Essa é uma receita de torta de maçã</p>
        </article>
        <article>
            <h2>Receita de torta de limão</h2>
            <p>Essa é uma receita de torta de maçã</p>
        </article>
    </main>
</body>
```

# Article
*Article* em tradução livre para o português artigo, é utilizado quando contem bloco de conteúdo relacionado como no exemplo acima onde todo são receitas, normalmente se repete varias vezes na página e **seu conteúdo deve ser dependendo o documento HTML**, ou seja, se retirarmos o conteúdo do elemento `<article>` e colar em outro lugar, deve ser entendido por completo, também não possui atributos específicos.

# Aside
O elemento `<aside>` tem como função descrever o conteúdo principal da página, por exemplo **explicações, glossários, links extras, biografia do autor, informações de perfil**, também não possui atributos específicos, normalmente é posicionado em uma barra lateral, porem não é uma regra.

# Footer
O elemento `<footer>` traduzido para o português é rodapé, assim trazendo a função de informações do autor, copyright, contrato, sitemap, voltar ao topo, entre outras ideais, também não possui atributos específicos, normalmente se encontra no final da página

# Section
O elemento `<section>` traduzido para o português é seção, normalmente traz um titulo e um conteúdo, uma ideia seria uma seção dentro dos `<article>` de receitas exemplificado acima mostrando o modo de preparo, não possui atributos específicos.

# Ênfase e Importância
Estou _feliz_ que você não chegou _atrasado_.

```html
<p>Estou <em>felix</em> que você nào chegou <em>atrasado</em>.<p>
```

Estou **feliz** que você não chegou **atrasado**.

```html
<p>Estou <strong>felix</strong> que você nào chegou <strong>atrasado</strong>.<p>
```

A primeira frase parece genuinamente aliviada de que a pessoa não estava atrasada. Em contraste, a segunda parece ser sarcástica ou passiva-agressiva, expressando aborrecimento que a pessoa chegou um pouco atrasada, exemplos de bom uso de importância

Este líquido é **altamente tóxico**.

```html
<p>Este líquido é <strong>altamente tóxico</strong>.</p>
```

Eu estou contando com você. **Não** se atrase!

```html
<p>Eu estou contrando com você. <strong>Não</strong> se atrase!</o>
```

## Mesmo resultado, significo diferente
-   [`<i>`](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/i) é usado para transmitir um significado tradicionalmente transmitido por itálico: palavras estrangeiras, designação taxonômica, termos técnicos, um pensamento...
-   [`<b>`](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/b) é usado para transmitir um significado tradicionalmente transmitido por negrito: palavras-chave, nomes de produtos, sentença principal...
-   [`<u>` (en-US)](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/u "Currently only available in English (US)") é usado para transmitir um significado tradicionalmente transmitido pelo sublinhado: nome próprio, erro de ortografia...