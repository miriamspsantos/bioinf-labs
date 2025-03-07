# O comando `grep`

O comando `grep` (Global Regular Expression Print), que já abordámos no laboratório anterior, é uma ferramenta muito útil do Unix/Linux utilizada para **pesquisar padrões de texto** dentro de ficheiros ou fluxos de entrada.

A sintaxe geral do `grep` é:

```bash
grep [opções] "padrão" ficheiro
```

!!! note "Exemplo `grep`"
    O comando seguinte procura a sequência `ATCG` dentro do ficheiro `sequencias.txt` e imprime as linhas onde essa sequência aparece:
    ```bash
    grep "ATCG" sequencias.txt
    ```
## Opções úteis do `grep`

- `-i` → Ignora diferenças entre maiúsculas e minúsculas.
- `-v` → Mostra as linhas que **NÃO** correspondem ao padrão.
- `-c` → Conta o número de ocorrências.
- `-n` → Mostra os números das linhas onde há correspondências.
- `-o` → Exibe apenas as partes da linha que correspondem ao padrão.
- `-r` ou `-R` → Pesquisa recursivamente em diretorias.
- `-l` → Lista apenas os ficheiros que contêm o padrão.
- `--color` → Destaca as correspondências no output.
- `-f` → Permite que os padrões sejam lidos a partir de um ficheiro.

Alguns exemplos são:

```bash
grep -i "gene" dados.txt                # Pesquisa "gene" ignorando maiúsculas/minúsculas
grep -v "erro" log.txt                  # Mostra as linhas que NÃO contêm "erro"
grep -c "AGCT" sequencias.txt           # Conta quantas vezes "AGCT" aparece no ficheiro "sequencias.txt"
grep -n "mutação" relatório.txt         # Mostra as linhas onde "mutação" aparece no "relatório.txt"
grep -o "A[TGC]G" sequencias.txt        # Mostra apenas as correspondências do padrão "A seguido de T/G/C seguido de G"
grep -r "proteína" /home/user/dados     # Pesquisa "proteína" em todos os ficheiros dentro da pasta "dados"
```

## Expressões Regulares
Para pesquisas mais avançadas, o `grep` permite o uso de **expressões regulares** ([regex](https://en.wikipedia.org/wiki/Regular_expression)):

- `^padrão` → Pesquisa linhas que começam com "padrão".
- `padrão$` → Pesquisa linhas que terminam com "padrão".
- `.` → Corresponde a **qualquer caractere**.
- `[ATCG]` → Corresponde a **qualquer um** dos caracteres especificados.
- `[^ATCG]` → Corresponde a **qualquer caractere que não seja** um dos especificados.
- `padrão1\|padrão2` → Corresponde a "padrão1" **ou** "padrão2".

Alguns exemplos:

```bash
grep "^ATG" sequencias.txt      # Encontra linhas que começam com "ATG"
grep "GTC$" sequencias.txt      # Encontra linhas que terminam com "GTC"
grep "A.G" sequencias.txt       # Encontra "A" seguido de qualquer caractere e depois "G"
grep "A[TC]G" sequencias.txt    # Encontra "A" seguido de "T" ou "C" e depois "G"
grep "AG\|CT" sequencias.txt    # Encontra linhas que contêm "AG" ou "CT"
```

## Outras utilizações do `grep`
O `grep` pode ser usado para pesquisar um padrão em vários ficheiros ao mesmo tempo:

```bash
grep "mutação" ficheiro1.txt ficheiro2.txt
```

Pode ser combinado com outros comandos através de **pipes (`|`)**:
```bash
cat sequencias.txt | grep "ATG"
```

```bash
ls -l | grep ".txt"  # Lista apenas ficheiros .txt
```

Existem outras variações do `grep` para diferentes tipos de ficheiros. Uma muito útil é o `egrep` (Extended Grep), que suporta expressões regulares mais avançadas. Tem a mesma função que o `grep -E`:

!!! note "`grep`, `grep -E` e `egrep`"
    ```bash
    grep "ATG\|TGA" sequencias.txt  # Encontra linhas com "ATG" ou "TGA"
    grep "A\{2,4\}" sequencias.txt  # Encontra "AA", "AAA" ou "AAAA"
    ```
    Neste caso é necessária a barra `\` (escape) para lidar com caracteres especiais (como `+`, `?`, `|`, `{}`).

    ```bash
    egrep "ATG|TGA" sequencias.txt      # Equivalente a grep "ATG\|TGA"
    grep -E "ATG|TGA" sequencias.txt    # Mesmo comportamento do egrep

    egrep "A{2,4}" sequencias.txt       # Encontra "AA", "AAA" ou "AAAA"
    grep -E "A{2,4}" sequencias.txt     # Mesmo comportamento do egrep
    ```
    O `egrep` ou `grep -E` permite o uso direto de operadores como `+`, `?`, `|` e `{}`.


