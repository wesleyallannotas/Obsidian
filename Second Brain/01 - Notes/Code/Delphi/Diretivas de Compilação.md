---
title: Diretivas de Compilação no Delphi
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [delphi]
description: Diretivas de compilação, mais versatilidade para o nosso software.
---
# 🚀 Introdução
Diretivas de compilação, nos permitem a partir de uma condição definir comportamentos no nosso _software_ seja ela o valor de um _label_ ou até mesmo qual tipo de conexão utilizara.
Podem definir essas diretivas dentro do `Project > Options > Delphi Compiler > Conditional Defines`. 

# ✍️ Utilizando
Para utilizar no nosso código podemos construir uma espécie de `IF` que será interpretado pelo compilador.

>[!tip] Mais de UM
>Podemos abilitar mais de uma diretiva dentro das configurações, basta separa-las com `;`, por exemplo `FIREDAC;ZEUS`

```pascal
{$IFDEF FIRDAC}
	lbVersion.Text := 'Conectado via FireDAC';
{$ENDIF}
{$IFDEF ZEOS}
	lbVersion.Text := 'Conectado via Zeos';
{$ENDIF}
```

Muito interessante para definir quais `units` serão compiladas para evitar erros por falta de dependências 

```pascal
{$IFDEF FIREDAC}
Menus.Model.Connections.ConnectFiredac in 'Model\Connections\Menus.Model.Connections.ConnectFiredac.pas',
Menus.Model.Connections.TableFiredac in 'Model\Connections\Menus.Model.Connections.TableFiredac.pas',
{$ENDIF}
```
