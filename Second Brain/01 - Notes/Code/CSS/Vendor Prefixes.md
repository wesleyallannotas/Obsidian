---
title: Vendor Prefixes
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [css]
description: Funcionamento dos vendor prefixes, para ativação de funcionalidades e compatibilidade
---
# Introdução

Vendor Prefixes permite que browsers adicione `features` a fim de colocar em uso alguma novidade do CSS, também permite adicionar compatibilidade ([Doc](https://developer.mozilla.org/pt-BR/docs/Glossary/Vendor_Prefix)), por exemplo:
```css
p {
	--webkit-background-clip: text; /* Chrome, Safari, IOS e Android*/
	--moz-background-clip: text; /* Mozilla (Firefox) */
	--ms-background-clip: text; /* Internet Explorer */
	--o-background-clip: text; /* Opera */
}
```

# Descobrindo

Podemos descobrir os browser compatíveis através dos seguintes sites:

-   [http://ireade.github.io/which-vendor-prefix](http://ireade.github.io/which-vendor-prefix)
-   [http://caniuse.com](http://caniuse.com)