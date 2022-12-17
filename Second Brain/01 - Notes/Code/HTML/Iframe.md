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
Basicamente `<iframe>` é um elemento que traz conteúdo externo, é usada para inserir um frame dentro de uma página web. Um frame é uma área na página que pode exibir outro documento, como uma página web ou um arquivo de imagem, muito utilizado para trazer medias de páginas externas como Youtube, e ate mesmo na importação de mapas, em suma seu uso é extenso e com certeza nos toparemos muito durante a carreira Web ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/iframe))

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

>[! warning] Cuidado
>A tag `iframe` é útil quando você deseja incorporar conteúdo de outro site em sua página, mas é importante lembrar que isso pode afetar a segurança e a privacidade dos usuários, pois o conteúdo do frame pode ser controlado por outra pessoa. Por isso, é importante usar com cuidado e sempre considerar as possíveis implicações de segurança e privacidade.