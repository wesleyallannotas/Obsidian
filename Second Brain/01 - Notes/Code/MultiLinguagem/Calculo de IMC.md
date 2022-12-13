---
title: Calculo de IMC em diferentes linguagens de programação
author: Wesley Silva
url:
book:
type: note
completed: false
aliases:
tags: [multiLinguagem]
description: Como calcular IMC utilizando diferentes linguagens de programação
---
# C++
```c++
#include <iostream>
#include <cmath>

using namespace std;

double calculateImc(double weight, double height) {
  return weight / (pow(height, 2));
}

int main() {
  double weight, height;

  cout << "Enter weight (in kg): ";
  cin >> weight;

  cout << "Enter height (in meters): ";
  cin >> height;

  cout << "IMC: " << calculateImc(weight, height) << endl;

  return 0;
}
```
Observe que nesta implementação em C++, usei a biblioteca `cmath` para calcular o valor de `height` elevado ao quadrado (`pow(height, 2)`). Também usei o `cout` e o `cin` da biblioteca `iostream` para ler e imprimir os valores de peso e altura, respectivamente

# C
```c
#include <stdio.h>
#include <math.h>

double calculateImc(double weight, double height) {
  return weight / (pow(height, 2));
}

int main() {
  double weight, height;

  printf("Enter weight (in kg): ");
  scanf("%lf", &weight);

  printf("Enter height (in meters): ");
  scanf("%lf", &height);

  printf("IMC: %lf\n", calculateImc(weight, height));

  return 0;
}
```
Observe que nesta implementação em C, usei a biblioteca `math.h` para calcular o valor de `height` elevado ao quadrado (`pow(height, 2)`). Também usei o `printf` e o `scanf` da biblioteca `stdio.h` para ler e imprimir os valores de peso e altura, respectivamente.

# TypeScript utilizando classe
```typescript
class Pessoa {
	nome: string;
	peso: number;
	altura: number;
	
	constructor(nome: string, peso: number, altura: number) {
		this.nome = nome;
		this.peso = peso;
		this.altura = altura;
	}
	
	calculaIMC(): number {
		return this.peso / (this.altura * this.altura);
	}
}

const pessoa = new Pessoa('João', 75, 1.75);
console.log(`IMC de ${pessoa.nome}: ${pessoa.calculaIMC()}`);
```
Neste código, criamos uma classe `Pessoa` que tem os atributos `nome`, `peso` e `altura`. O construtor da classe recebe esses três parâmetros e os atribui aos atributos da classe.

Em seguida, criamos um método chamado `calculaIMC` que calcula e retorna o índice de massa corporal da pessoa usando seu peso e altura.

Finalmente, criamos uma instância da classe `Pessoa` e usamos o método `calculaIMC` para calcular o IMC desta pessoa. O resultado é então exibido no console.

# Delphi utilizando classe
```pascal
type
  TPessoa = class
  private
    FNome: string;
    FPeso: Double;
    FAltura: Double;
  public
    constructor Create(nome: string, peso: Double, altura: Double);
    function CalculaIMC: Double;
  end;

constructor TPessoa.Create(nome: string, peso: Double, altura: Double);
begin
  FNome := nome;
  FPeso := peso;
  FAltura := altura;
end;

function TPessoa.CalculaIMC: Double;
begin
  Result := FPeso / (FAltura * FAltura);
end;

var
  pessoa: TPessoa;
begin
  pessoa := TPessoa.Create('João', 75, 1.75);
  try
    Writeln('IMC de ' + pessoa.FNome + ': ' + pessoa.CalculaIMC.ToString);
  finally
    pessoa.Free;
  end;
end.

```
Neste código, criamos uma classe `TPessoa` que tem os atributos `FNome`, `FPeso` e `FAltura`. O construtor da classe recebe esses três parâmetros e os atribui aos atributos da classe.

Em seguida, criamos um método chamado `CalculaIMC` que calcula e retorna o índice de massa corporal da pessoa usando seu peso e altura.