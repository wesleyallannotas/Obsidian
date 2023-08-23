---
title: PPO com Delphi
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [delphi]
description: Aprendendo POO com delphi
---
# 🚀 Introdução
Basicamente como vimos sobre [[Introdução a POO]], basicamente é a forma de pensar mais em contato com a realidade, abstraindo coisas do mundo real para a programação, facilitando a reutilização e compreensão do código.

# 🏗️ Criando Classes
Todas as classes ficam dentro do `type`, é onde as representamos 
Dentro do tempo por convenção toda classe começa com T por exemplo `TGarrafa`, em seguida a tipos como `class`, em seguida dentro deste bloco listamos os atributos.

```pascal
type
	TGarrafa = class
		Cor : string;
		Modelo : string;
		Tampo : string;
		procedure ArmazenarLiquido(Liquido: string);
	end;
```

Quando criamos uma classe dessa forma, estamos descendendo da classe `TObject` do Delphi

# 📥 Instanciando Objeto
Não basta declarar uma variável do tipo do nosso objeto desenvolvido e sair utilizando, é necessário criar uma instancia deste nosso objeto, ou seja, o criando na memória, onde conseguimos o mesmo através do método `create` herdado de `TObject`

```pascal
proceduto TForm.ButtonClick(Sender: TObject);
var
	MinhaGarrafa : TGarrafa;
begin
	MinhaGarrafa := TGarrafa.Create;
	MinhaGarrafa.Modelo := 'Video';
end;
```

Como boa pratica devemos destrui-lo quando o mesmo não tiver mais utilidade, assim limpando a memória e não ocorrendo o acumulo exacerbado de memoria, deixando o sistema lento, conseguimos realizar essa ação através do método `free` herdado de `TObject`.

```pascal
proceduto TForm.ButtonClick(Sender: TObject);
var
	MinhaGarrafa : TGarrafa;
begin
	MinhaGarrafa := TGarrafa.Create;
	MinhaGarrafa.Modelo := 'Video';
	MinhaGarrafa.Free;
end;
```

Melhorando nosso código e adicionando boas praticas, é interessante abraçar código com o `try`.

```pascal
proceduto TForm.ButtonClick(Sender: TObject);
var
	MinhaGarrafa : TGarrafa;
begin
	MinhaGarrafa := TGarrafa.Create;
	try
		MinhaGarrafa.Modelo := 'Video';
		MinhaGarrafa.Cor :- 'Vermelha';
	finally
		MinhaGarrafa.Free;
	end
end;
```

>[!attention] Atenção com a memória
>Delphi NÃO possui _garbage collection_, assim não limpando a memória, ou seja, necessita do cuidado do desenvolvedor para não sobrecarregar de variáveis em memórias, sem um uso

Atribuir valor `nil` para uma variável antes de utiliza-la, para aplicações com _desktop_ não possui nenhum problema, porem para _mobile_ onde é utilizado _ARC_ como _garbage collector_, ele ira limpar na memória, pois, é uma variável apontando para o nulo, assim não tendo necessidade de existir.

Quando utilizamos o `free` em um objeto, estamos apagando o mesmo da memória, porem a variável se mantem, só que sem o objeto, assim quando utilizamos o `FreeAndNil()` ele é limpado da memória e apontado para o nulo, assim o removendo do escopo que se encontra.

```pascal
proceduto TForm.ButtonClick(Sender: TObject);
var
	MinhaGarrafa : TGarrafa;
begin
	MinhaGarrafa := TGarrafa.Create;
	try
		MinhaGarrafa.Modelo := 'Video';
		MinhaGarrafa.Cor :- 'Vermelha';
	finally
		FreeAndNil(MinhaGarrafa);
	end
end;
```

Podemos concluir que quando vamos reutilizar a variável dentro do escopo é interessante utilizar o método `free` herdado de `TObject`, porem quando não vamos, podemos utilizar o `FreeAndNil()`

# 🔎 Verificando Objeto
Podemos verificar se o objeto foi criado com `Assigned()`

```pascal
proceduto TForm.ButtonClick(Sender: TObject);
var
	MinhaGarrafa : TGarrafa;
begin
	MinhaGarrafa := nil;
	
	if Assigned(MinhaGarrafa) then
		ShowMessage('Esta instanciado');
	else
		ShowMessage('Não esta instanciado');
	
	MinhaGarrafa := TGarrafa.Create;
	try
		MinhaGarrafa.Modelo := 'Video';
		MinhaGarrafa.Cor := 'Vermelha';
	finally
		FreeAndNil(MinhaGarrafa);
	end
end;
```

# 🔥 Records
Diferente de classes `record` trabalha na memória local, assim tendo seu valor copiado toda vez que é requisitado, ao contrario de `class` que utiliza referencia na memória, por isso não utilizamos o método `create` e podemos passar valores diretamente, porem o `record` tem perda de desempenho comparado com `class`, também não é necessário limpar da memória.

```pascal
type
	TConfig = record
		Host : string;
		Path : string;
		Usuario : string;
		Senha : string;
	end;
```

```pascal
proceduto TForm.ButtonClick(Sender: TObject);
var
	Configuracoes : TConfig;
begin
	Configuracao.Host := 'localhost';
	Configuracao.Path := 'C:/User/Admin';
	Configuracao.Usuario := 'testeuser';
	Configuracao.Senha := 'admin123'
	
	Exibe(Configuracao); // Procedure que exibe todos os valores
end;
```

Dessa forma quando passamos um `record` como um parâmetro, para uma _procedure_ ou _function_, os valores são copiados, ao contrario do objeto que utiliza uma referencia na memória, o que pode ser ruim para memória se for usado erroneamente.

# 🧱 Construtores e Destrutores
Quando desenvolvemos nossa classe podemos construir os métodos de `constructor` e `desctructor`, responsáveis por construir nossa instancia da classe, e o `destructor` e destruir, limpar a mesma da memória.

```pascal
type
	TConfig = record
		Host : string;
		Path : string;
		Usuario : string;
		Senha : string;
		constructor Create;
		destructor Destroy; override;
	end;
```

# 👥 Classes Compostas
Durante o desenvolvimento das nossas classes, pode ser necessário aninhar classes, assim sendo necessário adições nos nossos construtores e destrutores.

```pascal
interface
type
	TRoda = class
		dimensoes : string;
		material : string;
	end;
	
	TMotor = class
	 potencia : integer;
	 combustivel : string;
	end;
	
	TCarro = class
		ano : integer;
		modelo : string;
		marca : string;
		kilometragrem : double;
		Roda : TRoda;
		Motor : TMotor;
		constructor Create;
		destructor Destroy; override;
	end;

implementation
constructor TCarro.Create;
begin
	Roda = TRoda.Create;
	Motor = TMotor.Create;
end;

destructor Destroy;
begin
	Roda.Free;
	Motor.Free;
	inherited;
end;
```

# 📩 Classes Aninhadas
São basicamente classes declaradas dentro de classes, seu uso não é tão abrangente, porem é interessante em casos de encapsulamento.

```pascal
interface
type
	TCarro = class
	 type
		 TRoda = class
			 Tipo : string;
			 Tamanho : string;
		 end;
		private
			Marca : string;
			Modelo : string;
			Roda : TRoda;
		public
			procedure MontarCarro;
	end;

// .....

implementation
procedure MontarCarro;
begin
	Marca := 'BMW';
	Modelo := 'A320';
	Roda.Tipo := 'Liga Leve';
	Roda.Tamanho := 18;
end;
```

# ✍️ Property
Basicamente é uma facilidade do Delphi para o uso e criação dos _getters_ e  _setters_, o interessante é que os utilizando podemos executar como se fosse com a próprio atributo do objeto.

```pascal
interface
type
	TCliente = class
		private
			FNome : string;
			procedure SetNome(const Value : string);
		property Nome : string read FNome write SetNome
	end;
implementation
procedure SetNome(const value : string);
begin
	if value.length < 3 then
		raise Exception.create('Nome Invalido!');
	FNome := Value;
end;

// Utilizando essa classe

cliente.nome = 'Wesley';
```

# 🧑‍🤝‍🧑 Classes Amigas
Uma classe tem atributos privado de fato apenas quando esta sozinha em uma `unit`, quando existem mais de uma classe em uma `unit`, são interpretadas como classes amigas, assim possuindo a liberdade de acessar tais atributos privados.

# ⛓️ Strict Private
Basicamente corrige o problema das [[#Classes Amigas]] de quebrar o encapsulamento das nossas classes, assim removendo o acesso a tais propriedades e métodos, basta adicionar o `strict` antes do `private`

```pascal
type
	TRoda = class
		strict private
			Material : string;
	end;
	
	TCarro = class
		strict private
			Valor : currency;
	end;
```

# 👀 Protected
Quando adicionamos um atributo ou método no `private`, só tem acesso a mesma a classe que a declarou ([[#Classes Aninhadas|aninhamento]]) e as [[#Classes Amigas|classes amigas]], ou seja, os descendentes não tem acesso, para dar  acesso aos descendentes, invés de declarar dentro do `private`, utilizamos o `protected`

```pascal
type
	TPessoa = class
		protected
			exemplo : integer;
	end;
```

Porem devemos devemos tomar cuidado, pois, `protected` dando acesso direto, fere o encapsulamento, sendo mais interessante e preservando o encapsulamento a utilização de _getters_ e _setters_

# ☝️ Coesão
Cada método de nossa classe tem apenas uma responsabilidade, ou seja, ==o principio da responsabilidade única==, ferindo essa "regra", podemos encontrar problemas futuros, por exemplo, toda vez que cadastramos um cliente geramos financeiro, e se um dia não queremos mais isso?
Vale ressaltar que estamos falando sobre o método em si.

```pascal
procedure TForm1.ButtonClick(Sender : TObject);
var
	Cliente : TCliente;
begin
	Cliente = TCliente.Create;
	try
		Cliente.Nome := 'Jose';
		Cliente.Telefoe := '997386518'
		Cliente.Endereco := 'Rua Armelindo, Centro'
		Cliente.CadastrarCliente;
		Cliente.CriarFinanceiro;
	finally
		Cliente.free;
end;
```

O exemplo a cima segui a reponsabilidade única, pois, cada método chamado, é responsável por fazer uma única responsabilidade.

# 🔗 Acoplamento
Um bom sistema tem muita coesão é baixo acoplamento, um exemplo de acoplamento e quando criamos uma classe de conexão com o banco de dados e as usamos em todas as outras classes do sistema, assim gerando uma dependência um acoplamento, e se no futuro mudarmos de banco será um problema mudar em tudo, para eliminar o acoplamento existem diversos meios sendo um deles a utilização de `interface`

# 👤 Interface
Por convenção no _Delphi_ iniciamos nossas interfaces com a letra "I", mesmo não sendo umas das recomendações do _Clean Code_, normalmente geramos uma assinatura na nossa interface, basicamente com interface criamos uma espécie de contrato onde delimita o que tem existir, definimos campos que devem ser preenchidos, em seguida implementamos nossa interface em uma classe.

>[!tip] Importante
>1. É importante sempre utilizar o `TInterfaceObject` quando formos implementar um interface, basicamente é um facilitador do _Delphi_ que evita que temos que implementar algumas funcionalidades.
>2. _Object Pascal_ não permite herança multipla, diferentes de C++ por exemplo, assim podemos "burlar" quando necessário através do uso de interfaces.
>3. Quando trabalhamos com _interface_ o ARC já limpa a mesma da memoria sem a necessidade de que a limpamos.

```pascal
// ... Dentro do Arquivo de Interfaces ...

IConexao = interface
	// CTRL + ALT + G - Para gerar a assinatura
	procedure Gravar
end;

// ... Dentro da Classe ...

TConexaoSQLServer = class(TInterfaceObject, IConexao)
	procedure Gravar;
end;
```

Agora basta utilizar nossa interface para "Tipar" a conexão com o banco nas classes, assim qualquer classe que implemente esta interface será compatível, assim retirando o acoplamento e dando a liberdade para alterar de banco de dados a qualquer momento, basta implementar a conexão com o novo banco a partir da nossa interface, agora basta pedir nossa interface no `create` no nosso objeto, e quando implementado passar uma instancia da classe do banco.

```pascal
type
	Conexao : IConexao;
	// ...
	constructor Create(aConexao : IConexao);
	// ...

constructor TCliente.Create(aConexao : IConexao);
begin
	Conexao := aConexao
end;

// ...
Cliente := TCliente.Create(TConexaoMySQL.Create);
```

# 🌐 Virtual
Através da declaração do `virtual`, liberamos para que as classes que herdam esta classe possam alterar/sobrescrever/sobrecarregar tal método, assim aplicando o conceito de polimorfismo, onde nas classes filhas que vão alterar tal método, deve usar o `override`

```pascal
type
	TPessoa = class
		function Tipo : string; virtual; 
	end;

// ...

type
	TCliente = class(TPessoa)
		 function Tipo : string; override;
	end
```

## ✍️ Dinamyc
Quando utilizamos o virtual utilizamos a VMT é registrado em uma matriz de métodos virtuais toda vez que ele é chamado, assim impactando em uma maior performance, já no `dinamyc`, não tem isso, só é registrado e apenas uma vez quando o método é sobrescrito, assim sendo mais lento porem consumindo uma menor quantidade de memoria.

# 🎨 Métodos Abstratos
Basicamente é quando criamos um método que existira na classe pai, porem será implementado dentro das classes que as herdam, ou seja, as classes filhas.
Basta adicionar o `abstract` na frente da declaração do método.

```pascal
type
	TPessoa = class
		// ....
		function Tipo : string; virtual; abstract;
	end;
```

## ✍️ Exemplo
Utilizando herança com métodos abstrato, Voz existe dentro de animal, pois, foi criado como método abstrato dentro da classe pai, se não fosse declarado a gente não conseguiria "enxerga-lo".
TGato ou TCachorro são instancias atribuídas ao animal, pois, são descendentes de TAnimal.

```pascal
interface
type
	TAnimal = class
		 function Voz : string; virtual; abstract;
	end;
	
	TCachorro = class(TAnimal)
		function Voz : string; override;
	end;
	
	TGato = class(TAnimal)
	 funcion Voz : string; override;
	end;

implementation
function TCachorro.Voz : string;
begin
	Result := 'Au Au';
end;

function TGato.Voz : string;
begin
	Result := 'Miau';
end;

// ... Utilziando ...

procedure TForm.ButtonClick(Sender : TObject);
var
	Animal : TAnimal;
begin
	case ComboBox of
		0 : Animal := TCachorro.Create;
		1 : Animal := TGato.Create; 
	try
		ShowMessage(Animal.Voz);
	finally
		Animal.Free;
end;
```

# 💌 Classe Selada
São classes que não permitem serem herdadas, ou seja, não podemos a partir dela gerar outra classe, assim evitando uso indevido, tanto é que é uma praticam muito usada no desenvolvimento de componentes, também limita que criamos empilhamentos de heranças muito complexas, travando em determinado ponto, basta adicionar a palavra `sealed`

```pascal
type
	TDinossauro = class sealed (TAnimal)
	 function Voz : String; override;
	end;
```

# 🚧 Método Final
Parecido com a [[#Classe Selada|classe selada]] o método final, impede que a partir daquele ponto sobrecarregue/sobrescreva tal método, podemos atingir tal comportamento através do `final`

```pascal
type
	TDinossauro = class(TAnimal)
	 function Voz : string; override; final;
	end;
	
	TRex = class sealed (TDinossauro)
	 function foz : string; override; // DA ERRO!
	end;
```

# 🔋 Sobrecarga
Basicamente é quando possuímos o mesmo método sobrecarregado, ou seja, o mesmo método com parâmetros diferentes, é necessários adicionar o `overload` na frente da declaração, muito utilizado para reduzir o uso de `if`

```pascal
type
	// ...
	procedure CriarFinanceiro; overload;
	procedure CriarFinanceiro(Value : Currency); overload;
```

# 🎪 Orientação a Eventos
Definimos a estrutura do evento e o utilizamos dentro da classe, sem saber de fato onde esse evento será utilizado, seja para adicionar valor a um `memo`, `label`, não importa a classe não sabe e não precisa saber, apenas sabe que precisa ser passado uma `string`

```pascal
// Unit Class.Pessoa
type
	TEventMsg = procedure (Value : string) of object;
	
	TPessoa = class
	private
		 FNome : string;
		 FEventMsg : TEventMsg
		 procedure setNome(const Value : string);
		 procedure setEventMsg(const Value : TEventMsg);
		 // ...
	public
		procedure Cadastrar;
		property Nome : string read FNome write setNome;
		property EventMeg : TEventMsg read FEventMsg write setEventMsg;
	end;
	
implementation
	procedure Cadastrar;
		// Codigo...
		EventMsg(Nome + ' Cadastrado com sucesso!');
```

Onde no formulário que é quem esta chamando essa classe, passamos uma estrutura definimos a estrutura compatível que vai executar e passamos a mesma para a nossa classe, onde podemos ==apontar uma função ou passar uma função anônima==. 

```pascal
// Unit TForm1
interface
	TForm1 = class(TForm)
	 //...
	 private
		 procedure ExibeMsgMemo(Value : string);
	end;

implementation
	procedure TForm1.ExibeMsgMemo(Value : string);
	begin
		Memo1.Lines.Add(Value);
	end;

	procedure TForm1.ButtonClick1(Sender : TObject);
	var
		Cliente : TClient;
	begin
		Cliente := TClient.Create(TConexaoMySQL.Create);
		try
			 Cliente.EventMsg := ExibeMensagemMemo;
		finally
			Cliente.Free;
	end;
```

Assim podemos concluir que a classe não tem conhecimento do que será feito, apenas sabe que tem um evento que precisa de um parâmetro que precisa de uma `string`, onde podemos basicamente trocar por exemplo agora começar exibir em um _label_, não importa para a classe, o que abre uma gama de possibilidades incrível, com herdeiros de uma classe que implementa um evento, tento impacto em lugares diferentes no nosso formulário.

## 🤔 Melhorando esse Código
Podemos melhorar a forma que foi feita, protegendo contra erros e liberando toda responsabilidade do evento da classe e deixando para o formulário.

```pascal
// Unit Class.Pessoa
type
	TNotifyEvent = procedure (Sender : TObejct) of object;
	
	TPessoa = class
	private
		 FNome : string;
		 FEventMsg : TEventMsg
		 procedure setNome(const Value : string);
		 procedure setOnCadastro(const Value : TObejct);
		 // ...
	public
		procedure Cadastrar;
		property Nome : string read FNome write setNome;
		property OnCadastro : TNotifyEvent read FOnCadastro write setOnCadastro;
	end;
	
implementation
	procedure Cadastrar;
		// Codigo...
		OnCadastro(self);
```

Basicamente agora nosso parâmetro é um objeto genérico, ou seja, estamos pedindo um `TObject`, e já sabemos que no _Delphi_ todo objeto descendo de `TObject`, assim passamos nós mesmo para tal função, deixando para o formulário decidir como implementar o resultado.

```pascal
// Unit TForm1
interface
	TForm1 = class(TForm)
	 //...
	 private
		 procedure OnCadastro(Sender : TObject);
	end;

implementation
	procedure TForm1.OnCadastro(Sender : TObject);
	begin
		Memo1.Lines.Add('Foi cadastrado o cliente ' TPessoa(Sender).Nome);
	end;

	procedure TForm1.ButtonClick1(Sender : TObject);
	var
		Cliente : TClient;
	begin
		Cliente := TClient.Create(TConexaoMySQL.Create);
		try
			 Cliente.OnCadastro := OnCadastro;
		finally
			Cliente.Free;
	end;
```

Realizamos um _casting_ onde informamos que o nosso objeto é dó tipo de classe, assim possuindo acesso a suas propriedades e métodos.
Porem dessa forma pode ocorrer de quando chamarmos o objeto, esquecermos de passar um valor para o evento, assim podendo resultar em erros na nossa aplicação, porem temos uma técnica para evitar isso, basicamente validamos o mesmo dentro da classe.

```pascal
// Unit Class.Pessoa
type
	// ...
	public
		procedure Cadastrar;
		procedure EvOnCadastro;
		property Nome : string read FNome write setNome;
		property OnCadastro : TNotifyEvent read FOnCadastro write setOnCadastro;
	end;
	
implementation
	procedure Cadastrar;
	begin
		// Codigo...
		EvOnCadastro;
	end;
	
	procedure EvOnCadastro;
	begin
		 if Assigned(OnCadastro) then
			 OnCadastro(self);
	end;
```

Assim criamos uma `procedure` simples que validada se foi "assinado" algum valor na variável, onde ai sim chamamos a mesmo passando o próprio objeto, caso não, não fara nada evitando erros, tratamento importante, pois, ==uma classe tem que tratar todos seus atributos e métodos e não delegar isso a terceiros==.

# 🧩 Criando um Componente
No _Delphi_ todo componentes descende da classe `TComponent` que podemos obtê-la a partida a `unit` `System.Classes`, sem seguida podemos construir nosso componente/classe.
- `Publish` - Propriedades adicionadas nessa seção ficaram disponíveis para o usuário no _Object Inspection_

```pascal
type
	TEventos = class(Tcomponente);
		private
		public
		published
	end;
```

Em seguida precisamos registar nosso componentes, onde como parâmetros passaremos um nome para o pacote de componentes e uma _array_ com os componentes.

```pascal
procedure register;

type
// ...

procedure register;
begin
	RegisterComponents('Meus Componentes', [TEventos]);
end;
```

# 🏗️ Método Construtor
Utilizando o nossa `create` esta sendo criado uma instancia completa da nossa classe, dando a acesso a diversas coisas até mesmo herdadas do nosso objeto, utilizando um método construtor, conseguiremos instancias apenas `interface`, assim dando acesso apenas ao que tem na `interface`

```pascal
public
	constructor Create;
	destructor Destroy; override;
	class function New : IOperacao;

// ...
implementation
	procedure TForm.New: IOperacao ;
	begin
		Result := Self.Create;
	end;
```

# 🔗 Composição de Objetos com Interface
Utilizando a ideia de classes com responsabilidade única, onde por exemplo no desenvolvimento de uma calculadora podemos criar uma classe para cada operação e as compor em uma `interface` de calculadora.

```pascal
ICalculadora = interface
	// CTRL + G
	function Somar : IOperacão;
	function Subtrair : IOperacão;
	function Dividir : IOperacão;
	function Multiplicar : IOperacão;
end;
```

Após desenvolver a `interface` que conecta todas as classes que implementa a `interface IOperacao`, implementaremos a mesma em uma classe que ira implementar esta interface

```pascal
TCalculadora = class(TInterfaceObject, ICalculadora)
	public
		constructor Create;
		destructor Destroy; override;
		class function New: ICalculadora;
		function Somar : IOperacão;
		function Subtrair : IOperacão;
		function Dividir : IOperacão;
		function Multiplicar : IOperacão;
end;
```

Onde cada função retorna a execução da [[#Método Construtora|método construtor]] da classe da operação que o representa.

```pascal
interface
	function Multiplicar : IOperacao;
	begin
		Result := TMultiplicar.New;
	end;
```

# 🆘 Helpers
Classes _Helpers_ são classes de ajuda como o próprio nome diz é uma classe de ajuda, que podemos agregar a nossa classe atribuindo novas funcionalidades, em _Helpers_ podemos desenvolver novos métodos, porem não podemos criar novos atributos.

```pascal
interface
	TCaptionHelper = record helper for TCaption
		function ToCurrency : Currency;
	end;


implementation
	function TCaptionHelper.ToCurrency : Currency;
	begin
		Result := StrToCurr(Self);
	end;
```

No exemplo acima desenvolvemos um _helper_ para a classe `TCaption`, onde desenvolvemos uma função de nome `ToCurrency` que devolve um valor do tipo `Currency`.

Também podemos criar _Helpers_ para tipos primitivos.

```pascal
interface
	TStrHelper = record helper to string
		function ToCurrency : Currency;
	end;

implementation
	function TStrHelper.ToCurrency : Currency;
	begin
		 Result := StrToCurr(Self);
	end;
```

# Construindo Formulários em Tempo de Execução
## FireMonkey
Diferente da VLC, o FireMonkey não conseguimos criar a partir da classe o nosso formulário, sendo necessário utilizar o `initialization`

```pascal
initialization
	RegisterFMXClasses([TfrmProduct]);
```

Precisamos registrar a mesma a partir da função `RegisterFMXClasses`, onde como parâmetro passamos uma _array_ com os nomes das classes dos formulários.

# 🤔 Exemplo

1. Criamos um `interface` que executa uma ação com duas variáveis do tipo `double` e retorna um `doube`, em seguida criamos uma classe para cada operação implementando essa `interface`, já no formulários criamos uma `property` do tipo da nossa `interface` e uma função no `private` que executa a função que estará dentro dessa nossa `propety`, no acionar de cada botão instanciamos umas das classes correspondentes a operação que o botão realiza e em seguida executas a função que criamos no `private`.
2. Por boa pratica devemos definir sempre os `constructor` e o `destructor` com sobrecarga (`override`), também é interessante criar uma método construtor para cada classe que desenvolvemos, e mudar criação das instancias de `create` para `new` assim o utilizando.
3. Utilizamos o método de [[#Composição de Objetos com Interface]] criamos a classe `TCalculadora` agora basta instanciar a classe no formulário e para cada clique do botão chamar a função correspondente, por exemplo soma `Claculadora.Soma.Operacao(StrToCurr(Edit1.Text), StrToCurr(Edit2.Text))`.
4. Criamos uma [[#Helpers|classe helper]] para o `TCaption` com um método que transforma o valor de uma `string` para `currency`, e o utilizamos no lugar do _casting_.
5. Criamos uma [[#Helpers|classe helper]] para o tipo primitivo `string` que transforma o mesmo em um `currency`, em seguida implementamos uma [[#Sobrecarga]] do método `Operacao`, onde recebe duas `Strings` e devolve um `string`, onde dentro utiliza nosso método advindo do `helper` para realizar o _castings_ para realizar a operação.
6. Refatoramos o código separando cada classe em uma `unit`, construímos uma `unit` com todas as `interfaces` e uma `unit` com todas os _Helpers_, em seguida pela necessidade de importar a `unit` `System.Util`, fomos obrigados a abandonar nosso _Helper_ de `string` e utilizar o que ele nos disponibiliza, o `toDouble`, sendo necessário realizar algumas alterações no código.
7. Criamos uma `TList` genérica com o tipo `Double`, adicionamos sua instanciação no `create` e a limpamos no `destructor` com o método `free`, adicionamos o método para inserir dados na lista com [[#Sobrecarga]] de diferentes tipos, para não ser necessário realizar o _casting_, em seguida desenvolvemos uma classe que será utilizada para ser a ancestral das operações, assim a chamando de `TOperacoes`, onde ela implementara a interface `IOperacoes`, e agora as classes de cada operação herda dela, onde construímos um método executar `virtual` onde limpamos a lista, e nas classes de operações executaremos a conta e em seguida utilizaremos o `inherited` para executar o que tem na herança, nossa lista foi criada dentro do `protected` justamente para os filhos conseguirem enxergar, usamos o `var` para utilizar a referencia e não copiar o objeto. 
8. Criamos a tipagem de um evento, em seguida criamos interfaces que entram na atribuição desse evento e que sai, tanto para a calculadora quanto para operação, onde ambas também implemento essas novas interfaces, criamos uma função de exibição que é o evento em si, e o passamos no `formCreate` para a classe da calculadora que se encarregara de na função de soma passar para a classe de soma.