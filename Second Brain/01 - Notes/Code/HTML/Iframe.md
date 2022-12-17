---
title: Como utilizar a tag `<iframe>`
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [html]
description: Como utilizar a tag `<iframe>`, otima para reprodução de medias.
---
# Introdução
Basicamente `<iframe>` é um elemento que traz conteúdo externo, muito utilizado para trazer medias de páginas externas como Youtube, e ate mesmo na importação de mapas, em suma seu uso é extenso e com certeza nos toparemos muito durante a carreira Web

# Atributos
Em sua declaração temos a disposição vários atributos interessantes, sendo alguns deles:
- `src` - Link do conteúdo
- `height` - Altura
- `width` - Largura
- `title` - Titulo para acessibilidade
- `allowfullscreen` - *Allow* significa permitir, ou seja, estamos permitindo o *fullscreen* no nosso português tela cheia
- `frameborder` - Definimos a borda do elementos
- Também aceita [[01 - Notes/Code/HTML/Introdução#Atributos Globais|atributos globais]]

# Exemplo
É utilizada por exemplo pelo Youtube quando escolher a opção de **incorporar**, exemplo de declaração de elemento `<iframe>` tirado do Youtube
```html
<iframe 
	width="560" 
	height="315" 
	src="https://www.youtube.com/embed/tXiyQhHWBqY" 
	title="YouTube video player" 
	frameborder="0" 
	allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
	allowfullscreen>
</iframe>
```
Atributo `allow` normalmente tem como valor, "coisas", configurações que a página provedora ira entender, nesse caso o Youtube.