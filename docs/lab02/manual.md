Nem sempre sabemos de cor como usar todos os comandos, mas podemos consultar o manual do sistema através do comando `man`, que nos fornece informações sobre como usar os comandos, a sua sintaxe, as opções disponíveis e alguns exemplos. Cada comando tem tipicamente uma página correspondente.

### Utilização Básica do `man`
Para aceder à página de um comando, podemos usar o seguinte comando:

```bash
man <comando>
```

!!! note "Exemplo"

    ```bash
    man ls      # Mostra a página do manual para o comando 'ls'
    man grep    # Mostra detalhes sobre o comando 'grep'
    man wget    # Mostra a documentação do comando 'wget'
    ```

A página do manual está dividida em várias secções:

!!! abstract "Secções do Manual"
    - **NAME**: O nome do comando e uma descrição breve.
    - **SYNOPSIS**: Um resumo da sintaxe do comando.
    - **DESCRIPTION**: Informações detalhadas sobre o comando e suas opções.
    - **OPTIONS**: Uma lista das opções do comando e o que elas fazem.
    - **EXAMPLES**: Exemplos práticos de como usar o comando.
    - **SEE ALSO**: Links para comandos e páginas de manual relacionadas.

### Navegar pelas páginas do `man`
Dentro de uma página do manual, podemos navegar usando as seguintes teclas:

!!! abstract "Navegação no Manual"
    - **Espaço**: Avançar uma página.
    - **b**: Retroceder uma página.
    - **Enter**: Avançar uma linha.
    - **/termo_de_busca**: Procurar por uma palavra específica dentro do manual.
    - **n**: Avançar para o próximo resultado da pesquisa.
    - **q**: Sair do manual e voltar ao terminal.


### Exemplos: Explorar os comandos `ls`, `grep` e `cut`

!!! info "Explorar o comando `ls`"
    Para ver a página do manual para o comando `ls`, podemos escrever:

    ```bash
    man ls
    ```
    O manual mostra as seguintes secções:

    - **SYNOPSIS**:
    ```bash
    ls [OPTION]... [FILE]...
    ```
    - **OPTIONS**:
        - `-l`: Listar ficheiros no formato longo
        - `-a`: Mostrar todos os ficheiros, incluindo os ocultos
    
    - **EXAMPLES**:
    ```bash
    ls -lh  # Lista os ficheiros com tamanhos legíveis
    ls -a   # Lista todos os ficheiros, incluindo os ocultos
    ```


!!! info "Explorar o comando `grep`"
    O comando `grep` é frequentemente utilizado para procurar padrões em ficheiros. Para explorá-lo:

    ```bash
    man grep
    ```

    Secções que podemos ver:

    - **SYNOPSIS**:
    ```bash
    grep [OPTION]... PATTERN [FILE]...
    ```
    - **OPTIONS**:
        - `-i`: Ignorar maiúsculas/minúsculas na pesquisa.
        - `-v`: Inverter a correspondência (mostrar apenas as linhas que não coincidem).
        - `-r`: Buscar recursivamente em pastas/diretorias.

    - **EXAMPLES**:
    ```bash
    grep -i "ATGC" file.fasta   # Pesquisa sem considerar maiúsculas/minúsculas pelo padrão "ATGC"
    grep -r "padrão" diretoria  # Pesquisa recursiva pelo padrão "padrão" em todos os arquivos de uma diretoria
    ```

!!! info "Explorar o comando `cut`"
    O comando `cut` é útil para extrair colunas de arquivos, e por isso frequentement utilizado em conjuntos de dados de bioinformática como ficheiros CSV.

    ```bash
    man cut
    ```

    Secções chave:

    - **SYNOPSIS**:
    ```bash
    cut [OPTION]... [FILE]...
    ```

    - **OPTIONS**:
        - `-f <campos>`: Seleciona campos específicos (colunas).
        - `-d <delimitador>`: Especifica o delimitador entre os campos.

    - **EXAMPLES**:
    ```bash
    cut -f1,3 -d',' file.csv   # Extrai as colunas 1 e 3 de um ficheiro CSV
    cut -c1-5 file.txt         # Extrai os primeiros 5 caracteres de cada linha
    ```

## Argumentos e Opções
Muitos commandos aceitam argumentos e opções para modificar o seu comportamento:

!!! note "Exemplos"

    ```bash
    ls -l               # Lista os ficheiros em formato longo (com detalhes)
    ls -a               # Lista todos os ficheiros, incluindo os ocultos
    rm -r pasta/        # Remove a "pasta" e todo o seu conteúdo
    ```

Os **argumentos** são **entradas/informação** fornecidas a um comando para indicar sobre o que ele deve atuar, tal como o nome de um ficheiro ou diretoria:  

  ```bash
  cat ficheiro.txt  # 'ficheiro.txt' é um argumento passado para o comando 'cat'
  ```

As **opções** (também chamadas *flags*) modificam o comportamento de um comando. Normalmente, são precedidas por um traço (`-`) para opções curtas ou por dois traços (`--`) para opções mais longas:

- **Opções Curtas:** 
    - Começam com um único traço (`-`).
    - Usam uma única letra (`-l`, `-a`, `-r`, etc.).
    - Podem ser combinadas sem espaços (`-la` é o mesmo que `-l -a`).
    - São mais rápidas de digitar, mas menos descritivas.

!!! note "Opções Curtas"
    ```bash
    ls -l                             # '-l' é uma opção que exibe informações detalhadas sobre os ficheiros
    ls -a                             # Exibir ficheiros ocultos
    grep -i "padrão" ficheiro.txt     # Pesquisa sem diferenciar maiúsculas/minúsculas
    grep -c "padrão" ficheiro.txt     # Conta o número de ocorrências do padrão
    sort -r ficheiro.txt              # Ordenação reversa
    sort -u ficheiro.txt              # Remove duplicados ao ordenar
    ls -l -a                          # Listar arquivos em formato detalhado e incluir ocultos
    ls -la                            # O mesmo que acima, combinando as opções
    ```

- **Opções Longas:**
    - Começam com dois traços (`--`).
    - São palavras completas (`--all`, `--recursive`, `--verbose`, etc.).
    - Não podem ser combinadas e precisam de ser usadas separadamente.
    - São mais fáceis de entender, mas mais longas para digitar.

!!! note "Opções Longas"
    ```bash
    ls --all                                   # Mostra todos os ficheiros, incluindo os ocultos
    grep -i "padrão" ficheiro.txt              # Opção curta (-i) para ignorar maiúsculas/minúsculas
    grep --ignore-case "padrão" ficheiro.txt   # Opção longa equivalente
    ```

Para comandos frequentes, as opções curtas são mais rápidas (`ls -l`). Para scripts e comandos mais complexos, as opções longas são mais legíveis (`tar --verbose --extract --file=backup.tar`).