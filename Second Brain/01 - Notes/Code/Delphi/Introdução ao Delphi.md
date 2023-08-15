---
title: Introdução ao Delphi
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [delphi]
description: Conhecendo o Delphi e sua estrutura base
---
# Introdução
Delphi é basicamente uma IDE/Framework desenvolvido em cima da linguagem pascal, afim de proporcionar um desenvolvimento rápido de aplicações desktop inicialmente, hoje abrangendo todo tipo de softwares.

# Estrutura 
Um documento Delphi possui varias seções, cada uma com um propósito específico

## Cabeçalho
Uma unidade Delphi, inicia com a palavra reservada `unit`, seguida com o nome da unidade, este será o nome usado para referenciar essa unidade em outras unidades dentro do `uses`

```pascal
unit MinhaUnidade;
```

## Seção Interface
Seção interface contem a clausula `uses`, onde podemos listar outras unidades sejam elas de código ou de formulários (por padrão um novo formulário vem com algumas, sendo elas as bases do Windows),
Já `interface` é onde declaramos constantes globais, tipos de dados, variáveis, procedimentos e funções que serão acessíveis por outras unidades.

```pascal
interface
uses
	Windows, Messages, ...;
const
	MinhaConstante = 42;
type
	MeuTipo = Integer;
	MinhaClasse = class
		idade : Integer;
		nome : String;
		procedure ExibeNome();
	end
var
	MinhaVariável = Integer;
	procedure MeuProcedimento;
	function MinhaFuncao(value : integer): string;
```

## Seção de Implementação
Contem o código em si da unidade, sendo o responsável por implementar procedimentos e funções declarados na interface, também é  possível declarar variáveis, constantes e tipos nesta seção que não precisam ser visíveis para outras unidades.

```pascal
implementation
uses
	OutraUnidade;
var
	VariavelLocal : Integer;

procedure MeuProcedimento;
begin
	// Implementação do procedimento
end;

function MinhaFuncao: Integer;
begin
	// Implementaçào da função
end;
```

## Seção de Inicialização e Finalização
Ambas seções são **opcionais**. A seção de inicialização é usada para inicializar dados que a unidade utiliza. A seção de finalização é usada para executar ações de limpeza quando o programa é encerrado. A seção de inicialização de cada unidade é executada na ordem em que as unidades são referenciadas. Da mesma forma, a seção de finalização é executada na ordem inversa.

Os principais pontos a serem observados sobre a seção de inicialização são:
- **Ordem de Execução:** O código na seção de inicialização é executado automaticamente antes de qualquer outra parte do programa. Isso garante que as configurações iniciais sejam feitas antes que o restante do código comece a ser executado.
- **Recursos Compartilhados:** É comum usar a seção de inicialização para alocar recursos compartilhados, como conexões de banco de dados, para que esses recursos estejam prontos para uso ao longo da execução do programa.

Principais pontos sobre a seção de finalização:
- **Ordem de Execução:** O código na seção de finalização é executado automaticamente quando o programa está sendo encerrado. Isso ocorre após o término da execução do código principal.
- **Liberar Recursos:** A seção de finalização é um local adequado para liberar recursos que foram alocados durante a execução do programa. Isso pode incluir fechar conexões de banco de dados, liberar memória alocada dinamicamente, entre outras tarefas de limpeza.  
- **Evitar Vazamentos de Recursos:** A seção de finalização é uma oportunidade de garantir que todos os recursos sejam liberados adequadamente, evitando vazamentos de memória e outros problemas relacionados a recursos não liberados.

```pascal
initialization
  // Código de inicialização

finalization
  // Código de finalização
```