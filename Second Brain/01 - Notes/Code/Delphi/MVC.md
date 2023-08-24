---
title: MVC no Delphi
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [delphi]
description: Como utilizar a arquitetura MVC no delphi 
---
#  🚀 Introdução
MVC basicamente é a divisão do nosso software entre 3 camadas, sendo elas _Model_, _VIew_ e _Controller_, sua ideia é básica, porem sua implementação requer um conhecimento e alto raciocínio. 
- _Model_ - Responsável pelo acesso aos dados, validação dos dados, basicamente implementa a regra de negocio
- _Controller_ - Responsável por realizar o meio de campo, ligando o _view_ com o _model_
- _View_ - A interface do usuário, onde o mesmo interage com a aplicação, tratando de _backend_, a _view_ seria a URL com os dados em si.

Em uma analogia com um restaurante, o menu seria nossa _view_, onde temos acesso as requisições que podemos realizar,  quando escolhemos enviamos a solicitação para o garçom que é o _controller_, que entrega nosso pedido para o cozinheiro que é o _Model_, e depois volta do cozinheiro para o garçom e cliente.

_Model_ - Entidades, Conexão com o Banco de Dados, Datasets.
_Controller_ - Através da requisição da _View_ defini as configurações da conexão, nível de acesso, tabelas a serem consultadas.
_View_ - Requisições do usuário sobre o que deseja acessar.

_View_ chama fabrica do _Controller_ que se necessário chama fabrica do _Model_

# Nomenclatura
Uma convecção usada para nomeação de `units` em projetos que utiliza a arquitetura MVC é `nome do projeto + camada + e o nome em si`
Pro exemplo, `Calculadora.View.Main.pas`, e dividiremos as camadas em pastas separadas.

## Factory
Basicamente são fabricas de construção para reduzira acoplamentos entre as `units` e criar elementos .

```pascal
interface

uses
  Menus.Controller.Interfaces, Menus.Controller.ListBox.Itens.Default;

type
  TControllerListBoxItensFactory = class(TInterfacedObject, IControllerListBoxItensFactory)
    constructor Create;
    destructor Destroy; override;
    class function New : IControllerListBoxItensFactory;
    function Default : IControllerListBoxItensDefault;
  end;

implementation

{ TControllerListBoxItensFactory }

constructor TControllerListBoxItensFactory.Create;
begin
end;

function TControllerListBoxItensFactory.Default: IControllerListBoxItensDefault;
begin
  Result := TControllerListBoxItensDefault.New;
end;

destructor TControllerListBoxItensFactory.Destroy;
begin
  inherited;
end;

class function TControllerListBoxItensFactory.New: IControllerListBoxItensFactory;
begin
  Result := Self.Create;
end;

end.

```

## Classes Default
Criamos uma classe _default_ que prove o necessário para criar o que é necessário, porem sem utilizar de herança, basicamente um elemento base. Linkamos esse elemento _default_ com sua [[#Factory]], onde a partir da instanciação da _factory_ e de um _default_ dentro dela podemos criar novos itens.

```pascal
unit Menus.Controller.ListBox.Itens.Default;

interface

uses Menus.Controller.Interfaces, FMX.ListBox, FMX.Types, System.Classes;

type
  TControllerListBoxItensDefault = class(TInterfacedObject, IControllerListBoxItensDefault)
  private
    FListBoxItem : TListBoxItem;
  public
    constructor Create;
    destructor Destroy; override;
    class function New : IControllerListBoxItensDefault;
    function Name(Value : string) : IControllerListBoxItensDefault;
    function Text(Value : string) : IControllerListBoxItensDefault;
    function StyleLookup(Value : string) : IControllerListBoxItensDefault;
    function OnClick(Value : TNotifyEvent): IControllerListBoxItensDefault;
    function Item : TFMXObject;
  end;

implementation

{ TControllerListBoxItensDefault }

constructor TControllerListBoxItensDefault.Create;
begin
  FListBoxItem := TListBoxItem.Create(nil);
  FListBoxItem.Name := 'btnDefault';
  FListBoxItem.Text := 'Default';
  FListBoxItem.StyleLookup := 'listboxitemdetaillabel';
end;

destructor TControllerListBoxItensDefault.Destroy;
begin
  inherited;
end;

function TControllerListBoxItensDefault.Item: TFMXObject;
begin
  Result := FListBoxItem;
end;

function TControllerListBoxItensDefault.Name(
  Value: string): IControllerListBoxItensDefault;
begin
  FListBoxItem.Name := value;
  Result := Self;
end;

class function TControllerListBoxItensDefault.New: IControllerListBoxItensDefault;
begin
  Result := Self.Create;
end;

function TControllerListBoxItensDefault.OnClick(
  Value: TNotifyEvent): IControllerListBoxItensDefault;
begin
  FListBoxItem.OnClick := Value;
end;

function TControllerListBoxItensDefault.StyleLookup(
  Value: string): IControllerListBoxItensDefault;
begin
  FListBoxItem.StyleLookup := value;
  Result := Self;
end;

function TControllerListBoxItensDefault.Text(
  Value: string): IControllerListBoxItensDefault;
begin
  FListBoxItem.Text := value;
  Result := Self;
end;

end.
```

Em seguida criamos um interface comum para os itens não padrões.

```pascal
  IControllerListBoxItemForm = interface
    // CTRL + SHIFT + G
    function Show : TFMXObject;
  end;
```

Assim sendo o _Defaul_ faz o trabalho pesado, e os advindos dela realizam apenas a especialização.
Basicamente desenvolvemos as _factorys_, ou fabricas, onde iram conhecer todos que elas podem criar, criamos o _default_ que vai fazer o real trabalho duro, e os subsequentes utilizara do _default_ aplicando algumas alterações.
Onde ==nossa _view_ enxergara apenas nossa _Factory_.==

>[!tip] Violação de Acesso
>Pode ser falta de um `Result := Self` em algum método, ou esquecer de instanciar alguma classe, em 99,9% das vezes que da erro de _acess violation_ na programação funcional é esse o problema.

## Desacoplando Formulários
Podemos desacoplar o conhecimento de nossos _itens_ do _ListBox_ do formulário, basicamente criamos uma classe que criara o formulário o chama e o limpa da memoria, através do nome do mesmo que será passado como _string_.

>[!Tip] Trocando IF por try...except
>Antes o código verificava se a variável não era nula e devolvia um erro.
>```pascal
objFMX :=  TFmxObjectClass(GetClass(ClassName));
if objFMX <> nil then
>	newForm := TCustomForm(objFMX)
else
>	raise Exception.Create('Objeto não existe');
>	
>try
>	newForm.ShowModal;
>finally
>	newForm.Free;
end;
>```
>Porem nos podemos substituir esse `if` por um `try...exception` ficando da seguinte forma.

```pascal
unit Menus.Controller.Forms.Default;

interface

type
  TControllerFormDefault = class
    class procedure CreateForm(ClassName : string);
  end;

implementation

{ TControllerFormDefault }

uses
  FMX.Types, System.Classes, FMX.Forms, System.SysUtils;

class procedure TControllerFormDefault.CreateForm(ClassName: string);
var
  ObjFMX : TFmxObjectClass;
  newForm : TCustomForm;
begin
  objFMX :=  TFmxObjectClass(GetClass(ClassName));

  try
    newForm := (objFMX.Create(nil) as TCustomForm);
    try
      newForm.Position := TFormPosition.ScreenCenter;
      newForm.ShowModal;
    finally
      newForm.Free;
    end;
  except
    on E : Exception do
      raise Exception.Create(E.ClassName + E.Message);
  end;
end;
end.
```

# Model
_Model_ e a camada que lida com os dados, como sabemos é de extrema importância criar um sistema maleável que aceitem mudanças facilmente, por isso, criamos uma estrutura que permita independente do componente de conexão utilizado, diminuindo o acoplamento.

```pascal
type
  IModelConnection = interface
    ['{0BD0485F-506E-4A4F-97D4-CA2AAC2D6260}']
    function EndConnection : TComponent;
  end;
```

## Firedac
Vamos implementar essa interface utilizando o FireDAC com o componente de conexão, por padrão vamos utilizar o _FireBird_ existem formas de desacoplar o banco de dados também, mas não será nesse momento.

```pascal
unit Menus.Model.Connections.ConnectFiredac;

interface

uses
  Menus.Model.Connections.Intefaces, System.Classes, FireDAC.Comp.Client,
  FireDAC.Comp.UI, FireDAC.Phys.FB;

type
  TModelConnectionFiredac = class(TInterfacedObject, IModelConnection, IModelConnectionParams)
  private
    FConnection : TFDConnection;
    FDGUIxWaitCursor : TFDGUIxWaitCursor;
    FDPhysFBDriverLink : TFDPhysFBDriverLink;
    FDataBase : string;
    FUserName : string;
    FPassword : string;
    FDriverID : string;
    FServer : string;
    FPorta : Integer;
    procedure ReadParameters;
  public
    constructor Create;
    destructor Destroy; override;
    class function New : IModelConnection;
    function EndConnection : TComponent;
    function Params : IModelConnectionParams;
    function DataBase(Value : string) : IModelConnectionParams;
    function UserName(Value : string) : IModelConnectionParams;
    function Password(Value : string) : IModelConnectionParams;
    function DriverID(Value : string) : IModelConnectionParams;
    function Server(Value : string) : IModelConnectionParams;
    function Porta(Value : Integer) : IModelConnectionParams;
    function EndParams : IModelConnection;
  end;

implementation

uses
  System.SysUtils;

{ TModelConnectionFiredac }

constructor TModelConnectionFiredac.Create;
begin
  FConnection := TFDConnection.Create(nil);
  FDGUIxWaitCursor := TFDGUIxWaitCursor.Create(nil);
  FDPhysFBDriverLink := TFDPhysFBDriverLink(nil);
  ReadParameters;
  FConnection.Connected := True;
end;

function TModelConnectionFiredac.DataBase(
  Value: string): IModelConnectionParams;
begin
  FDataBase := Value;
  Result := Self;
end;

destructor TModelConnectionFiredac.Destroy;
begin
  FConnection.Free;
  FDGUIxWaitCursor.Free;
  FDPhysFBDriverLink.Free;
  inherited;
end;

function TModelConnectionFiredac.DriverID(
  Value: string): IModelConnectionParams;
begin
  FDriverID := Value;
  Result := Self;
end;

function TModelConnectionFiredac.EndConnection: TComponent;
begin
  Result := FConnection;
end;

function TModelConnectionFiredac.EndParams: IModelConnection;
begin
  Result := Self;
end;

procedure TModelConnectionFiredac.ReadParameters;
begin
  FConnection.Params.Database := FDataBase;
  FConnection.Params.UserName := FUserName;
  FConnection.Params.Password := FPassword;
  FConnection.Params.DriverID := FDriverID;
  FConnection.Params.Add('Server=' + FServer);
  FConnection.Params.Add('Port=' + IntToStr(FPorta));
end;

class function TModelConnectionFiredac.New: IModelConnection;
begin
  Result := Self.Create;
end;

function TModelConnectionFiredac.Params: IModelConnectionParams;
begin
  Result := Self;
end;

function TModelConnectionFiredac.Password(
  Value: string): IModelConnectionParams;
begin
  FPassword := Value;
  Result := Self;
end;

function TModelConnectionFiredac.Porta(Value: Integer): IModelConnectionParams;
begin
  FPorta := Value;
  Result := Self;
end;

function TModelConnectionFiredac.Server(Value: string): IModelConnectionParams;
begin
  FServer := Value;
  Result := Self;
end;

function TModelConnectionFiredac.UserName(
  Value: string): IModelConnectionParams;
begin
  FUserName := Value;
  Result := Self;
end;

end.
```

## Querys
Como estamos trabalhando independente da camada de dados, será necessário desenvolver uma forma genérica para não ficarmos presos e acoplados  com uma dependência na camada de _view_ especifico.
Teremos que criar `units` especificas para cada tipo de componente de conexão utilizado, por exemplo o FireDAC.

```pascal
unit Menus.Model.Connections.TableFiredac;

interface

uses
  Menus.Model.Connections.Intefaces, FireDAC.Comp.Client, System.Classes;

type
  TModelConnectionsTableFireDac = class(TInterfacedObject, IModelDataSet)
  private
    FTable : TFDTable;
  public
    constructor Create(Connection : IModelConnection);
    destructor Destroy; override;
    class function New(Connection : IModelConnection) : IModelDataSet;
    function Open(aTable : string) : IModelDataSet;
    function EndDataSet : TComponent;
  end;

implementation

{ TModelConnectionsTableFireDac }

constructor TModelConnectionsTableFireDac.Create(Connection : IModelConnection);
begin
  FTable := TFDTable.Create(nil);
  FTable.Connection := (Connection.EndConnection as TFDConnection);
end;

destructor TModelConnectionsTableFireDac.Destroy;
begin
  FTable.Free;
  inherited;
end;

function TModelConnectionsTableFireDac.EndDataSet: TComponent;
begin
  Result := FTable;
end;

class function TModelConnectionsTableFireDac.New(Connection : IModelConnection) : IModelDataSet;
begin
  Result := Self.Create(Connection);
end;

function TModelConnectionsTableFireDac.Open(aTable: string): IModelDataSet;
begin
  FTable.Open(ATable);
  Result := Self;
end;

end.
```

ssim sendo caso lance um novo componente de conexão basta mudar ConnectFiredac e TableFiredac para utilizar os novos compoentnes e adequando o nome dos atributos para os mesmo.
Também temos a opção de desenvolver novas `units`.

## Factorys sem Default
Pode ocorrer casos de _factorys_ sem uma classe Default, normalmente quando cada componente/classe que ela gere possua diferentes significativas na estrutura, como uma _factory_ para conexões com o banco de dados e de Datasets, dependendo das diferenças das classes/datases não tem com seguir um default.

## Interface Para Entidades
Entendendo entidades como tabelas do banco de dados, é interessante criar uma _interface_ genérica com o básico que toda entidade deve ter e a partir dela criar as especificas.

>[!attention] Atenção
>Precisamos de um DataSet no Entity para conectar com o banco, ai vem a duvida criamos o mesmo com a _factory_ dentro da Entity, NÃO, importante frisar quem CONTROLA é o _Controller_, ele que defini essas coisas, por isso criaremos _factorys_ no _controller_ para criar conexões e _datasets_.

No _Controller_ utilizaremos o _DataSource_ na tipagem, pois, é o mais genérico e utilizado como base para receber o _DataSets_ e outros, assim sendo compatível com todos.
O uso de classes genéricas é a base para o bom funcionamento com todos os tipos de componentes de conexão diferentes.

## Criando Novas Conexões
Utilizando outros componentes como por exemplo o Zeus, precisaríamos apenas criar novas classes para a Conexão e para o _DataSet_, modificando os mesmo para serem compotiveis com Zeus ou qualquer outro, posterior mente adicionar nas _Factorys_ e utiliza-los.

# View
Na nossa _view_ precisamos apenas de um _DataSorce_, e um atributo privado que contenha nossa entidade utilizando a _interface_ `IControllerEntity`.
Por exemplo utilizamos um _StringGrid_ então fizemos a conexão via `Live Bind`.