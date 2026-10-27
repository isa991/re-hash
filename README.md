# Tabela Rehash

Atividade desenvolvida para a disciplina de Resolução de Problemas Estruturados na Computação.

Implementação em Java de uma tabela hash com **endereçamento aberto** e **sondagem linear** para tratar colisões. A tabela tem um **limite de ocupação de 90%**: quando esse limite é atingido, as próximas inserções são bloqueadas, simulando o ponto em que um _rehash_ seria necessário.

## Objetivo

- Inserir 100 valores aleatórios em uma tabela de 100 posições
- Tratar colisões com sondagem linear
- Bloquear inserções quando a ocupação chega a 90%
- Mostrar estatísticas sobre colisões e posições livres

## Parâmetros

| Atributo              | Valor      | Descrição                         |
| --------------------- | ---------- | --------------------------------- |
| `tamanho`             | 100        | Quantidade de posições da tabela  |
| `qtdElementos`        | 100        | Quantidade de valores gerados     |
| `limite`              | 90         | Ocupação máxima (90% de 100)      |
| `vazio`               | -1         | Marca de posição livre            |
| Semente do `Random`   | 1090       | Deixa os resultados reproduzíveis |
| Intervalo dos valores | 0 a 100000 | `random.nextInt(100001)`          |

## Funcionamento

### 1. Inicialização

Todas as posições da tabela começam com `-1` (livres).

### 2. Função hash

$$
h(x) = x \bmod 100
$$

### 3. Tratamento de colisões (sondagem linear)

Se a posição calculada estiver ocupada, o algoritmo avança para a próxima posição, voltando ao início quando passa do fim da tabela:

$$
pos = (pos + 1) \bmod 100
$$

Cada avanço conta como **uma colisão** do elemento.

### 4. Limite de ocupação

Quando `ocupados >= 90`, o valor gerado não é inserido e o contador `bloqueados` aumenta.

### 5. Os 3 elementos que mais colidiram

São escolhidos com seleção simples: o programa percorre os elementos inseridos três vezes e, a cada vez, pega o que tem mais colisões entre os que ainda não foram escolhidos (vetor `escolhido`).

## Saída

O programa mostra:

- Quantidade de elementos inseridos
- Quantidade de inserções bloqueadas pelo limite de 90%
- Total de colisões
- Os 3 elementos que mais colidiram e quantas colisões cada um teve
- Os índices das posições livres
- O total de posições livres

## Como executar

```bash
javac TabelaHashRehash.java
java TabelaHashRehash
```
