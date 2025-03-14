*Teste-Driven Development*

Aparentemente essa porra vai usar:
- Dois projetos em dotnet 3.1 (um de teste)

---
#### Introdução ao TDD

- TDD - Test Driven Development
	- Testes antes de codar
- Premissa - Regra de negócios "primeiramente" nos testes
	- Você aplica as regras de negócio nos testes
- Quando é vantajoso usar?
	- Quando você tem regras de negócio bem específicas

Obs: Normalmente vai dar pau nos primeiros testes, o intuito é esse e é normal.

O ciclo é basicamente esse:
![[Pasted image 20241113194715.png]]
	*(ciclo horário)*

---
#### O que precisa para praticar o conteúdo

- Microsoft Visual Studio Community 2019
- DotNet Core 3.1
- xUnit

---
#### Refinamento inicial para o projeto de uma calculadora

- Uma Calculadora que contém Soma, Subtração, Divisão e Multiplicação e histórico de operações.

- Regras de negócios:
	- Números inteiros
	- 2 parâmetros por operação
	- Sempre retornar as últimas 3 operações do histórico

---
### Prática 

#### Parte 1 - Criando um novo projeto
*Meti do loko e instalei o Visual Studio Community 2022.*

Criamos aquela mesma estrutura de englobar dois projetos dentro de uma solution onde o projeto de testes aponta pro projeto de desenvolvimento. Lembrando que o de desenvolvimento não pode apontar para o de testes, porque não iremos usar nada do ambiente de testes no de desenvolvimento.

#### Parte 2 - Criando as funções da calculadora

- Criação dos testes falhos
- Aplicando as regras de negócio nos testes
- Boa prática na criação dos testes

##### Refinamento Inicial

- Um Calculadora contém Soma, Subtração, Divisão e Multiplicação e histórico de operações.

- Regras de negócios:
	- Números inteiros
	- 2 parâmetros por operação
	- Sempre retornar as últimas 3 operações do histórico

Antes de codificarmos os testes, precisamos definir a estrutura básica da nossa classe, e retornar valores padrão, neste caso, como é `int` iremos retornar zero:
```C#
namespace NewTalents
{
    public class Calculadora
    {
        public int Somar(int val1, int val2)
        {
            return 0;
        }

        public int Subtrair(int val1, int val2)
        {
            return 0;
        }

        public int Multiplicar(int val1, int val2)
        {
            return 0;
        }

        public int Dividir(int val1, int val2)
        {
            return 0;
        }

        public List<string> Historico()
        {
            return new List<string>();
        }
    }
```

---
##### Criando o primeiro teste de função - somar

É a mesma porra lá
```C#
public class CalculadoraTest
{
    [Theory]
    [InlineData(1, 2, 3)]
    [InlineData(4, 5, 9)]
    public void Test1(int val1, int val2, int resultadoEsperado)
    {
        Calculadora calc = new Calculadora();

        int resultadoCalculadora = calc.Somar(val1, val2);

        Assert.Equal(resultadoEsperado, resultadoCalculadora);
    }
}
```

---
##### Criando as outras funções básicas da calculadora

> [!tip] Cuidado com o métodos assíncronos 
> Cuidado com o métodos assíncronos  quando for usar o `[InlineData]` porque ***pode dar pau*** quando você compartilha dados e às vezes o método acaba primeiro que o primeiro Inline, ou algo assim, sla fih, toma cuidado.

A gente basicamente faz o mesmo pra todos, e obriga os testes a darem erro a partir do valor padrão lá da nossa classe.

```C#
[Theory]
[InlineData(5, 5, 1)]
[InlineData(25, 5, 5)]
public void TesteDividir(int val1, int val2, int resultadoEsperado)
{
    Calculadora calc = new Calculadora();

    int resultadoCalculadora = calc.Dividir(val1, val2);

    Assert.Equal(resultadoEsperado, resultadoCalculadora);
}

[Fact]
public void TestarDivisaoPorZero()
{
    Calculadora calc = new Calculadora();

    Assert.Throws<DivideByZeroException>(
            () => calc.Dividir(3, 0)
        );
}
```

---
##### Desenvolvendo o histórico das operações

```C#
[Fact]
public void TestarHistorico()
{
    Calculadora calc = new Calculadora();

    calc.Somar(1, 2);
    calc.Somar(3, 4);
    calc.Somar(5, 6);
    calc.Somar(2, 9);

    var lista = calc.Historico();

    Assert.NotEmpty(calc.Historico());
    Assert.Equal(3, lista.Count);
}
```

---
##### Parte 3 - Codificando as regras de negócio

- Codificando as regras de negócio
- Executando os testes durante a codificação

- A gente fez as regras de negócio, até as implícitas. Como testar se divide por zero.

- Aí a gente termina de implementar a classe, enquanto faz os testes.
	```C#
	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Text;
	using System.Threading.Tasks;
	
	namespace NewTalents
	{
	    public class Calculadora
	    {
	        private List<string> listaHistorico;
	
	        public Calculadora()
	        {
	            listaHistorico = new List<string>();
	        }
	
	        public int Somar(int val1, int val2)
	        {
	            int res = val1 + val2;
	
	            listaHistorico.Insert(0, "Res: " + res);
	
	            return res;
	        }
	
	        public int Subtrair(int val1, int val2)
	        {
	            int res = val1 - val2;
	
	            listaHistorico.Insert(0, "Res: " + res);
	
	            return res;
	        }
	
	        public int Multiplicar(int val1, int val2)
	        {
	            int res = val1 * val2;
	
	            listaHistorico.Insert(0, "Res: " + res);
	
	            return res;
	        }
	
	        public int Dividir(int val1, int val2)
	        {
	            int res = val1 / val2;
	
	            listaHistorico.Insert(0, "Res: " + res);
	
	            return res;
	        }
	
	        public List<string> Historico()
	        {
	            listaHistorico.RemoveRange(3, listaHistorico.Count - 3);
	            return listaHistorico;
	        }
	    }
	}
	
	```

---
#### Refatoração do código

