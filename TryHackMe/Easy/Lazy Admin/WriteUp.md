# Lazy Admin
 - Difficulty: Easy

### Task 1

- Pra começar utilizei o comando nmap -sV -sC <ip alvo> para realizar um port scan, mostrando os serviços e suas respectivas versões em cada porta, assim como testar os scripts default do nmap em cada uma das portas. O resultado do comando vocês podem conferir abaixo:

- Após isso, utilizei também o gobuster para descobrir diretórios que sejam interessantes (pois há uma porta 80 aberta com serviço http). Então o comando utilizado foi gobuster dir -u http://<ip alvo>/ -w <caminho para a wordlist> -t 30. O diretórios encontrados vocês podem ver logo abaixo:

 

- Achamos o diretório /content, porém não havia mais nada dentro dele, então usei novamente o gobuster mas dessa vez no /content para descobrir novos diretórios, o resultado vocês podem ver a seguir: 


- No /content/as há uma página de login, no qual ainda não temos as credencias para conseguir logar, então vamos procurar em outro diretório.


- Entrando nos diretórios o que terá as coisas mais interessantes será o /content/inc, no qual há um backup do banco de dados. Abrimos o backup e temos o usuário e a senha:

- Porém a senha está criptografada, então teremos que descobrir qual a criptografia e quebrá-la. Para quebrar a criptografia você podera ir por 2 caminhos: Um deles usando o hash-identifier e depois utilizando o john the ripper, ou o outro caminho você pode procurar um hash identifier online e utilizá-lo (https://hashes.com/en/tools/hash_identifier), no caso desta última opção ele já trará a senha descriptografada. Abaixo estará ambos:
 

- Agora que temos a senha descriptografada poderemos logar no /content/as que haviamos encontrado anteriormente. Após fazer login, iremos até a aba "Ads" e poderemos colocar um código .php para realizar o reverse shell. (Você pode gerar o código do reverse shell, no site revshells.com, o ip que será colocado no IP & Port é o da sua máquina). 


- Depois de dar upload no arquivo, abrimos uma conexão utilizando o comando nc -lnvp <porta do rev shell> e clicamos no arquivo .php que estará no caminho /content/inc/ads/ após isso, a conexão terá sido aberta:


- Utilizando o comando locate user.txt podemos localizar a flag do usuário. Usando o comando cat <caminho para o user.txt> podemos responder a 1ª pergunta.

- Para encontrar a flag do root, utilizei o comando sudo -l para ver as permissões. Percebi que há um arquivo chamado /home/itguy/backup.pl então vamos ler ele com o comando cat.
- Aparecerá que ele roda um bashscript em /etc/copy.sh então vamos ler o arquivo:

- Apos isso, já sabemos que podemos modificá-lo devido as permissões que vimos, então faremos: 

- Agora, abriremos uma porta na nossa máquina (no meu caso 443) usando o nc -lnvp 443 e iremos executar o copy.sh para abrir a conexão reversa


- Bom, somos root agora. Só usar o comando locate root.txt e depois utilizar o comando cat para obter a flag.


