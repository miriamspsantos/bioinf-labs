# O comando `sed`

O `sed` (*s*tream *ed*itor) é um comando muito útil para **processamento de texto**. O `sed` permite-nos ler os dados de um ficheiro ou a partir da entrada padrão (*stdin*), modificá-los conforme as instruções fornecidas e enviar o resultado para a saída padrão (*stdout*). É ideal para manipular ficheiros grandes, automatizar tarefas repetitivas e integrar pipelines de análise de dados.

A sua sintaxe geral é a seguinte:

```bash
sed [opções] 'script' ficheiro
```

!!! note "Exemplo `sed`"
    ```bash
    echo "Olá, Mundo!" | sed 's/Mundo/Terra/'
    ```
    Neste exemplo, o comando `echo "Olá Mundo!` imprime a string `"Olá, Mundo!"`. Com o pipe, é aplicado o comando `sed 's/Mundo/Terra/'` que substitui a palavra `"Mundo"` por `"Terra"`. A saída final será: `Olá, Terra!`

    No caso, o script `s/Mundo/Terra/` é uma expressão de substituição onde `s` significa substituição, `Mundo` é o texto a ser substituído e `Terra` é o novo texto.


## Opções úteis do `sed`

- `-e` → Permite especificar vários comandos diretamente na linha de comandos
- `-f` → Permite aplicar os comandos definidos num ficheiro
- `-i` → Edita diretamente o ficheiro de entrada

Alguns exemplos são:

```bash
echo "Olá, Mundo!" | sed -e 's/Mundo/Terra/' -e 's/Olá/Oi/'    # Substitui "Mundo" por "Terra" e "Olá" por "Oi"
echo "Olá, Mundo!" | sed -f comandos.sed                       # Aplica os comandos definidos em "comandos.sed" (por exemplo, "comandos.sed" pode conter `s/Mundo/Terra/`)
sed -i 's/Mundo/Terra/' texto.txt                              # Edita directamente o ficheiro texto.txt
```

## Substituição de Texto

O `sed` é amplamente usado para substituir texto dentro de ficheiros.

```bash
sed -e 's/antigo/novo/' ficheiro.txt
```
Neste caso, substitui a primeira ocorrência de "antigo" por "novo" **em cada linha**. Se uma linha tiver várias ocorrências da palavra "antigo", apenas a primeira será substituída. Para substituir **todas as ocorrências** podemos usar o comando:

```bash
sed -e 's/antigo/novo/g' ficheiro.txt
```

Por exemplo, podemos também usar o `sed` para converter todas as ocorrências de `chr` em `CHR` num ficheiro .bed:

```bash
sed -e 's/chr/CHR/g' genes.bed
```

## Pesquisa de Padrões
Tal como o `grep`, o `sed` pode ser usado para pesquisar e imprimir as linhas que contêm um padrão. Por exemplo, para mostrar apenas as linhas que correspondem ao padrão `"Mundo"` poderíamos fazer:

```bash
sed -n '/Mundo/p' ficheiro.txt
```

- `-n` → Impede que o `sed` imprima todas as linhas, só irá imprimir as que forem especificadas
- `/Mundo/` → A expressão regular que define o padrão que queremos pesquisar
- `p` → Instrução para imprimir as linhas que correspondem ao padrão

## Extração de Linhas
Também podemos **extrair linhas específicas** com o `sed`. Por exemplo, se quisermos extrair especificamente a linha 3 de um ficheiro, podemos usar o comando:

```bash
sed -n '3p' ficheiro.txt
```

- `-n` → Impede que o `sed` imprima todas as linhas
- `'3p'` → Indica ao `sed` para **imprimir** (`p`) apenas a linha 3

Para extrair um intervalo de linhas, por exemplo, da linha 2 à linha 4, podemos usar:

```bash
sed -n '2,4p' ficheiro.txt
```
Neste caso, `'2,4p'` indica ao `sed` para imprimir as linhas do intervalo de 2 a 4.

Podemos ainda selecionar linhas com um **intervalo regular**. Por exemplo, a sintaxe `1~4p` no `sed` indica que devemos começar na linha 1 e em seguida, extrair a 4ª linha depois dela. Genericamente, o formato `X~Yp` significa: **começar na linha `X` e imprimir a cada `Y` linhas**.

Por exemplo:

```bash
sed -n '1~4p' ficheiro.txt
```
A sintaxe `1~4p` diz ao `sed` que queremos começar na linha 1 e extrair de 4 em 4 linhas. Se o conteúdo do `ficheiro.txt` for:

```bash
Linha 1
Linha 2
Linha 3
Linha 4
Linha 5
Linha 6
Linha 7
Linha 8
```

O comando produz o efeito:
```
Linha 1
Linha 5
```