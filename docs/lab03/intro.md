# Introdução ao Shell Scripting

*Shell Scripting* (i.e., "programação na *shell*") é uma forma alternativa de interagir com o sistema operativo através da shell. Em vez de inserir os comandos um a um, é possível escrevê-los em *scripts*, que serão interpretados sequencialmente. O Shell scripting inclui os conceitos básicos de programação como **variáveis, estruturas de controlo (condições e loops) e funções**, permitindo-nos automatizar certas tarefas na shell. 
 
 
!!! warning "Bash Shell"
    Diferentes *shells* (e.g. bash, sh, zsh, ...) podem apresentar variações de sintaxe. Nos **Laboratórios de Bioinformática**, vamos focar-nos mais na **bash shell**.

## Conceitos Básicos

### Extensão e `!/bin/bash`
Os scripts de shell são frequentemente ficheiros com a extensão **.sh** e para serem interpretados, precisam de permissões de execução e leitura. Estas permissões podem ser adicionadas com o comando `chmod`, como no exemplo:  

```bash
chmod a+rx <ficheiro_do_script>
```  

Como diferentes shells podem ter diferenças na sintaxe, a primeira linha de qualquer *script* é um comentário especial que indica o shell "alvo" (i.e., onde o script deve ser executado). Para a bash shell, essa primeira linha deve ser:  

```bash
#!/bin/bash
```  

O símbolo **#** pode depois ser utilizado para inserir comentários em qualquer linha.  

### Variáveis
As **variáveis** podem ser úteis para armazenar informações que serão necessárias em etapas posteriores do script. A sintaxe para definir variáveis é a seguinte:  

```bash
<variável>=<valor>
```

Nota que **não devem existir espaços antes ou depois do sinal `=`**, pois, caso contrário, a shell interpretará o nome da variável como um comando. Outro aspeto importante é que **o tipo da variável não é definido**, ou seja, a shell armazena todas as variáveis como strings, mas distingue dados textuais de dados numéricos.  

Para **aceder ao valor de uma variável**, deve-se preceder o seu nome com `$`, como no exemplo:  

```bash
$<variável>
```  

Este símbolo `$` também é utilizado para aceder às **informações sobre os argumentos** passados ao script, nomeadamente:  

- `$0` a `$9` – Acede a cada argumento individualmente;  
- `$*` – Acede a todos os argumentos de uma vez;  
- `$#` – Obtém o número total de argumentos passados.  

### **Exemplos**

!!! note "Definir e usar variáveis"
    Criamos as variáveis `nome` e `idade` com valores `Miriam` e `99`:
    ```bash
    nome="Miriam"
    idade=99
    echo "O meu nome é $nome e tenho $idade anos."
    ```

    Usamos a sintaxe `$nome` e `$idade` para aceder aos valores:

    ```bash
    O meu nome é Miriam e tenho 99 anos.
    ```

    Se houver espaços antes ou depois do `=`, é devolvido um erro:
    ```bash
    nome = Miriam       # Erro!
    ```

    
!!! note "Aceder aos argumentos passados ao script"
    Se criarmos um ficheiro `script.sh` com este conteúdo:
    ```bash
    #!/bin/bash
    echo "Nome do script: $0"
    echo "Primeiro argumento: $1"
    echo "Segundo argumento: $2"
    echo "Todos os argumentos: $*"
    echo "Número total de argumentos: $#"
    ```
    E executarmos o script passando argumentos:
    ```bash
    ./ script.sh Ana 30
    ```

    O output esperado será:

    ```bash
    Nome do script: script.sh
    Primeiro argumento: Ana
    Segundo argumento: 30
    Todos os argumentos: Ana 30
    Número total de argumentos: 2
    ```

## Estruturas de Controlo

### Condições (`if-elif-else`)
As estruturas condicionais permitem-nos tomar decisões com base em testes ou condições. A sintaxe básica é a seguinte:

```bash
if <condição>; then
    # Comandos a executar se a condição for verdadeira
elif <outra_condição>; then
    # Comandos a executar se a outra condição for verdadeira
else
    # Comandos a executar se nenhuma das condições anteriores for verdadeira
fi
```
Em relação a esta condição, os seguintes tipos são aceites:

- **Comparações com variáveis numéricas, strings ou ficheiros**, que são definidas dentro de `[ ... ]`:

    !!! info "Comparação numérica"
        ```bash
        #!/bin/bash

        a=10
        b=5

        if [ $a -gt $b ]; then
            echo "$a é maior que $b"
        else
            echo "$a não é maior que $b"
        fi
        ```

        **Nota:** `-gt` (greater than) é usado para verificar se `a` é maior que `b`.

    !!! info "Comparação de strings"
        ```bash
        #!/bin/bash

        nome1="João"
        nome2="Ana"

        if [ "$nome1" = "$nome2" ]; then
            echo "Os nomes são iguais"
        else
            echo "Os nomes são diferentes"
        fi
        ```
        **Nota:** Usamos `=` para verificar se as strings são iguais.


    !!! info "Comparação de ficheiros"
        ```bash
        #!/bin/bash

        ficheiro="/caminho/para/ficheiro.txt"

        if [ -f "$ficheiro" ]; then
            echo "$ficheiro é um ficheiro regular"
        else
            echo "$ficheiro não é um ficheiro regular"
        fi
        ```
        **Nota:** `-f` é usado para verificar se o ficheiro fornecido é um ficheiro regular.


- **Execução de comandos numa subshell**, onde a condição é baseada no código de saída dos comandos, que são definidos dentro de `(...)`.

    !!! info "Execução de comandos numa subshell"
        ```bash
        #!/bin/bash

        # Verificar se o comando 'ls' foi bem-sucedido
        if ( ls /diretorio/nao/existe ); then
            echo "Comando executado com sucesso"
        else
            echo "Comando falhou"
        fi

        ```
       **Nota:** O comando `ls` está dentro de uma subshell `( ... )`. O código de saída do comando `ls` é verificado. Como a diretoria não existe, a condição falha e a cláusula `else` será executada.


- **Operações aritméticas**, que são definidas dentro de `((...))`.


    !!! info "Operações aritméticas"
        ```bash
        #!/bin/bash

        x=5
        y=10

        if (( x + y > 10 )); then
            echo "A soma de x e y é maior que 10"
        else
            echo "A soma de x e y não é maior que 10"
        fi    
        ```

- **Comparações mais complexas**, baseadas nas mencionadas no primeiro ponto, como verificar se uma string corresponde a uma expressão regular, que são definidas dentro de `[[ … ]]`.

    !!! info "Operações complexas (e.g., regex)"
        Um exemplo de uma operação mais complexa seria fazer comparações com expressões regulares (i.e., [regex](https://en.wikipedia.org/wiki/Regular_expression)):

        ```bash
        #!/bin/bash

        nome="João123"

        if [[ $nome =~ ^João[0-9]+$ ]]; then
            echo "A string segue o padrão"
        else
            echo "A string não segue o padrão"
        fi
   
        ```

        **Nota:** Neste exemplo, usamos `[[...]]` para incorporar a expressão regular. O operador `=~` permite comparar uma string com uma expressão regular; neste caso, queremos verificar se a variável `nome` começa com "João" e tem números no final (`[0-9]+`), ou seja qualquer número entre 0 e 9; `+` indica que pode haver um ou mais dígitos consecutivos.

!!! warning "Espaços entre `[`e `]`"
    É importante usar correctamente os espaços ao usar `[`e `]` no bash. A razão é que `[` é, na verdade, um comando (uma forma alternativa do comando `test`) e no Bash, os comandos e os seus argumentos devem ser separados por espaços.

    ```bash
    while [$contador -le 5]  # Erro: sem espaços ao redor de [ e ]
    while [ $contador -le 5 ]  # OK: Espaços corretos
    ```

    Podemos testar com `test` diretamente:
    ```bash
    test 5 -le 10 && echo "Verdadeiro"  # OK
    test5 -le 10 && echo "Verdadeiro"   # Erro: `test5` não é um comando
    ```

    O mesmo vale para `[`:
    ```bash
    [ 5 -le 10 ] && echo "Verdadeiro"  # OK
    [5 -le 10] && echo "Verdadeiro"    # Erro
    ```




#### Operadores de Comparação na Shell
Para realizar as comparações com variáveis numéricas, strings e ficheiros, são necessários diferentes operadores.

##### Operadores Numéricos
No caso dos tipos numéricos, o operador é definido entre dois valores ou variáveis, como: `<num1> <op> <num2>`. Os operadores disponíveis são:

- **`-eq`** – igual
- **`-ne`** – diferente
- **`-lt`** – menor que
- **`-le`** – menor ou igual a
- **`-gt`** – maior que
- **`-ge`** – maior ou igual a

Os operadores "tradicionais" (por exemplo, `<` ou `>`) só podem ser usados dentro de **`((…))`**. 

##### Operadores de Strings
No caso das **strings**, o operador é definido da mesma forma que para os tipos numéricos e os operadores disponíveis são:

- **`=`** – igual
- **`!=`** – diferente
- **`-n`** – a string não é nula
- **`-z`** – a string é nula

##### Operadores de Ficheiros
Os operadores de ficheiros são definidos antes do caminho para um ficheiro específico, como: `<op> <file>`. Alguns dos operadores disponíveis são:

- **`-e`** – existe
- **`-f`** – é um ficheiro regular (não um diretoria)
- **`-d`** – é uma diretoria
- **`-r`** – tem permissões de leitura
- **`-w`** – tem permissões de escrita
- **`-x`** – tem permissões de execução

### Loops (`for`, `while`)

O *Shell Scripting* suporta os comandos `for` e `while`. 

#### Loop `for`
O loop `for` é utilizado para repetir um conjunto de comandos um determinado número de vezes, geralmente iterando sobre uma lista ou intervalo.

```bash
for <variável> in <lista>
do
    # Comandos a executar para cada item da lista
done
```

!!! note "Loop `for`"
    ```bash
    #!/bin/bash

    for i in 1 2 3 4 5
    do
        echo "Número $i"
    done
    ```

     **Saída:**
    ```bash
    Número 1
    Número 2
    Número 3
    Número 4
    Número 5
    ```

!!! note "Loop `for` com intervalo"

    ```bash
    #!/bin/bash

    for i in {1..5}
    do
        echo "Número $i"
    done
    ```
    **Saída:**
    ```bash
    Número 1
    Número 2
    Número 3
    Número 4
    Número 5
    ```

!!! note "Loop `for` com lista de valores"

    ```bash
    #!/bin/bash

    for i in Alice Bob Carlos "Diana Silva" 42
    do
        echo $i
    done
    ```
    **Saída:**
    ```bash
    Alice
    Bob
    Diana Silva
    42
    ```

Também existe a sintaxe mais "tradicional", onde a variável é incrementada entre um valor inicial e um valor final:

```bash
for ((exp1; exp2; exp3))
do
	# Comandos a executar em cada iteração
done
```

!!! note "Loop `for` com intervalo"

    ```bash
    #!/bin/bash
    for ((i = 1; i <= 5; i++))  # Inicia em 1, vai até 5, incrementando 1 a cada iteração
    do
        echo "Número: $i"
    done

    ```
    **Saída:**
    ```bash
    Número 1
    Número 2
    Número 3
    Número 4
    Número 5
    ```

#### Loop `while`
O loop `while` executa um conjunto de comandos enquanto uma condição for verdadeira:

```bash
while [ condição ]
do
    # Comandos a executar enquanto a condição for verdadeira
done
```

!!! note "Loop `while`"
    ```bash
    #!/bin/bash

    contador=1

    while [ $contador -le 5 ]
    do
        echo "Contador: $contador"
        contador=$((contador + 1))  # Incrementa o contador
    done
    ```
    **Saída:**
    ```bash
    Contador: 1
    Contador: 2
    Contador: 3
    Contador: 4
    Contador: 5
    ```


## Subshells

Por vezes, temos interesse em executar comandos em subshells (i.e., "processos filhos" do processo atual) para obter o *output* de determinados comandos da mesma forma que "chamamos" uma função. Essa execução pode ser feita definindo os comandos dentro de `$(...)`.

Por exemplo, o output the um comando pode ser guardado numa variável no formato:

```bash
<variável>=$(<comando>)
```

## Leitura e Escrita na Shell

O **Shell Scripting** também oferece alguns comandos que permitem a interação com o utilizador, através do `echo` e `read`.

Para escrever algo na shell, utiliza-se o comando `echo`. O comando `echo` recebe uma string e escreve-a na consola; se essa string contiver variáveis previamente definidas, esses valores são apresentados:

!!! note "echo"
    ```bash
    #!/bin/bash

    # Definir a variável
    NOME="Miriam"

    # Exibir uma mensagem com a variável
    echo "O meu nome é $NOME"
    ```
    **Saída:**
    ```
    O meu nome é Miriam
    ```
Para pedir informações ao utilizador através da shell, o comando **`read`** pode ser usado, seguido pelo nome da variável que vai armazenar a string inserida, como: `read <variável>`. Esta variável não precisa de ser declarada previamente.

!!! note "read"
    ```bash
    #!/bin/bash

    # Perguntar ao utilizador pelo nome
    echo "Qual é o teu nome?"

    # Ler a resposta e armazená-la na variável NOME
    read NOME

    # Exibir a mensagem com o nome inserido
    echo "Olá, $NOME!"
    ```
    **Saída:**
    ```
    Qual é o teu nome?
    Miriam
    Olá, Miriam
    ```




