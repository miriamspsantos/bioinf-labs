# Processamento Básico de Sequências

## Exercícios

1. Escreva uma função `random_dna_sequence(length)` que crie uma sequência de DNA aleatória de tamanho `length`, com a mesma funcionalidade da [Random DNA Sequence do SMS2](https://www.bioinformatics.org/sms2/random_dna.html).
```python
def random_dna_sequence(length):
    """Creates a random DNA sequence of a given length"""
    pass
```
2. Escreva uma função `random_sequence(length, seq_type)` que altere a função anterior para também poder gerar sequências de RNA aleatórias:
```python
def random_sequence(length, seq_type):
    """Creates a random DNA/RNA sequence of a given length"""
    pass
```
3. Incorpore também a possibilidade de criar sequências aleatórias de proteínas, com a mesma funcionalidade da [Random Protein Sequence do SMS2](https://www.bioinformatics.org/sms2/random_protein.html). Para isso, pode considerar o seguinte alfabeto:
```python
PROTEIN_ALPHABET = "ACDEFGHIKLMNPQRSTVWY"
```

4. Escreva uma função `match(seq1, seq2)` para determinar se duas sequências são iguais.
```python
def match_seq(seq1, seq2):
    """
    Determines if two sequences are equal.
    Returns True if they are; False otherwise.
    """
```
5. Crie uma função `mutate_base(dna_seq, idx, base)` que introduza uma mutação pontual numa sequência de DNA, substituindo o nucleótido presente na posição `idx` por um nucleótido indicado em `base`.
```python
def mutate_base(seq, idx):
    """
    Introduces a point mutation at position idx
    by replacing the nucleotide with base.
    """
    pass
```
6. Crie uma função `validate_dna(dna_seq)` para verificar se a sequência de dna de *input* é válida (retorna `True` se for válida e `False` caso contrário).
```python
def validate_dna(dna_seq):
    """Evaluates if DNA sequence is valid."""
    pass
```
7. Generalize a função anterior (`validate_sequence(seq, alphabet)`) para validar também sequências de RNA e proteínas.
```python
def validate_sequence(seq, alphabet):
    """Evaluates if biologic sequence is valid."""
    pass
```
8. Crie uma função `count_nucleotides(dna_seq)` que retorne o número de cada nucleótido de uma sequência de DNA (considere a construção de um dicionário).
```python
def count_nucleotides(seq):
    """Counts the number of each nucleotide in a DNA sequence"""
    pass
```
9. Crie uma função `create_histogram(seq)` que permita imprimir um histograma das frequências dos nucleótidos numa sequência. Por exemplo, o código:
```python
seq = "ATCGGCGGA"
nt_lst = create_histogram(seq)
print(*nt_lst, sep="\n")
```
deve imprimir:
```python
A: **
T: *
G: ****
C: **
```
10. Crie uma função `gc_content(dna_seq)` que determine a percentagem de nucleótidos `C` e `G` na sequência.
```python
def gc_content(dna_seq):
    """Returns G/C content in the DNA sequence"""
    pass
```
11. Escreva um função `transcript(dna_seq)` que transcreva a sequência de DNA dada.
```python
def transcript(dna_seq):
    """Computes the RNA corresponding to the DNA sequence provided"""
    pass
```
12. Crie uma função `reverse(dna_seq)` que a partir de uma sequência de DNA gere o seu reverso. Compare o seu resultado com a função [Reverse Complement do SMS2](https://www.bioinformatics.org/sms2/rev_comp.html) (escolha a opção "reverse").
```python
def reverse(dna_seq):
    """Returns the reverse of the sequence"""
    pass
```
13. Crie uma função `complement(dna_seq)` que a partir de uma sequência de DNA gere o seu complemento. Compare o seu resultado com a função [Reverse Complement do SMS2](https://www.bioinformatics.org/sms2/rev_comp.html) (escolha a opção "complement").
```python
def complement(dna_seq):
    """Returns the complement of the sequence"""
    pass
```
14. Crie uma função `reverse_complement(dna_seq)` que a partir de uma sequência de DNA gere o seu complemento reverso (use as funções que acabou de criar!). Compare o seu resultado com a função [Reverse Complement do SMS2](https://www.bioinformatics.org/sms2/rev_comp.html) (escolha a opção "reverse complement").
```python
def reverse_complement(dna_seq):
    """Returns the reverse complement od the sequence"""
    pass
```
15. Escreva uma função `codon_usage(seq)` que conte a frequência de cada codão numa sequência de DNA. A função deve retornar um dicionário onde as chaves são os codões e os valores correspondem ao número de ocorrências de cada um.
```python
def codon_usage(seq):
    """
    Returns a dictionary with the frequency
    of each codon in the DNA sequence.
    """
    pass

seq = "ATGGCTATGGCT"
print(codon_usage(seq))
{'ATG': 2, 'GCT': 2}
```
16. Crie uma função `find_start_codons(seq)` que determine todas as posições onde ocorre o codão de início numa sequência de DNA.
```python
def find_start_codons(seq):
    """
    Returns the list of positions where
    the start codon ATG occurs in the sequence.
    """
    pass

seq = "ATGCGTATGAAATG"
print(find_start_codons(seq))
[0, 6, 11]
```
17. Escreva uma função `translate_seq(dna_seq)` que traduza uma sequência de DNA para uma cadeia de aminoácidos. Use a seguinte função `translate_codon(codon)`:
```python
def translate_seq(dna_seq):
    """ 
    Translates a DNA sequence strand into
    an aminoacid sequence (starting at offset 0)
    """
    pass

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

18. Escreva uma função `translate_dna_seq(dna_seq)` que estenda a função anterior para poder considerar a leitura noutras posições, i.e., começando nas posições 0, 1 e 2 para encontrar as 3 *reading frames* da sequência fornecida.
```python
def translate_dna_seq(dna_seq, init_pos=0):
    """
    Translates a DNA sequence strand into
    an aminoacid sequence (starting at offset init_pos)
    """
    pass
```
Por exemplo:
```python
dna_seq='ATGGGGCTCAGCGAC'
print(translate_dna_seq(dna_seq)) # 'MGLSD'
print(translate_dna_seq(dna_seq, init_pos=1)) # 'WGSA'
print(translate_dna_seq(dna_seq, init_pos=2)) # 'GAQR'
```

19. Escreva uma função `get_reading_frames(seq)` que, dada uma sequência de DNA, calcule todas as *reading frames* possíveis (as 3 da *conding strand* e as 3 da *template strand*). Compare o resultado seguinte com o [SMS2 Translate](https://www.bioinformatics.org/sms2/translate.html). Por exemplo, de acordo com o SMS2, a sequência:
```python
dna_seq = 'AATGCTCGTAATTTA'
```
Deveria retornar:
```
Reading Frame 1, Direct: NARNL
Reading Frame 2, Direct: MLVI
Reading Frame 3, Direct: CS_F
Reading Frame 1, Reverse: _ITSI
Reading Frame 2, Reverse: KLRA
Reading Frame 3, Reverse: NYEH
```
20. Escreva uma função `read_fasta(filename)` que leia um ficheiro `.fasta` para que depois possam ser usadas as funções previamente definidas. Por exemplo:
```python
seq = read_fasta("filename.fasta")
if validate_dna(seq):
    print("Valid sequence")
    print("Transcription: ", transcript(seq))
    print("Reverse complement: ", reverse_complement(seq))
    print("GC Content: ", gc_content(seq))
    print("Translation: ", translate_seq(seq))
else: print("DNA Sequence is not valid")
```
Use um ficheiro fasta de mRNA do NCBI para validar os seus resultados.

<!--
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
15. Escreva uma função codon_plot que receba uma sequência de DNA e gere um histograma com a contagem de cada codão. Compare o resultado obtido com o [Codon Plot do SMS2](https://www.bioinformatics.org/sms2/codon_plot.html). Pode epxlorar os módulos matplotlib ou seaborn para fazer gráficos mais detalhados.
-->