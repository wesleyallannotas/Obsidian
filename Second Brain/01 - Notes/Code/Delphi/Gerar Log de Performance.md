---
title: Gerando log de performance
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [delphi]
description: Gerando log de performance no Delphi
---
# Código
Código fonte da Classe em Delphi para gerar logs em `.txt`

```pascal
unit ULog;

interface

type
	TLog = class
	private
		mNivel : Integer;
		mSPID: Integer;
		mIdentificacao: String;
		IniTick: TTime;
		Acumulado: TTime;
	public
		property Nivel: Integer read mNivel;
		property SPID: Integer read mSPID;
		procedure IniProc(Proc: String);
		procedure FimProc(Proc: String);
		procedure StartCount;
		procedure LogaPerformance(Passo: String);
		constructor Create(Identificacao: String); reintroduce;
end;

Var LogGlobal: TLog = nil;

implementation

uses
	Forms, 
	SysUtils, 
	UConexao, 
	System.Classes, 
	Winapi.Windows;
	
{ TLoggerSingleton }

constructor TLog.Create(Identificacao: String);
begin
	mIdentificacao := Identificacao;
	mNivel := 0;
	Randomize;
	mSPID := Random(100000);
end;

procedure TLog.FimProc(Proc: String);
begin
	mNivel := mNivel -1 ;
end;

procedure TLog.IniProc(Proc: String);
var 
	conexao: TConexao;
	sql : string;
begin
	Exit;
	try
		{ sql := 'INSERT INTO LOG_SERVIDOR(SPID,NIVEL,PROCEDIMENTO,DH_INCLUSAO) VALUES ('+
		mSpid.ToString+','+Proc.QuotedString+','+mNIvel.ToString+',CURRENT_TIMESTAMP);';
		conexao := TConexao.Create(mIdentificacao);
		conexao.ExecutaComando(sql); }
	finally
		FreeAndNil(conexao);
		mNivel := mNivel + 1 ;
	end;
end;

procedure TLog.LogaPerformance(Passo: String);
var
	arq: tstringlist;
	nome_arq: string;
	ms: TTime;
	texto: string;
begin
	if not fileexists('c:\temp\master\geralog.txt') then
		exit;
		
	try
		ms := 0;
		nome_arq := 'c:\temp\master\perf_'+Spid.ToString+'.log';
		Arq := TStringList.Create;
		ForceDirectories(ExtractFilePath(nome_arq));
		
		if fileexists(nome_arq)then
			arq.LoadFromFile(nome_arq);
			
		if IniTick <> 0 then
			ms := IniTick - Now;
			
		Acumulado := Acumulado + ms;
		Texto := '';
			
		if ms <> 0 then
		begin
			if Acumulado <> ms then
				Texto := '['+FormatDateTime('HH:NN:SS:ZZZ',Acumulado)+']';
				
			Texto := Texto + '('+FormatDateTime('HH:NN:SS:ZZZ',ms)+') '
		end;
			Arq.Add(texto+Passo);
			arq.SaveToFile(nome_arq);
		finally
			FreeAndNil(Arq);
			IniTick := Now;
		end;
end;

procedure TLog.StartCount;
begin
	IniTick := 0;
	Acumulado := 0;
end;

end.
```

# Utilizar
Basta importar a *unit* que contem a classe através do comando `uses`, criar a variável global, iniciar a contagem e adicionar as gravações onde interessa.

```pascal
LogGlobal := TLog.Create(sessao.identificacao);
LogGlobal.StartCount;
LogGlobal.LogaPerformance('Nome da unit - Antes da Gravação'); // Interessante segui esse padrão de String
Gravar();
LogGlobal.LogaPerformance('Nome da unit - Depois da Gravação');
```