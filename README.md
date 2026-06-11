## Uso de IA para geração de cenários de teste

### Função escolhida

`dividir(a, b)`

### Prompt utilizado

```text
Atue como um professor de Teste de Software.

Tenho a seguinte função Python:

def dividir(a, b):
    return a / b

Quero criar testes unitários usando unittest.

Liste cenários de teste para essa função, incluindo:
- divisão exata;
- divisão com resultado decimal;
- divisão de número negativo;
- divisão de zero por outro número;
- divisão por zero.

Para cada cenário, informe:
- nome do cenário;
- entrada;
- resultado esperado;
- tipo do cenário: caso normal, caso de borda ou caso de erro.

Não gere código ainda.
```

### Cenários sugeridos pela IA

| ID  | Cenário                  | Entrada           | Resultado esperado  | Tipo          |
|-----|--------------------------|-------------------|---------------------|---------------|
| T01 | Divisão exata            | `dividir(10, 2)`  | `5`                 | caso normal   |
| T02 | Divisão com decimal      | `dividir(5, 2)`   | `2.5`               | caso normal   |
| T03 | Divisão com negativo     | `dividir(-10, 2)` | `-5`                | caso normal   |
| T04 | Zero dividido por número | `dividir(0, 5)`   | `0`                 | caso de borda |
| T05 | Divisão por zero         | `dividir(10, 0)`  | `ZeroDivisionError` | caso de erro  |

### Análise dos cenários

Todos os 5 cenários sugeridos pela IA foram aceitos, pois:

- **T01, T02 e T03** cobrem os usos normais da função com diferentes tipos de resultado.
- **T04** é um caso de borda importante: zero no numerador é válido e deve retornar zero.
- **T05** é o caso de erro esperado: dividir por zero gera `ZeroDivisionError` no Python.

Nenhum cenário foi removido. A IA não inventou comportamentos inexistentes na função e todos os resultados esperados estavam corretos.

### Código final dos testes

```python
def test_dividir_com_varios_casos(self):
    casos = [
        (10, 2, 5),
        (5, 2, 2.5),
        (-10, 2, -5),
        (0, 5, 0),
    ]
    for a, b, esperado in casos:
        with self.subTest(a=a, b=b):
            self.assertEqual(dividir(a, b), esperado)

def test_dividir_por_zero(self):
    with self.assertRaises(ZeroDivisionError):
        dividir(10, 0)
```

### Resultado da execução

```bash
python -m unittest discover
```

Saída obtida:

```
------------------------------------------------------------------------
Ran 8 tests in 0.002s

OK
```