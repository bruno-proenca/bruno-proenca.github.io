# Eletrônica Digital 1 - revisão para a P1

Data da revisão: 07/10/2026

## Conteúdos da prova

- Multiplexadores e demultiplexadores
- Codificadores e decodificadores
- Circuitos aritméticos: somadores e subtratores
- Registradores de deslocamento
- Revisão complementar: latchs e flip-flops

## Prioridade indicada pelo professor

- MUX/Demux: questões 1, 4, 6 e 7 da lista.
- Latchs: revisar todos os conceitos da lista.
- Flip-flops: revisar tabelas e diagramas de tempo.
- Codificadores/decodificadores: questões 4, 7 e 8.
- Somador/subtrator: questão 8, adaptada para 3 bits.
- Registradores: questão 4.

## 1. Multiplexadores e demultiplexadores

Um MUX seleciona uma entrada de dados usando as linhas de seleção. Um demux faz o contrário: envia uma entrada para uma única saída escolhida.

### Questão 1 da lista de MUX

Pela tabela, usando um MUX 4:1 com `A` e `B` como seleção:

| Seleção | Entrada |
|---|---|
| `AB = 00` | `D0 = 0` |
| `AB = 01` | `D1 = 1` |
| `AB = 10` | `D2 = C` |
| `AB = 11` | `D3 = C̅` |

### MUX de 32 canais usando MUX 8:1

Usar quatro MUX 8:1 no primeiro estágio e um MUX 8:1 no segundo.

- Os três bits menos significativos são ligados às seleções dos quatro MUX iniciais.
- Os quatro resultados vão para `I0`, `I1`, `I2` e `I3` do MUX final.
- Os dois bits mais significativos escolhem qual grupo de oito será usado.
- As entradas restantes do MUX final devem ser fixadas em nível lógico definido.

### Questão 6: demux da figura

Considerando `D = 1` e habilitação ativa em nível baixo, os intervalos `f, e, d, c, b, a` ativam:

| Intervalo | `S2 S1 S0` | Saída |
|---|---:|---:|
| `f` | `111` | 7 |
| `e` | `010` | nenhuma: circuito desabilitado |
| `d` | `001` | 1 |
| `c` | `101` | 5 |
| `b` | `110` | 6 |
| `a` | `000` | 0 |

### Questão 7: MUX de 8 entradas

Na figura, `S0 = A`, `S1 = B`, `S2 = C`. As entradas de dados são:

`I0 = D`, `I1 = 0`, `I2 = 1`, `I3 = 0`, `I4 = D̅`, `I5 = 0`, `I6 = 0`, `I7 = 0`.

Portanto:

```text
Z = C̅ B̅ A̅ D + C̅ B A̅ + C B̅ A̅ D̅
```

### Função com MUX 8:1

Para `Z = Σm(0, 3, 5, 6, 9, 10, 12, 15)`, usando `A, B, C` como seleção e `D` como variável de dados:

| Entrada | Valor |
|---|---|
| `I0` | `D̅` |
| `I1` | `D` |
| `I2` | `D` |
| `I3` | `D̅` |
| `I4` | `D` |
| `I5` | `D̅` |
| `I6` | `D̅` |
| `I7` | `D` |

## 2. Codificadores e decodificadores

### Codificador decimal/BCD prioritário

Nas entradas ativas em nível baixo, `0` significa acionada e `1` significa inativa. Se várias entradas estiverem acionadas, vence a de maior prioridade.

| Decimal | BCD (`D C B A`) |
|---:|---:|
| 0 | 0000 |
| 1 | 0001 |
| 2 | 0010 |
| 3 | 0011 |
| 4 | 0100 |
| 5 | 0101 |
| 6 | 0110 |
| 7 | 0111 |
| 8 | 1000 |
| 9 | 1001 |

Para resolver o diagrama de tempo, em cada intervalo procure as entradas que estão em `0`, escolha a de maior valor e converta para BCD.

### Questões 7 e 8

Para:

```text
F(X,Y,Z,W) = Σm(2, 5, 8, 9, 11, 15)
```

Com decodificador de saídas ativas em nível baixo:

```text
F = NAND(Y̅2, Y̅5, Y̅8, Y̅9, Y̅11, Y̅15)
```

Com decodificador de saídas ativas em nível alto:

```text
F = Y2 + Y5 + Y8 + Y9 + Y11 + Y15
```

Regra: saída ativa baixa normalmente exige NAND; saída ativa alta exige OR.

## 3. Somador/subtrator de 3 bits

Use três Somadores Completos em cascata, do bit menos significativo para o mais significativo.

Para uma entrada de controle `M`:

```text
B'i = Bi XOR M
C0 = M
Si = Ai XOR B'i XOR Ci
Ci+1 = Ai B'i + Ci(Ai XOR B'i)
```

- `M = 0`: `A + B`
- `M = 1`: `A + B̅ + 1 = A - B`

Na subtração, `C3 = 0` indica borrow; `C3 = 1` indica que não houve borrow.

## 4. Registradores de deslocamento

Para o registrador da questão 4:

```text
Q0+ = I
Q1+ = Q0
Q2+ = Q1
Q3+ = Q2
```

A cada pulso de clock, todos os flip-flops atualizam simultaneamente.

Exemplo com entrada serial `1011`, começando em `0000` e mostrando `Q0 Q1 Q2 Q3`:

| Pulso | Entrada | Estado |
|---:|---:|---:|
| Inicial | - | 0000 |
| 1 | 1 | 1000 |
| 2 | 0 | 0100 |
| 3 | 1 | 1010 |
| 4 | 1 | 1101 |

Assim, lendo da saída final para a entrada, o valor armazenado é `1011`.

- Escrita serial de 4 bits: 4 pulsos.
- Leitura serial de 4 bits: 4 pulsos.
- Leitura paralela: os quatro bits aparecem simultaneamente, sem pulsos adicionais.

## 5. Latchs

### Latch RS-NAND

Entradas ativas em nível baixo:

| S̅ | R̅ | Ação |
|---:|---:|---|
| 1 | 1 | mantém |
| 0 | 1 | Set, `Q = 1` |
| 1 | 0 | Reset, `Q = 0` |
| 0 | 0 | estado proibido |

### Latch RS-NOR

Entradas ativas em nível alto:

| S | R | Ação |
|---:|---:|---|
| 0 | 0 | mantém |
| 1 | 0 | Set |
| 0 | 1 | Reset |
| 1 | 1 | estado proibido |

Latch é sensível ao nível: enquanto o enable está ativo, a saída pode acompanhar a entrada.

## 6. Flip-flops

### Flip-flop JK

| J | K | Próximo estado |
|---:|---:|---|
| 0 | 0 | mantém |
| 0 | 1 | reset |
| 1 | 0 | set |
| 1 | 1 | alterna |

O JK elimina o estado proibido do RS.

### Flip-flop D

```text
Q+ = D
J = D
K = D̅
```

Aplicação: armazenamento de dados.

### Flip-flop T

```text
Q+ = T XOR Q
J = K = T
```

Aplicação: contadores e divisores de frequência.

Diferença essencial:

- latch: sensível ao nível;
- flip-flop: sensível à borda;
- borda de subida: `0 → 1`;
- borda de descida: `1 → 0`.

## Pegadinhas finais

- Bolinha ou barra geralmente indica lógica ativa baixa.
- Confira sempre qual bit é MSB e qual é LSB.
- Em MUX, primeiro descubra qual entrada foi selecionada.
- Em codificador prioritário, vence a maior prioridade.
- Em subtração por complemento de 2, não esqueça `C0 = 1`.
- Em registradores, os bits mudam juntos no clock.
- Em flip-flops, a saída muda apenas na borda ativa.

## Estratégia rápida de revisão

1. Memorizar as tabelas RS, JK, D e T.
2. Refazer a questão 1 de MUX.
3. Refazer a questão 7 de decodificadores nos casos ativo-baixo e ativo-alto.
4. Desenhar três Somadores Completos em cascata.
5. Fazer a tabela de deslocamento `1011`.
6. Revisar as diferenças entre latch e flip-flop.
