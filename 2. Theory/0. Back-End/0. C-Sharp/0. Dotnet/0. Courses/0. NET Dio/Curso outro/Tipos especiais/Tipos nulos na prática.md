
```C#
bool? desejaReceberEmail = null;

if (desejaReceberEmail.HasValue && desejaReceberEmail.Value)
{
	Console.WriteLine("O usuário optou por receber e-mail.");
} 
else
{
	Console.WriteLine("O usuário não respondeu ou optou por receber e-mail.");
}
```

- `.HasValue`
	- Se possui valor diferente de nulo
- `.Value`
	- É o próprio valor, consequentemente, precisa que retorne um valor diferente de nulo ou `.HasValue = true`

Também funciona assim:
```C#
bool? desejaReceberEmail = null;

if (desejaReceberEmail.HasValue && desejaReceberEmail.Value)
{
	Console.WriteLine("O usuário optou por receber e-mail.");
} 
else
{
	Console.WriteLine("O usuário não respondeu ou optou por receber e-mail.");
}
```
