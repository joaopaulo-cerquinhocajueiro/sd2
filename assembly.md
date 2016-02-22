# ANEM

ANEM é um núcleo de microcontrolador de 16 bits desenvolvido na UFPE para fins didáticos.

## Instruções
O conjunto de instruções para este processador é dado na tabela abaixo.

| Aritméticas | Saltos | Deslocamentos | Dados |
|-------------|--------|---------------|-------|
| ADD         | J      | SHL           | LW    |
| SUB         | JAL    | SHR           | SW    |
| AND         | JR     | SAR           | LIL   |
| OR          | BEQ    | ROL           | LIU   |
| XOR         |        | ROR           |       |
| NOR         |        |               |       |
| SLT         |        |               |       |

as instruções LIL - Load Immediate Lower byte e LIU - Load Immediate Upper byte inserem um byte imediato nos registradores. Nenhuma das instruções aritméticas aceitam valores imediatos.

## Formatos de instruções

O ANEM usa 5 tipos de instuções: R, W, S, L e J.

As instruções aritméticas tem todas o mesmo opcode e são diferenciadas por um campo em separado (FUNC).Estas instruções trabalham com apenas 2 operandos como o 8086 faz: add $1,$2, significando $1 = $1+$2. São instruções tipo R.

| opcode | reg1 | reg2 | func |
|--------|------|------|------|
| 4 bits | 4 bits | 4 bits | 4 bits |

Instruções tipo W são JR, SW, LW e BEQ, tracando o campo FUNC por um offset do endereço de memória.

| opcode | reg1 | reg2 | offset |
|--------|------|------|--------|
| 4 bits | 4 bits | 4 bits | 4 bits |

As instruções de deslocamento usam uma variação do formato R, onde no local do segundo registrador acrescenta-se um campo SHAMT - SHift AMounT (tipo S):

| opcode | reg1 | shamt | func  |
|--------|------|------|--------|
| 4 bits | 4 bits | 4 bits | 4 bits |

As instruções LIL e LIU carregam um byte dentro delas e endereçam um registrador, logo seguem o seguinte formato (tipo L):

| opcode | reg1 | byte |
|--------|------|------|
| 4 bits | 4 bits | 8 bits |

Por último, as instruções de salto requerem um valor do maior tamanho possível. Como o opcode é de 4 bits, podemos colocar o endereço de 12 bits (tipo J).

| opcode | endereço |
|--------|----------|
| 4 bits | 12 bits |

## Assembler e simulador

O assembler do anem é executado pelo seguinte comando:
```
assembler.exe nome_do_arquivo
```

Onde nome_do_arquivo é o arquivo com a linguegem assembly sem a terminação .asm.

Para gerar o programa do 'multiplicador.asm' por exemplo, deve-se fazer:

```
assembler.exe multiplicador
```

O que vai gerar os seguintes arquivos:
- **multiplicador.clean** - versão sem os comentários, com todas as letras maiúsculas e sem espaços a mais, com as pseudo-instruções trocadas.
- **multiplicador.ind** - versão com os endereços de cada linha, o número da linha no código original e os endereços dos labels
- **multiplicador.bin** - versão com os comandos em binário
- **multiplicador.hex** - versão aceita pelo simulador.

Para simular é necessário colocar o arquivo `.hex` na pasta `data` do simanem com o nome modificado para `cod_maquina.hex` e executar o simanem no processing.

### Formatação
Comentários começam por `--` e vão até o fim da linha.
Linhas vazias ou apenas com comentários são ignoradas.

Registradores são de `$0` a `$15`. Lembrando que o registrador $0 é sempre zero (se tentar gravar nele outro valor não funciona).

Endereçamento indexado (registrador mais offset) é da forma `offset(registrador)`.

Labels são marcados por `nome_do_label:` no começo da linha e referenciados por `%nome_do_label%`.
