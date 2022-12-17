---
title: Medias com HTML
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [html] 
description: Como adicionar e manipular medias com HTML
---
# Vídeo
Podemos adicionar vídeos ao nossa HTML através da tag `<video>` com pelo menos um atributo que é obrigatório, que obviamente é o atributo que guarda o caminho do vídeo que para essa tag é o atributo `src`, outro atributo interessante é o atributo booleano `controls` que ativa os controles do vídeo. ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/Video))
```html
<video src="exemplo.mp4" controls></video>
```
Podemos perceber que a tag  `<video>` não é um elemento vazio, então fica a duvida, o que podemos adicionar como conteúdo, podemos adicionar um texto que funcionara com `fallback content` que será exibido em caso de erro na execução.
```html
<video src="exemplo.mp4" constrols>
	<p>Este browser não suporta video</p>
</video>
```
Para haver um melhor uso da tag `<video>` podemos adicionar os *sources* (`src`) de forma separada, adicionar uma ordem de prioridade, através da tag de elemento vazio `<source>`, utilizamos o atributo `type` para especificar qual tipo de arquivo é esse *source*
```html
<video controls width="600" height="500" preload="metadata">
	<source src="examplo.mp4" type="video/mp4" />
	<source src="examplo.avi" type="video/avi" />
	<p>Não rodou, se vira!</p>
</video>
```
Onde seguira a ordem de cima para baixa, parando no que funcionar.

>[!tip] Interessante
>Podemos configurar imagem de fundo ate carregar o vídeo, se o vídeo inicia mutado, autoplay e ate mesmo legendas, vale a pena consultar a [documentação no MDN](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/video)

# Áudio
Tag muito semelhante a tag  [[Medias#Vídeo|vídeo]], com a mesma ideia de ou adicionar o audio diretamente na tag `<audio>` através do atributo `src` ou utilizar tag `<source>` que abre a possibilidade de criar uma lista de prioridade, também possui a possibilidade da utilização de um `fallback content` que será exibido caso os `<source>` não funcionem, possui atributos para a tag `<audio>` semelhante a tag `<video>` como por exemplo o atributo booleano `controls` ([Doc](https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/Audio))