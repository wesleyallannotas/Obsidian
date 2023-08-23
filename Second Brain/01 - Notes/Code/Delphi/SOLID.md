---
title: SOLID com Delphi
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [delphi]
description: Aplicando SOLID com delphi.
---
# 🚀 Introdução
SOLID é um acrônimo com cinco princípios que utilizamos no nosso código para seguir as boas praticas e manter um código limpo orientado a objetos, sendo esses princípios.
1. Princípio da Responsabilidade Única - **SRP**
2. Princípio do aberto e Fechado - **OCP**
3. Princípio de Substituição de Liskov - **LSP**
4. Princípio de Segregação de interfaces - **ISP**
5. Princípio da inversão de Dependência -- **DIP**Titulo

# 🧩 SRP - Princípio da Responsabilidade Única
O princípio da responsabilidade única se baseia na ideia de possuir um baixo acoplamento e uma alta coesão assim resultando em uma alta possiblidade de reuso de código, e uma facilitação na hora de manutenção, assim não sendo necessário o uso do conhecido `CTRL + F`, pois, alterações se propagarem naturalmente sem a necessidade de alteração em vários pontos diferentes onde muitas vezes nem se sabe onde é.

```pascal
procedure TVenda.Venda;
begin
	AdicionaProduto(StrToInt(Edit1.Text));
	CalcularTotal;
	EnviarEmail;
end;
```

Esse exemplo acima é um exemplo de classe não coesa, pois a mesma realiza diferentes funções assim não seguindo o conceito de responsabilidade única, por exemplo a classe de venda enviando e-mail, faz sentido adicionar produto e calcular o total, porem o envio de e-mail já foge de sua reponsabilidade.
Métodos de classes distantes não devem ao mínimo se entrelaçar, pois essa pratica aumenta o acoplamento.

# 🧩 OCP - Aberto e Fechado
Basicamente diz que nosso código deve ser aberto a extensões e fechado para modificações, por exemplo.

```pascal
interface
	type
		TArquivo = class
			procedure GerarWord;
			procedure GerarPDF;
			procedure GerarXML;
			procedure GerarArquivos(Tipo : string);
		end;

implementation
procedure TArquivo.GerarArquivo(Tipo : string);
begin
	if Tipo = 'Word' then
		GerarWord
	else if Tipo = 'PDF' then
		GerarPDF;
	else if Tipo = 'XML' then
		GerarXML;
end;
```

Aplicando o conceito de aberto para extensões e fechado para modificações, basicamente a nossa função de `GerarArquivos` tem que ser fechada para modificações, ou seja, independente se for adicionado ou removo tipos de arquivos ela deve funcionar, e nossa classe tem que ser aberta pra extensões no sentido que deve ser possível adicionar novos tipos de arquivos.

```pascal
interface
	type
		TArquivo = class
			procedure GerarArquivo; virtual; abstract;
		end;
		
		TArquivoWord = class(TArquivo)
			procedure GerarArquivo; override;
		end;
		
		TArquivoPDF = class(TArquivo)
			procedure GerarArquivo; override;
		end;
		
		TArquivoXML = class(TArquivo)
			procedure GerarArquivo; override;
		end;
		
		TArquivoTXT = class(TArquivo)
			procedure GerarArquivo; override;
		end;

implementation
procedure TForm.ButtonCLick(Sender : TObject);
var
	Arquivo : TArquivoWord;
begin
	Arquivo := TArquivoWord.Create;
	try
		Arquivo.GerarArquivo;
	finally
		Arquivo.Free;
end;
```

Como exemplo até simulei a adição de mais um tipo de arquivo, sendo ele o TXT, ou seja, utilizamos herança e abstração,  criando uma classe para os arquivos onde possui um método abstrato que é implementado pelos filhos que são os tipos de arquivos.

# 🧩 LSP - Princípio de Substituição Liskov
Toda classe filha tem que ser substituído por sua classe pai sem que seu funcionamento mude.
Por exemplo nossa solução no principio anterior erra nisso, pois, a classe pai tem seu método abstrato, assim não possuindo código e sendo implementada pelas classes filhas, vamos corrigi-lo

```pascal
interface
	type
		IArquivo = interface
			// CTRL + G
			procedure GerarArquivo;
		end;
		
		TArquivoTXT = class(TInterfaceObject, IArquivo)
			procedure GerarArquivo;
		end;
		
		TArquivoWord = class(TArquivoTXT)
			procedure GerarArquivo;
		end;
		
		TArquivoPDF = class(TArquivoTXT)
			procedure GerarArquivo;
		end;
		
		TArquivoXML = class(TArquivoTXT)
			procedure GerarArquivo;
		end;

implementation
procedure TForm.ButtonCLick(Sender : TObject);
var
	Arquivo : IArquivo;
begin
	Arquivo := TArquivoWord.Create;
	// Arquivo := TArquivoTXT.Create;
	Arquivo.GerarArquivo;
end;
```

Criamos uma interface, implementamos a mesma em uma classe, a escolhida foi `TArquivoTXT`, onde os outros tipos de arquivos descendem dela, assim conseguimos a qualquer momento em sua implementação alterar para a classe pai e ter seu funcionamento igual.
Como vantagem conseguimos trabalhar com teste unitários testando as superclasses assim possuindo um resultado igual.

# 🧩 ISP - Princípio da Segregação de Interfaces
É quando utilizamos classes altamente genéricas e ou que exijam implementações que não são pertinentes a nossa classe, assim por consequência acumulando lixo no nosso código e até ocorrendo problemas maiores, como por exemplo a adição de novas parâmetros para um método que pode resultar em alteração em classes que não a utilizam.

```pascal
type
	IFutebol = interface
		procedure Treinartime;
		procedure OrganizarTatica;
		procedure jogar;
	end;

	TComissaoTecnica = class(TInterfaceObject, IFutebol)
	begin
		procedure Treinartime;
		procedure OrganizarTatica;
		procedure jogar;
	end;
	
	TTreinador = class(TInterfaceObject, IFutebol)
	begin
		procedure Treinartime;
		procedure OrganizarTatica;
		procedure jogar;
	end;
	
	TJogador = class(TInterfaceObject, IFutebol)
	begin
		procedure Treinartime;
		procedure OrganizarTatica;
		procedure jogar;
	end;
```

`IFutebol` uma classe genérica que implementa diversos métodos, onde por sua vez a implementamos em classes que não utilizam todos esses métodos, por exemplo a classe `TJogador` que desrespeito ao jogador, qual a necessidade de ele ter um método de `OrganizarTatica`, ou seja, acumula lixo no código, e se futuramente esse método necessita de uma parâmetros especifica, será necessário atualizar esse método que ele nem utiliza,

Para corrigir, basta separar em interfaces especificar que atende cada classe.

```pascal
type
	IJogador = interface
		procedure Jogar;
	end;
	
	IComissaoTecnica = interface
		procedure TreinarTime;
	end;

	ITreinador = interface
		procedure Organizartatica;
	end;
```

# 🧩 DIP - Princípio da Inversão de Dependências
Define que ==classes maiores não devem depender de classes menores,== ambas devem depender de _interfaces_,  as ==abstrações não devem depender dos detalhes que estão implícitos ali dentro, e sim os detalhes depender da abstração.==

```pascal
interface
	type
		TLampada = class
			procedure Ligas;
			procedure Desligar;
		end;
		
		TBotao = class
			Lampada : TLambada;
			constructor Create;
			procedure Acionar;
		end;

implementation
	constructor TBotao.Create;
	begin
		Lampada := TLampada.Create;
	end;
```

Por exemplo esse botão precisa conhecer a lâmpada, e ele só servi para ligar a lâmpada, e se precisássemos de um botão para ligar um ventilador? não conseguiríamos utilizar o mesmo, pois, ele esta atrelado, acoplado a lâmpada.
Em vez disso vamos programa-lo para ligar um dispositivo, que tenha os métodos ligar e desligar.

```pascal
interface
	type
		IDispositivo = interface
			// CTRL + G
			procedure Ligar;
			procedure Desligar;
		end;
	
		TLampada = class(TInterfaceObejct, IDispositivo)
				procedure Ligas;
				procedure Desligar;
			end;
		
		TBotao = class
			FDispositivo : IDispositivo;
			constructor Create(Dispositivo : IDispositivo);
			procedure Acionar;
		end;

implementation
constructor TBotao.Create(Dispositivo : IDispositivo);
begin
	FDispositivo := Dispositivo;
end;

procedure TBotao.Acionar;
begin
	FDispositivo.Ligar;
end;
```

Perceba como invertemos a dependência, e agora nossa classe `TBotao`, recebe uma classe que implemente a interface `IDispositivo`, assim invertendo sua dependência, o seja, ==abstrações não podem depender de detalhes, mas o detalhes dependem das abstrações==, não imputamos a dependência dentro da nossa classe, criamos uma _interface_ para abstrair.