# O comando `awk`

O `awk` é uma linguagem muito útil para processar ficheiros semi-estruturados ou estruturados através da manipulação de padrões (*patterns*) especificados através de expressões regulares (*regular expressions*), o que o torna muito versátil.
O comando `awk` permite-nos manipular dados e texto linha a linha, permitindo a pesquisa, formatação e cálculos, entre outros. É especialmente útil para trabalhar com ficheiros estruturados, como `.csv`.

A sua sintaxe geral é a seguinte:

```bash
awk 'condição {ação}' ficheiro
```

- `condição` →  Define a condição que, se for verdadeira, executa a ação
- `ação` → O que fazer se condição for verdadeira

!!! note "Exemplo `awk`"
    ```bash
    awk '{print $1, $3}' ficheiro.txt
    ```
    O `awk` divide cada linha em campos, que são numerados a partir de `$1` (primeiro campo), `$2` (segundo campo) e assim por diante. No exemplo acima, se o `ficheiro.txt` for constituído por:

    ```bash
    João 30 Lisboa
    Maria 25 Porto
    Pedro 22 Coimbra
    ```

    O comando `awk` produziria o resultado:

    ```bash
    João Lisboa
    Maria Porto
    Pedro Coimbra
    ```

    **Nota - Delimitadores de campo:** Por defeito, o `awk` usa espaços ou *tabs* como delimitadores de campos, mas é possível definir outro delimitador (e.g., `,` ou `;`) utilizando a opção `-F`. Por exemplo, se o arquivo estiver separado por vírgulas (e.g., `.csv`), podemos fazer:

    ```bash
    awk -F, '{print $1, $2}' ficheiro.csv
    ```

## Outras operações com o `awk`

!!! tip "Filtragem com condições"
    É possivel usar o `awk` para imprimir apenas as linhas que atendam a um determinado critério. Por exemplo, para imprimir as linhas onde o valor do primeiro campo é `"Maria"`:
    ```bash
    awk '$1 == "Maria" {print}' ficheiro.txt
    ```

    Neste, caso a saída seria:
    ```bash
    Maria 25 Porto
    ```

!!! tip "Somar valores de uma coluna"
    O `awk` também pode ser usado para realizar operações matemáticas. Por exemplo:
    ```bash
    awk '{soma += $2} END {print soma}' ficheiro.txt
    ```
    Este comando soma os valores na segunda coluna e imprime o resultado, neste caso seria `77`. Aqui, `soma += $2` vai somando os valores da coluna 2 e a instrução `END {print soma}` imprime o total após serem processadas todas as linhas.

!!! tip "Combinar condições"
    Por exemplo, para imprimir as linhas em que o segundo campo (idade) seja maior que 20:

    ```bash
    awk '$2 > 20 {print}' ficheiro.txt
    ```

!!! tipo "Usar variáveis no `awk`"
    É possível usar o `awk` para fazer cálculos ou manipular valores, tal como calcular a média de idades no ficheiro:
    ```bash
    awk '{soma += $2; count++} END {print soma/count}' ficheiro.txt
    ```
    Aqui, `count` conta o número de linhas e soma acumula o valor do segundo campo (idade). A média é calculada na parte `END {print soma/count}`.

## `BEGIN` e `END` no `awk`

O `awk` processa as linhas de um arquivo de texto **linha a linha**. A estrutura `BEGIN` e `END` permite-nos executar  código **antes** ou **depois** de processar o ficheiro. Como vimos nos exemplos acima, não é necessário usar o `BEGIN` se não precisarmos de algo a ser executado antes de processarmos o conteúdo do ficheiro. O **`END`** é útil quando queremos executar algum código **após** o processamento de todas as linhas (por exemplo, imprimir a soma, uma contagem, etc.)

O bloco `BEGIN` é executado **antes** de o `awk` processar as linhas do ficheiro. É útil quando queremos fazer configurações iniciais, como **definir variáveis** ou imprimir algo:

```bash
awk 'BEGIN {print "Início do script"} {print} END {print "Fim do script"}' ficheiro.txt
```

Este comando imprime a mensagem `"Início do script"` antes de começar a processar as linhas do ficheiro. Em seguida, imprime todas as linhas do ficheiro com `{print}` e no final imprime a mensagem `"Fim do script"`, no final do processamento de todas as linhas.

Por sua vez, o bloco `END` é executado **após** o processamento de todas as linhas e é útil para realizar alguma ação **final**, como por exemplo, imprimir resultados agregados ou mensagens após processar todas as linhas, como já vimos anteriormente:

```bash
awk 'BEGIN {print "Início do processamento"} {print $1, $2} END {print "Processamento completo"}' ficheiro.txt
```
Se não precisarmos de executar nada antes de processar as linhas, podemos omitir o bloco `BEGIN`. Em vez disso, basta ter a parte do `END` para realizar uma ação após o processamento do ficheiro:

```bash
awk '{soma += $2} END {print "Soma:", soma}' ficheiro.txt
```

Também é possível usar apenas o `BEGIN` para configurações ou inicializações antes de começar o processamento de dados. Por exemplo, podemos definir o separador de campos como `,` e imprimir uma linha de cabeçalho:

```bash
awk 'BEGIN {FS=","; print "Cabeçalho: Nome, Idade, Cidade"}'
```

## Variáveis úteis no `awk`
O `awk` trabalha com **registos** (linhas) e **campos** (colunas) e algumas variáveis predefinidas facilitam o trabalho:

- **`FS`**: Define o delimitador dos campos na entrada (por defeito usa o espaço)
- **`OFS`**: Define o delimitador entre campos na saída (por defeito é o espaço)
- **`RS`**: Define o separador de linhas na entrada (por defeito é uma linha nova `\n`)
- **`ORS`**: Define o separador de linhas na saída (por defeito é uma linha nova `\n`)
- **`NF`**: Número de campos na linha atual
- **`NR`**: Número total de linhas processados
- **`$0`**: A linha inteira, e.g. `{print $0}` equivale a `{print}`
- **`$1`, `$2`, ..., `$NF`**: Campos individuais (por exemplo, `$1` é o primeiro campo, `$2` é o segundo, etc.)
- **`$NF`**: O último campo da linha


## **Uso avançado do `awk`**
O `awk` é uma ferramenta poderosa, não só para processamento de texto simples, mas também para fazer operações mais complexas como condicionais (`if-else`) e loops (e.g. `for`). Alguns exemplos encontram-se abaixo:


```bash
awk '{if ($2 > 50) {print $1 " é maior que 50"} else {print $1 " é menor ou igual a 50"}}' ficheiro.txt
awk 'BEGIN {for (i=1; i<=5; i++) print "Valor de i:", i}' 
awk '{sum += $2} END {print "Soma:", sum; print "Média:", sum/NR}' ficheiro.txt
awk '{if ($1 ~ /^J/) print $1 " começa com J"}' ficheiro.txt
awk '{if ($1 == "João" && $2 > 20) print $0; else if ($1 == "Maria" || $2 < 25) print $0}' ficheiro.txt
```