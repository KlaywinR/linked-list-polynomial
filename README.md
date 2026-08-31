# Projeto Polinômio — Estrutura de Dados Lineares

[![Python](https://img.shields.io/badge/python-3.8%2B-blue)]()
[![Tests](https://img.shields.io/badge/tests-passing-brightgreen)]()
[![License](https://img.shields.io/badge/license-MIT-lightgrey)]()

Implementação de uma estrutura de dados para representação e manipulação de **polinômios univariados** utilizando **lista encadeada**, desenvolvida como projeto da disciplina de Estrutura de Dados Lineares.

Cada monômio `aᵢ·x^j` é armazenado como um nó da lista, mantida sempre ordenada de forma decrescente pelo grau — permitindo operações eficientes de adição, subtração, multiplicação, avaliação e simplificação.

```
Head -> [<null>] -> [-7|5] -> [2|3] -> [5.3|1] -> [-2|0] -> null
                     (coeficiente | grau)
```

## Índice

- [Funcionalidades](#funcionalidades)
- [Estrutura do projeto](#estrutura-do-projeto)
- [Instalação](#instalação)
- [Como usar](#como-usar)
- [Formato do arquivo de entrada](#formato-do-arquivo-de-entrada)
- [Testes](#testes)
- [Detalhes de implementação](#detalhes-de-implementação)
- [Licença](#licença)

## Funcionalidades

| Operação          | Método / operador Python             |
|-------------------|----------------------------------------|
| Grau              | `p.grau()`                             |
| Tamanho           | `p.tamanho()`                          |
| Adição            | `p + q`                                |
| Subtração         | `p - q`                                |
| Multiplicação     | `p * q`                                |
| Avaliação em `x`  | `p.avaliar(x)`                         |
| Exibição textual  | `str(p)`                               |
| Simplificação     | `p.simplificar()` (automática)         |

A simplificação — fusão de termos de mesmo grau e remoção de coeficientes nulos — é aplicada automaticamente ao final da construção e de toda operação aritmética, garantindo que o resultado já saia normalizado.

Requer apenas **Python 3.8+**, sem dependências externas.

## Estrutura do projeto

```
projeto_polinomio/
├── src/                       # Código-fonte (pacote Python)
│   ├── __init__.py             # API pública do pacote
│   ├── termo_polinomio.py      # Classe TermoPolinomio (nó: coeficiente + grau)
│   ├── polinomio.py            # Classe Polinomio (todas as operações)
│   └── file_processor.py       # Leitura e execução de arquivos de comandos
├── tests/                      # Testes unitários (unittest)
│   ├── test_polinomio.py
│   └── test_file_processor.py
├── data/                       # Arquivos de entrada de exemplo
│   └── entrada_exemplo.txt
├── main.py                     # Programa principal / demonstração
└── README.md
```

## Instalação

```bash
git clone <url-do-repositorio>
cd projeto_polinomio
```

Não há dependências externas — nenhum passo adicional de instalação é necessário.

## Como usar

```bash
# Demonstração completa (todas as operações + processamento de um arquivo de entrada)
python3 main.py

# Processar um arquivo de entrada específico
python3 main.py caminho/para/arquivo.txt
```

### Uso programático

```python
from src import Polinomio

p = Polinomio([(-7, 5), (2, 3), (5.3, 1), (-2, 0)])   # -7x^5 + 2x^3 + 5.3x - 2
q = Polinomio([(6, 4), (8, 1), (-2, 0)])                # 6x^4 + 8x - 2

p.grau()        # 5
p.tamanho()     # 4
p.avaliar(2)    # -199.4
p + q            # -7x^5 + 6x^4 + 2x^3 + 13.3x - 4
p - q            # -7x^5 - 6x^4 + 2x^3 - 2.7x
p * q            # -42x^9 + 12x^7 - 56x^6 + ...
```

## Formato do arquivo de entrada

O módulo `src/file_processor.py` interpreta arquivos com comandos e polinômios "achatados" (`coeficiente grau coeficiente grau ...`). Por exemplo, `-3 5 6 3 -7 1 8 0` representa `-3x^5 + 6x^3 - 7x + 8`.

| Comando           | Linhas de dados consumidas em seguida        |
|-------------------|-----------------------------------------------|
| `+` `-` `*`       | 2 linhas (dois polinômios)                     |
| `g/G` `t/T` `p/P` | 1 linha (um polinômio)                         |
| `a/A`             | 1 linha com `x`, depois 1 linha com o polinômio |

## Testes

Suíte de testes unitários com cobertura de construção, ordenação, operações aritméticas, simplificação e processamento de arquivos:

```bash
python3 -m unittest discover -s tests -v
```

## Detalhes de implementação

- **Estrutura de dados:** lista encadeada simples com nó-cabeça sentinela, ordenada de forma decrescente pelo grau.
- **Simplificação automática:** aplicada ao final da construção, adição, subtração e multiplicação, garantindo que qualquer resultado retornado já esteja normalizado (sem termos de grau repetido ou coeficientes nulos).
- **Comparação de ponto flutuante:** uso de tolerância (epsilon) para tratar coeficientes numericamente próximos de zero como nulos.

## Licença

Este projeto é distribuído sob a licença MIT. Sinta-se à vontade para utilizá-lo, adaptá-lo e distribuí-lo.
