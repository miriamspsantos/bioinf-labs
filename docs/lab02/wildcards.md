# Wildcards
Os **wildcards** são caracteres especiais usados para representar um ou mais caracteres nos nomes de ficheiros, facilitando a seleção e manipulação de múltiplos ficheiros ao mesmo tempo. São particularmente úteis quando se trabalha com um grande número de ficheiros que seguem uma convenção de nomenclatura semelhante, algo muito comum em bioinformática (por exemplo, ficheiros de sequências, ficheiros de alinhamento, etc.).  

### Wildcards Comuns  

- **Asterisco (`*`)**:
    - Corresponde a **zero ou mais caracteres**.  
    - É o wildcard mais utilizado para corresponder a múltiplos ficheiros ou partes de nomes de ficheiros.  

    !!! note "Exemplos"
        ```bash
        ls *.txt       # Lista todos os ficheiros que terminam em .txt
        ls sample*     # Lista todos os ficheiros que começam com "sample" (e.g., 'sample1.txt', 'sample_data.csv', etc.)
        ```

- **Ponto de Interrogação (`?`)**:
    - Corresponde **exatamente a um caracter**.
    - Útil para corresponder a nomes de ficheiros que diferem por apenas um caracter.  

    !!! note "Exemplos"
        ```bash
        ls file?  # Listar ficheiros com exatamente 5 caracteres, começando por `file (e.g., 'file1', 'fileA', 'filex', etc.)
        ls *.???  # Corresponde a qualquer ficheiro com uma extensão de 3 caracteres (e.g.,'dados.txt', 'sequencias.fna', etc.)
        ```

- **Parêntesis Rectos (`[]`)**:
    - Corresponde **a qualquer um dos caracteres especificados dentro dos parêntesis**.
    - Pode incluir letras, números ou intervalos de caracteres.  

    !!! note "Exemplos"
        ```bash
        ls data[123]    # Qualquer ficheiro que comece com `data` e termine em `1`, `2` ou `3` (e.g., 'data1', 'data2', 'data3')
        ```

- **Hífen (`-`) dentro de Parênteses Rectos**:
    - Representa um **intervalo de caracteres**.  

    !!! note "Exemplos"
        ```bash
        ls [a-z]*          # Ficheiros que comecem por uma letra minúscula (`a` a `z`), (e.g., 'banana.csv', 'arquivo.txt', etc.)
        ls file[1-3].txt   # Ficheiros com um número entre `1` e `3` (e.g., 'file1.txt', 'file2.txt', 'file3.txt')
        ```

- **Circunflexo (`^`) dentro de Parêntesis Rectos**: 
    - Quando usado no início da expressão dentro dos parêntesis rectos, o circunflexo (`^`) nega o padrão, correspondendo a **qualquer carácter excepto os especificados**.  

    !!! note "Exemplos" 
        ```bash
        ls [^ab]*  # Ficheiros que NÃO comecem por `a` ou `b` (e.g., 'casa.txt', 'dados.fna', mas não 'apple.txt')
        ```

### Combinar Wildcards com Outros Comandos  
Os *wildcards* são frequentemente usados com comandos como `ls`, `cp`, `mv`, `rm` e outros para operar em múltiplos ficheiros ao mesmo tempo.  

!!! tip "Listar Ficheiros com Wildcards" 
    Para listar todos os ficheiros `.fastq` numa diretoria:  
    ```bash
    ls *.fastq  # Lista todos os ficheiros com extensão .fastq
    ```
    Para listar todos os ficheiros que começam com `seq` e têm qualquer extensão:  
    ```bash
    ls seq*.*  # Corresponde a seq1.fasta, seq2.fastq, seq3.txt, etc.
    ```
    
    
!!! tip "Copiar Ficheiros com Wildcards" 
    Para copiar todos os ficheiros `.fasta` de uma diretoria para outra:  
    ```bash
    cp *.fasta /caminho/do/destino/
    ```

!!! tip "Remover Ficheiros com Wildcards" 
    Para remover todos os ficheiros `.log` numa diretoria:  
    ```bash
    rm *.log  # Remove todos os ficheiros com extensão .log
    ```

!!! tip "Procurar Ficheiros com Wildcards" 
    Também é possível usar wildcards com `grep` para pesquisar padrões em ficheiros. Por exemplo, para procurar a sequência `ATGC` em todos os ficheiros FASTA:  
    ```bash
    grep "ATGC" *.fasta  # Pesquisa "ATGC" em todos os ficheiros .fasta
    ```