---
title: CodeTemplates Delphi
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [delphi]
description: O que são as CodeTemplates no Delphi
---
# 🚀 Introdução
Basicamente são estruturas de códigos pré prontos que conseguimos chamar através de atalhos no teclado.

# 🏗️ Construindo um TemplateCode
Primeiro devemos ativar a barra de Templates que se encontra no caminho `View > Tool Windows > Templates`, em seguida seleciona o código que será adicionado ao _template_ em seguida clica no botão de criar um novo _template_ que se encontra na janela que apareceu, ira aparecer um código XML que podemos alterar algumas informações sobre o nosso _CodeTemplate_.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<codetemplate	xmlns="http://schemas.borland.com/Delphi/2005/codetemplates"
				version="1.0.0">
	<template name="" invoke="manual">
		<description>

		</description>
		<author>

		</author>
		<code language=""><![CDATA[interface

type
  TMinhaClasse = class(TInterfacedObject, IMinhaInterface)
    constructor Create;
    destructor Destroy; override;
    class function New : IMinhaInterface;
  end;

implementation

{ TMinhaClasse }

constructor TMinhaClasse.Create;
begin

end;

destructor TMinhaClasse.Destroy;
begin

  inherited;
end;

class function TMinhaClasse.New: IMinhaInterface;
begin
  Result := Self.Create;
end;]]>
		</code>
	</template>
</codetemplate>
```

Podemos alterar o atributo  `name` dentro da _tag_ `template` que desrespeito ao nome do nosso _CodeTemplate_.
Dentro das _tags_ de `description` podemos escrever uma descrição sobre o nosso _CodeTemplate_.
Podemos definir o autor dentro da _tag_ `Author`.
E Devemos informar a linguagem dentro do atributo `language` que esta na _tag_ `code`

#  ✍️ Utilizando
Para utilizar nosso _CodeTemplate_ basta que digitamos o nome que informamos no atributo `name` e acionar o atalho `CTRL + J`