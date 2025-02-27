# Manipulação de Ficheiros
Existem vários comandos que permitem realizar operações com ficheiros como copiar, mover, mudar o nome, criar e visualizar o seu conteúdo. Estes comandos são essenciais para manter a estrutura de ficheiros organizada e facilitar a navegação e edição de dados.

## Navegação, Criação, Eliminação

- `pwd`: Mostra a diretoria atual
- `ls`: Lista as pastas e ficheiros na diretoria atual
- `cd <diretoria>`: Muda para a diretoria especificada
- `mkdir <diretoria>`: Cria uma nova diretoria
- `rmdir <diretoria>`: Remove uma diretoria

!!! note "Exemplos"
    ```bash
    pwd                     # Mostra a diretoria atual
    ls                      # Lista as pastas e ficheiros na diretoria atual
    cd Documentos           # Muda para a diretoria "Documentos"
    mkdir projeto_bioinf    # Cria a pasta "projeto_bioinf"
    rmdir projeto_bioinf    # Apaga a pasta "projeto_bioinf"
    ```

## Operações com Ficheiros

- `cp <origem> <destino>`: Copia um ficheiro de um local para outro
- `mv <origem> <destino>`: Move ou muda o nome de um ficheiro
- `rm <ficheiro>`: Apaga um ficheiro
- `touch <ficheiro>`: Cria um ficheiro vazio
- `cat <ficheiro>`: Mostra o conteúdo de um ficheiro
- `less <ficheiro>`: Mostra o conteúdo de um ficheiro página por página
- `head -n <número> <ficheiro>`: Exibe as primeiras n linhas de um ficheiro
- `tail -n <número> <ficheiro>`: Exibe as últimas n linhas de um ficheiro

!!! note "Exemplos"
    ```bash
    cp ficheiro.txt backup.txt           # Copia "ficheiro.txt" para "backup.txt"
    mv nome_antigo.txt nome_novo.txt     # Renomeia o ficheiro "nome_antigo.txt" para "nome_novo.txt"
    rm ficheiro_indesejado.txt           # Remove "ficheiro_indesejado.txt"
    touch novo_ficheiro.txt              # Cria um ficheiro vazio chamado "novo_ficheiro.txt"
    cat exemplo.txt                      # Mostra o conteúdo do ficheiro "exemplo.txt"
    less ficheiro_grande.txt             # Mostra o conteúdo do "ficheiro_grande.txt" página por página
    head -n 10 ficheiro.txt              # Mostra as primeiras 10 linhas do "ficheiro.txt"
    tail -n 10 ficheiro.txt              # Mostra as últimas 10 linhas do "ficheiro.txt"
    ```

## Operações de Procura em Ficheiros

- `find <diretoria> -name "*.extensão"`: Encontra ficheiro por nome e extensão
- `grep "padrão" <ficheiro>`: Pesquisa por um padrão de texto dentro de um ficheiro
- `wc -l <ficheiro>`: Conta o número de linhas num ficheiro
- `sort <ficheiro>`: Mostra as linhas de um ficheiro ordenadas
- `uniq <ficheiro>`: Mostra as linhas únicas de um ficheiro

!!! note "Exemplos"
    ```bash
    find /home/user -name "*.fasta"         # Encontra arquivos com extensão ".fasta" na diretoria /home/user
    grep "ATGC" sequencias.fasta            # Pesquisa o padrão "ATGC" no ficheiro "sequencias.fasta"
    wc -l dados.txt                         # Conta o número de linhas no arquivo "dados.txt"
    sort nomes.txt                          # Ordena as linhas do ficheiro "nomes.txt"
    sort nomes.txt | uniq                   # Ordena as linhas do arquivo "nomes.txt", removendo as duplicadas
    ```

## Redireccionamento

O **redirecionamento** permite controlar de onde vem a entrada de um comando e para onde vai a sua saída. Ess processo pode ser indicado através dos seguintes símbolos:

- **`>`**: Redireciona a saída para um ficheiro (faz "overwrite" ao ficheiro, i.e., "escreve por cima").  
- **`>>`**: Redireciona a saída para um ficheiro, adicionando ao final caso o ficheiro já exista.  
- **`<`**: Redireciona a entrada de um ficheiro.  


### Sobrescrever um Ficheiro (`>`)  

O símbolo `>` redireciona a saída (*stdout*) de um comando para um ficheiro. Se o ficheiro já existir, **o conteúdo é substituído**.  

Por exemplo, podes edirecionar a saída de `echo` para um ficheiro `output.txt`:
```bash
echo "Olá, Bioinformática!" > output.txt
```
Este comando cria um ficheiro chamado `output.txt` (ou substitiu o seu conteúdo se ele já existir), escrevendo "Olá, Bioinformática!".

### Adicionar ao Final de um Ficheiro (`>>`)  
Para adicionar dados ao final de um ficheiro sem substituir o seu conteúdo usamos `>>`.  

Por exemplo, podes adicionar data e hora atual a um ficheiro de registo (log):  
```bash
date >> log.txt
```
Este comando adiciona a data e hora atual ao ficheiro `log.txt` sem apagar o conteúdo existente.  

### Redirecionar a Entrada de um Ficheiro (`<`)  

Em vez de escrevermos a entrada manualmente no terminal, podemos usar `<` para indicar a entrada de um ficheiro. Nalgumas situações, esoecialmente com comandos que não aceitam ficheiros como argumento, usar o `<` é vantajoso. Por exemplo, no comando seguinte o `tr` converte as letras minúsculas em maiúsculas, mas não aceita ficheiros diretamente como argumento. Usar `<` garante que o conteúdo do `texto.txt` é passado para o `tr` através da entrada padrão:

```bash
tr 'a-z' 'A-Z' < texto.txt
```