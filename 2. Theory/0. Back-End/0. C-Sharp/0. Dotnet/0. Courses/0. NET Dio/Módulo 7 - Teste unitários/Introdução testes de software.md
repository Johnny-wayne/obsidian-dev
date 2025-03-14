
Existem vários tipos de testes de software: unitários, integração, regressivo, segurança, etc...
	Tudo visando a qualidade do código.

Os testes são fundamentais para garantir a qualidade e o correto funcionamento de um software.
	Às vezes funciona do jeito que vc pensou, mas o cliente testa de outro, e dá ruim.

Serve principalmente para validar se o que foi construído. está atendendo ao que se é esperado.

---
#### O que é um teste unitário?

Cada etapa do software, vai ter alguém responsável por fazer algum tipo de teste, nesse caso, é o próprio desenvolvedor.

Teste unitário (ou teste de unidade) são testes realizados diretamente no código fonte, buscando testar a menor unidade de código possível, através de cenários que podem ocorrer no sistema.

- *Exemplo:*
	Um usuário do sistema só é cadastrado se possuir um CPF e um e-mail válido. Caso contrário, retornará um erro indicando o que está errado.
	
	Possíveis casos de teste:
	- Usuário com todos os dados válidos
	- Usuário com CPF inválido
	- Usuário com e-mail inválido

É importante testar cenários positivos também.

---
#### Vantagem dos testes

A maior vantagem é a **Qualidade**

- Garante que a alteração não tenha impactos no sistema
- Menos bugs
- Maior confiança de que suas classes e métodos funcionam
- Prevenir problemas futuros

---
#### Frameworks de teste

- MSTest
- NUnit
- **xUnit** - é o que estaremos usando

Arquitetura dos testes:
![[Pasted image 20241112194306.png]]
- A solution junta os dois `.csproj` com um deles sendo de testes que referencia o outro projeto dentro de seu `.csproj`

---
#### Criando nosso projeto

Ele basicamente, criou os projetos, criando uma pasta pra cada um, mudando o diretório no terminal, e criando dentro das pastas, os projetos:
- `dotnet new console`
- `dotnet new xunit`

Aí depois ele usou aquela extensão de solution `vscode-solution-explorer` pra criar a solution, adicionar os `.csproj` dentro dela e também referenciar o `.csproj` da aplicação dentro do `.csproj`  de testes.

Pra referenciar, é só clicar com o botão direito que ele dá um monte de opções.

---
#### Implementando a classe calculadora

Basicamente ele cria uma pasta chamada `Services` cria uma classe `CalculadoraImp` de "Implementação".

```C#
namespace Calculadora.Services
{
    public class CalculadoraImp
    {
        public int Somar(int num1, int num2)
        {
            return num1 + num2;
        }
    }
}
```

E depois implementa essa classe no `Program.cs`
```C#
using Calculadora.Services;

CalculadoraImp c = new CalculadoraImp();

int num1 = 5;
int num2 = 10;

Console.WriteLine($"{num1} + {num2} = {c.Somar(num1, num2)}");
```

---
#### Criando a classe de teste

Deve existir um teste para cada classe.
`Calculadora.cs` -> `CalculadoraTests.cs`

Se você for ver, o cenário de testes, é praticamente um método. Um método que a gente vai validar esse cenário.
```C#
namespace CalculadoraTestes;

public class UnitTest1
{
    [Fact]
    public void Test1()
    {

    }
}
```

- Cada método, vai ter esse atributo chamado `[Fact]` que significa que esse método é um cenário de testes e deve ser validado de acordo.

Nós temos algumas etapas para podermos criar nosso teste unitário. Temos três conceitos:
- Arrange *(monta)*
	- Serve para montarmos nosso cenário. Disponibilizarmos os números e preparamos o cenário.
- Act *(tenta)*
	- Agora que temos nosso cenário, precisamos executar a ação, no caso, somar
- Assert *(vê se tá certo)*
	- Isso é pra validar se tudo tem o resultado esperado.

```C#
using Calculadora.Services;

namespace CalculadoraTestes;

public class CalculadoraTestes
{
	// aqui chamou a classe que implementamos lá atrás
    private CalculadoraImp _calc;
	
	// Aqui definiu um construtor
    public CalculadoraTestes()
    {
        _calc = new CalculadoraImp();
    }

    [Fact]
    public void TesteSoma()
    {
        // Arrange
        // Act
        // Assert
    }
}
```

---
#### Implementando o teste unitário

```C#
using Calculadora.Services;

namespace CalculadoraTestes;

public class CalculadoraTestes
{
    private CalculadoraImp _calc;

    public CalculadoraTestes()
    {
        _calc = new CalculadoraImp();
    }

    [Fact]
    public void TesteSoma()
    {
        // Arrange
        int num1 = 5;
        int num2 = 10;

        // Act
        int resultado = _calc.Somar(num1, num2);

        // Assert
        Assert.Equal(15, resultado);
    }
}
```

- `Assert` - Essa é a classe chave da validação do resultado.
	- Ela tem diversos métodos, nesse caso, estamos comparando se o resultado retorna 15.

Para testarmos, é só mudar pro diretório de testes, e dar um:
- `dotnet test`

---
#### Implementando validações de string

Novo arquivo:
`Services/ValidacoesString`
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;

namespace Calculadora.Services
{
    public class ValidacoesString
    {
        public int ContarCaracteres(string texto)
        {
            int num = texto.Length;
            return num;
        }
    }
}
```

Novo teste:
`ValidacoesStringTests.cs` 
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Calculadora.Services;
using Xunit;

namespace CalculadoraTestes
{
    public class ValidacoesStringTests
    {
        private ValidacoesString _validacoes;

        public ValidacoesStringTests()
        {
            _validacoes = new ValidacoesString();
        }

        [Fact]
        public void DeveContar3CaracteresEmOlaERetornar3()
        {
            string stringContar = "Olá";

            int resultado = _validacoes.ContarCaracteres(stringContar);

            Assert.Equal(3, resultado);
        }
    }
}
```

Fiz suavão isso aí

---
#### Verificando se um número é par

```C#
namespace Calculadora.Services
{
    public class CalculadoraImp
    {
        public int Somar(int num1, int num2)
        {
            return num1 + num2;
        }
		
		// Adicionamos um novo método
        public bool EhPar(int num)
        {
            return num % 2 == 0;
        }
    }
}
```

E testamos ele:
`CalculadoraTests.cs`
```C#
[Fact]
public void DeveVerificarSe4ehParERetornarVerdadeiro()
{
	int numero = 4;
	
	bool resultado = _calc.EhPar(numero);
	
	// Neste caso, usar Equal não é recomendado
	// aqui é tipo um "É true? Esse resultado aí"
	Assert.True(resultado);
}
```

---
#### Utilizando o Theory
*O cara disse que a gente tá usando um Queue*

E se precisássemos, nesse caso de verificar se um número é par, utilizar vários números? Não só o 4, mas o 2, 6, 8, 10 e etc?

A gente não ia fazer um teste pra cada né.

A gente faz desse jeito:
```C#
    [Theory]
    [InlineData(2)] //acaba sendo 5 cenário
    [InlineData(4)]
    [InlineData(6)]
    [InlineData(8)]
    [InlineData(10)] // acaba sendo um laço de repetição
    public void DeveVerificarSeOsNumerosSaoParesERetornarVerdadeiro(int numero)
    {
        // Act
        bool resultado = _calc.EhPar(numero);
        // Assert
        Assert.True(resultado);
    }
```

- Tira o `[Fact]`
- Adiciona o `[Theory]` - conjunto de cenários que vão passar pelo menos teste
- Coloca `[InlineData(numero que vamos usar pra testar)]` ele se passa como valor do parâmetro do método de teste.

---
#### Refatorando o método de teste

Nós podemos passar uma lista como parâmetro também para os testes.

Dá pra fazer desse jeitão:
```C#
[Theory]
// Dá pra colocar a lista na mesma InlineData
// Só tamo usando assim pra mostrar que dá
[InlineData(new int[] {2, 4})]
[InlineData(new int[] {6, 8, 10})]
public void DeveVerificarSeOsNumerosSaoParesERetornarVerdadeiro(int[] numeros)
{
	// Act / Asserts
	foreach (var item in numeros)
	{
		Assert.True(_calc.EhPar(item));
	}

}
```

MAS DÁ PRA MELHORAR!
```C#
[Theory]
[InlineData(new int[] {2, 4})]
[InlineData(new int[] {6, 8, 10})]
public void DeveVerificarSeOsNumerosSaoParesERetornarVerdadeiro(int[] numeros)
{
	// Act / Asserts
	Assert.All(numeros, num => Assert.True(_calc.EhPar(num)));
}
```
#pesquisar O que krls é essa lambda expression em C# nesse contexto
