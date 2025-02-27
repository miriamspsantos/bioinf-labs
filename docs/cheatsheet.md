| Comando  | Descrição | Exemplo | Explicação |
|----------|----------|---------|------------|
| `ls` | Lista os ficheiros e pastas na diretoria atual. | `ls -l` | Lista os ficheiros em formato detalhado. |
| `cd` | Muda para outra diretoria. | `cd /home/user` | Vai para a diretoria `/home/user`. |
| `pwd` | Mostra o caminho da diretoria atual. | `pwd` | Mostra o caminho completo da diretoria atual. |
| `mkdir` | Cria uma nova diretoria. | `mkdir novos_docs` | Cria a diretoria `novos_docs`. |
| `rmdir` | Remove uma diretoria vazia. | `rmdir antigos_docs` | Remove `antigos_docs`, se estiver vazio. |
| `rm` | Remove ficheiros ou pastas. | `rm -r pasta` | Remove a `pasta` e todo o seu conteúdo. |
| `cp` | Copia ficheiros ou pastas. | `cp ficheiro.txt backup/` | Copia `ficheiro.txt` para a pasta `backup/`. |
| `mv` | Move ou renomeia ficheiros e diretorias. | `mv ficheiro.txt novo_nome.txt` | Renomeia `ficheiro.txt` para `novo_nome.txt`. |
| `find` | Pesquisa ficheiros e diretorias no sistema. | `find /home -name "*.txt"` | Procura ficheiros `.txt` em `/home`. |
| `grep` | Pesquisa padrões de texto dentro de ficheiros. | `grep "erro" log.txt` | Procura a palavra "erro" dentro de `log.txt`. |
| `tar` | Compacta ou extrai ficheiros. | `tar -cvf backup.tar pasta/` | Cria um ficheiro `backup.tar` com os ficheiros da `pasta/`. |
| `zip` / `unzip` | Compacta e descompacta ficheiros ZIP. | `zip arquivo.zip documento.txt` | Compacta `documento.txt` em `arquivo.zip`. |
| `wget` | Faz download de ficheiros da web. | `wget http://site.com/ficheiro.zip` | Baixa `ficheiro.zip` do site especificado. |
| `curl` | Transferência de dados via protocolos variados. | `curl -O http://site.com/ficheiro.zip` | Faz download de `ficheiro.zip` usando `curl`. |
| `cat` | Mostra o conteúdo de um ficheiro. | `cat texto.txt` | Exibe o conteúdo do ficheiro `texto.txt`. |
| `less` | Visualiza ficheiros página a página. | `less texto.txt` | Permite navegar pelo ficheiro `texto.txt`. |
| `nano` | Editor de texto simples no terminal. | `nano texto.txt` | Abre `texto.txt` para edição no `nano`. |
| `echo` | Exibe mensagens no terminal. | `echo "Olá, Mundo!"` | Mostra a mensagem `"Olá, Mundo!"` no terminal. |
| `exit` | Sai da sessão atual do terminal. | `exit` | Fecha o terminal ou termina a sessão SSH. |
| `wc`      | Conta linhas, palavras e caracteres em ficheiros. | `wc -l ficheiro.txt` | Conta o número de linhas em `ficheiro.txt`. |
| `head`    | Mostra as primeiras linhas de um ficheiro. | `head -n 5 ficheiro.txt` | Mostra as primeiras 5 linhas de `ficheiro.txt`. |
| `tail`    | Mostra as últimas linhas de um ficheiro. | `tail -n 5 ficheiro.txt` | Mostra as últimas 5 linhas de `ficheiro.txt`. |
| `touch`   | Cria um ficheiro vazio ou atualiza a data de modificação. | `touch novo.txt` | Cria `novo.txt` se não existir ou atualiza sua data. |
| `whoami`  | Mostra o utilizador atualmente logado. | `whoami` | Retorna o nome do utilizador. |
| `date`    | Mostra a data e hora atuais. | `date` | Mostra a data e hora do sistema. |
| `man`     | Mostra o manual de um comando. | `man ls` | Mostra o manual do comando `ls`. |
| `basename`| Extrai o nome do ficheiro de um caminho (*path*). | `basename /home/user/documento.txt` | Retorna `documento.txt`. |
| `dirname` | Extrai a pasta de um caminho. | `dirname /home/user/documento.txt` | Retorna `/home/user`. |
| `uniq`    | Remove linhas duplicadas de um ficheiro. | `sort lista.txt | uniq` | Remove duplicados da lista ordenada. |
| `cut`     | Extrai partes específicas de linhas em ficheiros. | `cut -d"," -f2 dados.csv` | Mostra apenas as idades de um ficheiro `dados.csv` organizado como `Nome,Idade`. |
| `tr`      | Substitui ou remove caracteres em texto. | `echo "teste" | tr 'e' 'a'` | Substitui `"e"` por `"a"` na palavra `"teste"` (*tasta*). |
