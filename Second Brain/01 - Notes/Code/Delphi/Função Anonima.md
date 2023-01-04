---
title: Função Anonima com Delphi
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [delphi]
description: Criando e Utilizando Função anonima.
---
# Introdução
Função Anônima no Delphi, parecido com o [[Funções#*Arrow Function*|JavaScript]], utilizada no lugar de atalho de funções,
exemplo abaixo traz um projeto em Delphi com um botão e um *edit*
```pascal
// ...........Oculto

type
  TProc = reference to function(arg: string): String;
  TForm1 = class(TForm)
    Button1: TButton;
    Edit1: TEdit;
    procedure Button1Click(Sender: TObject);
  private
    procedure showProc(proc: TProc);
    
// ..........Oculto

implementation

{$R *.dfm}
{ TForm1 }

procedure TForm1.Button1Click(Sender: TObject);
begin
  showProc(function(arg:string):string
  begin
    result := 'Wesley '+arg;
  end);
end;

procedure TForm1.showProc(proc: TProc);
begin
  ShowMessage(Proc(edit1.text));
end;

end.
```

# `String of Object`
Utilizamos o `string of object` quando o nosso tipo será utilizado dentro do objeto e não solto após a declaração do objeto, porem *reference to function*, ou seja, função anônima não utiliza