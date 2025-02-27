# Utilização de Pipes (`|`)

### O que é um Pipe?  
Um **pipe** (`|`) é uma funcionalidade que permite **ligar a saída** de um comando diretamente à **entrada** de outro comando. Isto possibilita a criação de uma **sequência de operações** -- ou um **pipeline** -- onde a saída de um comando é processada pelo comando seguinte na cadeia.  

Em vez de executarmos cada comando separadamente e gerirmos manualmente ficheiros intermédios, podemos **passar dados de um comando para outro**, tornando o fluxo mais eficiente. Isto é especialmente útil quando se lida com grandes volumes de dados em bioinformática, onde múltiplas etapas de processamento podem ser combinadas numa única linha de comando.  

### Sintaxe Básica  

A sintaxe básica para usar pipes é: 

```bash
comando1 | comando2 | comando3
```

Neste caso, a saída do `comando1` é passada como entrada para o `comando2` e a saída do `comando2` é passada para o `comando3`.  

### Exemplos

!!! success "Combinar `ls` e `grep`"
    Para listar todos os ficheiros numa diretoria e depois filtrar apenas os ficheiros `.txt`, podes usar o `ls` em combinação com o `grep` utilizando um pipe:  
    ```bash
    ls | grep ".txt"
    ```
    - `ls` lista todos os ficheiros na diretoria atual.  
    - `grep ".txt"` filtra a saída e mostra apenas as linhas que contêm `.txt`.  

!!! success "Combinar `cat`, `grep` e `sort`"
    Se tiveres um ficheiro de texto grande e quiseres contar as ocorrências de uma palavra específica (por exemplo, "gene"), podes ordenar a saída e mostrar os 10 resultados mais frequentes:  
    ```bash
    cat ficheiro.txt | grep -o "gene" | sort | uniq -c | sort -nr | head -n 10
    ```
    - `cat ficheiro.txt` mostra o conteúdo do ficheiro.  
    - `grep -o "gene"` extrai todas as ocorrências da palavra "gene".  
    - `sort` ordena as ocorrências alfabeticamente.  
    - `uniq -c` conta o número de ocorrências de cada palavra.  
    - `sort -nr` ordena os contadores por ordem decrescente.  
    - `head -n 10` mostra os 10 resultados mais comuns.  

!!! success "Combinar `wc` e `sort`"
    Para contar o número de sequências (linhas que começam com `>`) em vários ficheiros FASTA e ordená-los pelo número de sequências, podes usar:  
    ```bash
    grep -c "^>" *.fasta | sort -n
    ```
    - `grep -c "^>" *.fasta` conta o número de sequências em cada ficheiro FASTA.  
    - `sort -n` ordena os resultados por ordem crescente.  

!!! success "Combinar `cut` e `sort`"
    Se tiveres um ficheiro tabulado (`data.csv`) e quiseres extrair a primeira e a terceira colunas, ordená-las e remover duplicados, podes usar:  
    ```bash
    cut -f1,3 data.tsv | sort | uniq
    ```
    - `cut -f1,3 data.csv` extrai as colunas 1 e 3 do ficheiro.  
    - `sort` ordena os dados.  
    - `uniq` remove as linhas duplicadas.  


### Casos Práticos em Bioinformática
Os pipes são especialmente úteis na bioinformática, onde a manipulação de grandes volumes de dados é frequente. Combinando comandos simples, é possível processar, analisar e organizar sequências biológicas de forma rápida e eficiente, sem necessidade de software complexo. Eis alguns exemplos:

- **Contar o Número de Sequências num Ficheiro FASTA**  
   Para contar as sequências em vários ficheiros FASTA:  
   ```bash
   grep -c "^>" *.fasta | sort -n
   ```

- **Analisar Dados de Sequências**  
   Para encontrar todas as ocorrências de um *motif* (`ATGC`) num conjunto de ficheiros FASTA e contar quantas vezes aparece:  
   ```bash
   grep -o "ATGC" *.fasta | wc -l
   ```

3. **Limpar e Organizar Dados**  
   Para remover linhas duplicadas num ficheiro de texto grande:  
   ```bash
   sort ficheiro.txt | uniq > ficheiro_limpo.txt
   ```