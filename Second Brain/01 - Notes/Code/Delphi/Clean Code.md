---
title: Clean Code com Delphi
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [delphi]
description: Aplciando Clean Code no Delphi
---
# ✍️ Nomenclatura
Devemos nos ==atentar a nomenclatura== de nossas variáveis, funções, métodos entre outros, para facilitar nossa busca e o entendimento do código como um todo para implantação de atualizações e manutenção, devemos ==evitar abreviações==, pois, dentro de uma equipe o funcionamento de abreviações de cada um pode ser diferente, ocasionando em confusão, por exemplo, um utilizar `end` para endereço e outro utilizar `ender`.

# 💬 Comentários
Devemos ==evitar colocar comentários== em nosso código, nosso código bem escrito deve ser entendido como for lido, sem a necessidade de comentários para o entendimento do código, devemos utilizar apenas em momentos específicos como quando implementado algo por necessidade jurídica ou fiscal.

# 📦 Objetos e Estruturas de Dados
Basicamente uma estrutura de dados e quando temos a acesso ao conjunto de dados estruturas, podendo acessar o que for necessário a qualquer momento, a ideia de objeto advindo de orienta a objetos se baseia na ideia de estar disponível apenas o necessário, assim seguindo as regras de encapsulamento, ==nossos objetos não devem ser sacolas de _getters_ e _setters_==

```pascal
TCarro = class
	private
		FCapacidadeDoTanque : integer;
		FLitrosDisponiveis : integer;
		procedure setCapacidadeDeTanque (const Value : integer);
		procedure setLitrosDisponiveis (const Value : integer);
	published
		property CapacidadeDoTanque : integer read FCapacidadeDoTanque write setCapacidadeDeTaque;
		property LitrosDisponiveis : integer read FLitrosDisponiveis write setLitrosDisponiveis;
end;
```

No exemplo acima temos uma classe estrutura de dados apenas, ou seja, não possui encapsulamento, apenas atributos, apenas dados de forma estruturada.

```pascal
ICarro = interface
	function CapacidadeDisponivelTanque : integer;
end;

TCarro = class(TInterfaceObejct, ICarro)
	private
		FCapacidadeDoTanque : integer;
		FLitrosDisponiveis : integer;
	public 
		function CapacidadeDisponivelTanque : integer;
end;
```

Já neste exemplo possuímos o encapsulamento de variáveis privadas e métodos que devolve valores tratados e interessantes ao usuário, diferentes de antes com apenas dados estruturados com acesso livre.

Quando a necessidade de expor uma `property`, é necessário que seja desenvolvido o `get` e o `set` para a mesma, para que possa ser adiciona a _interface_ corretamente.

```pascal
ICarro = interface
	function CapacidadeDisponivelTanque : integer;
	procedure setMarca(const Value : string);
	function getMarca : string;
	property Marca : string read getMarca write setMarca;
end;

TCarro = class(TInterfaceObejct, ICarro)
	private
		FCapacidadeDoTanque : integer;
		FLitrosDisponiveis : integer;
		FMarca : string;
	public 
		function CapacidadeDisponivelTanque : integer;
		procedure setMarca(const Value : string);
		function getMarca : string;
		property Marca : string read getMarca write setMarca;
end;
```

# Limites na Utilização de Terceiros
Devemos tomar cuidado quando utilizamos componentes externos, seja do proprio Delphi, ou adquiridos. Assim devemos evitar acoplamentos e trabalhar com os mesmo encapsulados em classes podendo facilmente propagar uma atualização quando necessário.

```pascal
interface
	type
		IConexao = interface
			procedure Conectar;
		end
		
		IQuery = interface
			procedure ExecQuery;
		end;
		
		TConexaoFiredac = class(TInterfaceObject, IConexao)
			procedure Conectar;
		end;
		
		TQueryFiredac = class(TInterfaceObject, IQuery)
			procedure ExecQuery;
		end;
		
		TConexaoDBExpress = class(TInterfaceObjecdt, IConexao)
			procedure Conectar;
		end; 
		
		TQueryDBExpress = class(TInterfaceObject, IQuery)
			procedure ExecQuery;
		end;
```

Perceba como desenvolvemos uma _interface_ que possui a `procedure` conectar, onde a mesma e implementada por classes que vão utilizar componentes de conexão com banco de dados diferentes. Assim encapsulando tais componentes externos dentro de uma classe que possuímos controle, diminuindo o acoplamento, facilitando manutenção e ate substituição rápida, pois, estaremos utilizando a _interface_.

# Concorrência
Devemos tomar cuidado com o uso de _threds_, devemos utiliza-las em momentos de necessidade, e vale ressaltar a importância da responsabilidade única para o bom funcionamento na implementação da mesma.

# Mau Cheiros no Código
- Informação Inapropriadas
- Passagem de vários parâmetros
- Parâmetros de saída e entrada
- Parâmetros Lógicos
- Códigos de outras linguagens
- Quebra de segurança
- Duplicidade de código
- Níveis errados de abstração
- Classe base depender das derivadas
- Acoplamentos obsoletos
- Nome das variáveis, métodos e funções
- `if` e `case` no lugar de polimorfismo
- Evite números mágicos, utilizar constantes