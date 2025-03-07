### Símbolos

| **Símbolo** | **Descrição** | **Exemplo** | **Explicação** |
|------------|-------------|-------------|--------------|
| **$0 ... $9** | Parâmetros da linha de comandos | `$1` | Representa o primeiro argumento passado ao script |
| **$*** | Todos os parâmetros da linha de comandos | `echo "$*"` | Exibe todos os argumentos como uma única string |
| **$#** | Número de parâmetros da linha de comandos | `echo $#` | Retorna a contagem dos argumentos passados |
| **$?** | Código de retorno (*exit status*) do último comando executado | `ls /teste; echo $?` | Mostra `0` se o comando for bem-sucedido ou um número diferente se falhar |
| **"..."** | Protege uma *string*, mas reconhece `$`, `` ` ``, `\` e `!` como especiais | `echo "O usuário é $USER"` | Expande variáveis dentro da string |
| **'...'** | Protege uma *string* sem reconhecer caracteres especiais | `echo 'O usuário é $USER'` | A string é impressa exatamente como está, sem expansão |
| **\`...\` ou $(...)** | Executa comandos numa *subshell* | `` echo "Hoje é `date`" `` | O comando dentro das *backticks* é executado e substituído pelo resultado |
| **$((...))** | Retorna o resultado de uma expressão aritmética | `echo $((5 + 3))` | Avalia a expressão e imprime `8` |

### Testes e Expressões

| **Comando** | **Descrição** | **Exemplo** | **Explicação** |
|------------|-------------|-------------|--------------|
| **test expressão** | Testa uma expressão | `test 5 -gt 3` | Retorna verdadeiro (`0`) se 5 for maior que 3 |
| **Comparação numérica** | `NUM1 OP NUM2` *(OP: -lt, -gt, -le, -ge, -eq, -ne)* | `[ 10 -eq 10 ]` | Compara dois números inteiros |
| **Comparação de strings** | `STR1 OP STR2` *(OP: =, !=, -n, -z)* | `[ "abc" = "abc" ]` | Verifica se duas strings são iguais |
| **Testes em ficheiros** | `OP FICH` *(OP: -e, -f, -d, -r, -w, -x)* | `[ -f ficheiro.txt ]` | Verifica se um ficheiro existe e é regular |
| **expr expressão** | Operações aritméticas | `expr 5 + 3` | Retorna `8`, equivalente a `5 + 3` |
| **$((expressão))** | Avalia uma expressão | `echo $((4 * 2))` | Retorna `8`, usado para cálculos matemáticos |


### Estruturas de Controlo

#### Condicionais
```bash
if condição
then
    ...
elif condição
then
    ...
else
    ...
fi
```

#### Loop `while`
```bash
while condição
do
    ...
done
```

#### Loops `for`
```bash
for variável in lista
do
    ...
done
```

ou

```bash
for ((exp1; exp2; exp3))
do
    ...
done
```


