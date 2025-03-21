# Processamento Básico de Sequências

## Exercícios

1. Escreva uma função `random_dna_sequence` que crie uma sequência de DNA aleatória de tamanho `length`, com a mesma funcionalidade da [Random DNA Sequence do SMS2](https://www.bioinformatics.org/sms2/random_dna.html).
```python
def random_dna_sequence(length):
    ...
```
2. Escreva uma função `random_sequence` que altere a função anterior para também poder gerar sequências de RNA aleatórias:
```python
def random_sequence(length, seq_type):
    ...
```
3. Incorpore também a possibilidade de criar sequências aleatótias de proteínas, com a mesma funcionalidade da [Random Protein Sequence do SMS2](https://www.bioinformatics.org/sms2/random_protein.html).

4. Crie uma função `validate_dna` para verificar se a sequência de dna de *input* é válida (retorna `True` se for válida e `False` caso contrário).
```python
def validate_dna(dna_seq):
    ...
```
5. Generalize a função anterior (`validate_sequence`) para validar sequências de RNA e proteínas.

6. Crie uma função `hamming_distance` que determine a distância de Hamming entre duas sequências.
```python
def hamming_distance(seq1, seq2):
    ...
```

7. Crie uma função `dot_plot` que retorne uma matrix de comparação entre duas sequências:
```python
def dot_plot(seq1, seq2):
    ...
```
8. Crie uma função `count_nucleotides` que retorne o número de nucleótidos da sequência, para cada tipo (considere a construção de um dicionário).
```python
def count_nucleotides(sequence):
    ...
```
9. Crie uma função que determine a percentagem de nucleótidos `C` e `G` na sequência.
```python
def gc_content(dna_seq):
    ...
```
10. Escreva um função `transcript` que transcreva a sequência de DNA dada.
```python
def transcript(dna_seq):
    ...
```
11. Crie uma função `reverse` que a partir de uma sequência de DNA gere o seu reverso. Compare o seu resultado com a função [Reverse Complement do SMS2](https://www.bioinformatics.org/sms2/rev_comp.html) (escolha a opção "reverse").
```python
def reverse(dna_seq):
    ...
```
12. Crie uma função `complement` que a partir de uma sequência de DNA gere o seu complemento. Compare o seu resultado com a função [Reverse Complement do SMS2](https://www.bioinformatics.org/sms2/rev_comp.html) (escolha a opção "complement").
```python
def complement(dna_seq):
    ...
```
13. Crie uma função `reverse_complement` que a partir de uma sequência de DNA gere o seu complemento reverso (use as funções que acabou de criar!). Compare o seu resultado com a função [Reverse Complement do SMS2](https://www.bioinformatics.org/sms2/rev_comp.html) (escolha a opção "reverse complement").
```python
def reverse_complement(dna_seq):
    ...
```
14. Escreva uma função `translate_seq` que traduza uma sequência de DNA para uma cadeia de aminoácidos. Use a seguinte função `translate_codon(codon)`:
```python
def translate_codon(codon):
    """ Translates a codon into an aminoacid.
        Considers the direct translation of DNA to proteins
        using a provided conversion table.
    """
    map = {"GCT":"A", "GCC":"A", "GCA":"A", "GCG":"A",
           "TGT":"C", "TGC":"C", "GAT":"D", "GAC":"D",
           "GAA":"E", "GAG":"E", "TTT":"F", "TTC":"F",
           "GGT":"G", "GGC":"G", "GGA":"G", "GGG":"G",
           "CAT":"H", "CAC":"H", "ATA":"I", "ATT":"I",
           "ATC":"I", "AAA":"K", "AAG":"K", "TTA":"L",
           "TTG":"L", "CTT":"L", "CTC":"L", "CTA":"L",
           "CTG":"L","ATG":"M", "AAT":"N", "AAC":"N", 
           "CCT":"P", "CCC":"P", "CCA":"P", "CCG":"P",
           "CAA":"Q", "CAG":"Q", "CGT":"R", "CGC":"R",
           "CGA":"R", "CGG":"R", "AGA":"R", "AGG":"R",
           "TCT":"S", "TCC":"S", "TCA":"S", "TCG":"S",
           "AGT":"S", "AGC":"S", "ACT":"T", "ACC":"T",
           "ACA":"T", "ACG":"T", "GTT":"V", "GTC":"V",
           "GTA":"V", "GTG":"V", "TGG":"W", "TAT":"Y",
           "TAC":"Y","TAA":"_", "TAG":"_", "TGA":"_"
           }
    
    if codon.upper() in map:
        return map[codon]
    return None
```

15. Escreva uma função codon_plot que receba uma sequência de DNA e gere um histograma com a contagem de cada codão. Compare o resultado obtido com o [Codon Plot do SMS2](https://www.bioinformatics.org/sms2/codon_plot.html). Pode epxlorar os módulos matplotlib ou seaborn para fazer gráficos mais detalhados.

16. Estenda a função anterior para poder considerar a leitura noutras posições, i.e., começando nas posições 0, 1 e 2 para encontrar as 3 *reading frames* da sequência fornecida.
```python
def translate_dna_seq(dna_seq, init_pos):
    ...
```
Por exemplo:
```python
dna_seq='ATGGGGCTCAGCGAC'
print(translate_dna_seq(dna_seq)) # 'MGLSD'
print(translate_dna_seq(dna_seq, init_pos=1)) # 'WGSA'
print(translate_dna_seq(dna_seq, init_pos=2)) # 'GAQR'
```

17. Estenda a função anterior para que, dada uma sequência de DNA, sejam calculadas todas as *reading frames* possíveis (as 3 da *conding strand* e as 3 da *template strand*). Compare o resultado seguinte com o [SMS2 Translate](https://www.bioinformatics.org/sms2/translate.html). Por exemplo, de acordo com o SMS2, a sequência:
```python
dna_seq = 'AATGCTCGTAATTTA'
```
Deveria retornar:
```
Reading Frame 1, Direct: NARNL
Reading Frame 2, Direct: MLVI
Reading Frame 3, Direct: CS*F
Reading Frame 1, Reverse: *ITSI
Reading Frame 2, Reverse: KLRA
Reading Frame 3, Reverse: NYEH
```
18. Escreva uma função `read_genome` que leia um ficheiro `.fa` para que depois possam ser usadas as funções previamente definidas. Por exemplo:
```python
fname = input("Insert input filename")
seq = read_genome(fname)
if validate_dna(seq):
    print("Valid sequence")
    print("Transcription: ", transcript(seq))
    print("Reverse complement: ", reverse_complement(seq))
    print("GC Content: ", gc_content(seq))
    print("Translation: ", translate_seq(seq))
else: print("DNA Sequence is not valid")
```
