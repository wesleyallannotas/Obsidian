---
title: Concta Correntes Simples em Varias Linguagens de Programação
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [multiLinguagem] 
description: Criar classe conta corrente bem simplificada em várias linguagens de programação 
---
# JavaScript
Aqui está uma classe em JavaScript que representa uma conta corrente com métodos de saque e depósito:

```javascript
class ContaCorrente {
  constructor(saldoInicial) {
    this.saldo = saldoInicial;
  }

  deposita(valor) {
    this.saldo += valor;
  }

  saca(valor) {
    this.saldo -= valor;
  }

  getSaldo() {
    return this.saldo;
  }
}
```

Para usar esta classe, basta criar uma nova instância de `ContaCorrente` passando o saldo inicial, e em seguida chamar os métodos `deposita()` e `saca()` conforme necessário. Por exemplo:

```javascript
let conta = new ContaCorrente(100);
conta.deposita(50);
conta.saca(25);
let saldoAtual = conta.getSaldo(); // saldoAtual = 125
```

# Java
Aqui está uma classe em Java que representa uma conta corrente com métodos de saque e depósito:

```java
public class ContaCorrente {
  private double saldo;

  public ContaCorrente(double saldoInicial) {
    this.saldo = saldoInicial;
  }

  public void deposita(double valor) {
    this.saldo += valor;
  }

  public void saca(double valor) {
    this.saldo -= valor;
  }

  public double getSaldo() {
    return this.saldo;
  }
}
```

Para usar esta classe, basta criar uma nova instância de `ContaCorrente` passando o saldo inicial, e em seguida chamar os métodos `deposita()` e `saca()` conforme necessário. Por exemplo:

```java
ContaCorrente conta = new ContaCorrente(100);
conta.deposita(50);
conta.saca(25);
double saldoAtual = conta.getSaldo(); // saldoAtual = 125
```

# Delphi
Aqui está uma classe em Delphi que representa uma conta corrente com métodos de saque e depósito:

```pascal
type
  TContaCorrente = class
  private
    FSaldo: Double;
  public
    constructor Create(saldoInicial: Double);
    procedure deposita(valor: Double);
    procedure saca(valor: Double);
    function getSaldo: Double;
  end;

implementation

constructor TContaCorrente.Create(saldoInicial: Double);
begin
  FSaldo := saldoInicial;
end;

procedure TContaCorrente.deposita(valor: Double);
begin
  FSaldo := FSaldo + valor;
end;

procedure TContaCorrente.saca(valor: Double);
begin
  FSaldo := FSaldo - valor;
end;

function TContaCorrente.getSaldo: Double;
begin
  Result := FSaldo;
end;
```

Para usar esta classe, basta criar uma nova instância de `TContaCorrente` passando o saldo inicial, e em seguida chamar os métodos `Deposita()` e `Saca()` conforme necessário. Por exemplo:

```pascal
var
  conta: TContaCorrente;
  saldoAtual: Double;
begin
  conta := TContaCorrente.Create(100);
  conta.Deposita(50);
  conta.Saca(25);
  saldoAtual := conta.GetSaldo(); // saldoAtual = 125
end;
```

# Rust
Aqui está uma implementação básica de uma classe de conta corrente em Rust que inclui métodos para sacar e depositar dinheiro:

```rust
// Define a classe de conta corrente
struct ContaCorrente {
    // Define o saldo atual da conta
    saldo: f32,
}

// Implementa um método para depositar dinheiro na conta
impl ContaCorrente {
    fn depositar(&mut self, valor: f32) {
        self.saldo += valor;
    }
}

// Implementa um método para sacar dinheiro da conta
impl ContaCorrente {
    fn sacar(&mut self, valor: f32) -> bool {
        if self.saldo >= valor {
            self.saldo -= valor;
            return true;
        } else {
            return false;
        }
    }
}

fn main() {
    // Cria uma nova conta corrente com saldo inicial de 100
    let mut conta = ContaCorrente { saldo: 100.0 };
	
    // Tenta sacar 50 da conta
    let sucesso = conta.sacar(50.0);
    if sucesso {
        println!("Saque realizado com sucesso!");
    } else {
        println!("Saldo insuficiente");
    }
	
    // Imprime o saldo atual da conta
    println!("Saldo atual: {}", conta.saldo);
	
    // Deposita mais 50 na conta
    conta.depositar(50.0);
	
    // Imprime o saldo atual da conta
    println!("Saldo atual: {}", conta.saldo);
}
```