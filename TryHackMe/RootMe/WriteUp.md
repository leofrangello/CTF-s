# Root Me WriteUp
 - Difficulty: Easy

### Task 2 - Reconnaissance
- Primeiro de tudo vamos executar o nmap para fazer um portscan e descobrir quais portas estão abertas juntamente com os serviços (e suas respectivas versões) que estão rodando em cada porta 'nmap -sV <ip maquina>' 
- Após o nmap finalizar o scan, iremos poder responder as 3 primeiras perguntas: 
 -- How many ports are open?
 -- What version of Apache is running?
 -- What service is running on port 22?

- Após isso iremos usar o dirb para procurar os diretórios que o servico web possui, utilizando o comando 'gobuster dir --url http://<ip_maquina/ --wordlist <path to wordlist> -t 30', após o gobuster terminar de executar teremos a resposta para a última pergunta da Task 2
 -- What is the hidden directory?

### Task 3 - Getting a Shell
- Entrei no diretório encontrado acima e tentei dar upload num arquivo .php porém recebi uma mensagem que PHP não é permitido. 
- Após isso, fui atrás de uma maneira de bypassar o file upload que restringe o .php, descobrindo que posso modificar a extensão do arquivo para .phtml (por exemplo) que ele ainda será lido como .php e assim irei conseguir o shell reverso. 
- Então fui até o site revshells.com e gerei um código de reverse shell como podem ver a seguir:

-Observação: o ip que coloquei no site, foi o ip do turn0 e não o do eth0 (que você pode conferir usando o comando 'ifconfig')
-Então dei upload no arquivo e utilizei o nc para escutar na porta 33456 'nc -lnvp 33456'. Fui no diretorio <ip maquina>/uploads/ e cliquei no arquivo .phtml e assim consegui o shell reverso 


- E como podemos ver acima temos o nosso shell. Para encontrar a flag do usuário eu utilizei o comando 'find / -name user.txt'

- Após isso dei um 'cat <caminho flag' e pronto, conseguimos responder a pergunda da Task 3

### Task 4 - Privilege Escalation

- Agora temos que escalar o privilégio para conseguir a flag do root. A primeira pergunta da task 4 nos da uma dica para onde devemos ir (Search for files with SUID permission, which file is weird?). Então utilizei o comando 'find / -user root -perm /4000'. Após isso teremos encontrado nosso arquivo estranho. 

- Usando a dica da 2ª pergunta, fui até o https://gtfobins.github.io/ e procurei por Python. Como na questão anterior havia falado sobre SUID encontrei o seguinte comando: 


- Após executá-lo conseguimos verificar que escalamos o privilégio e somos o root. 
- Então fui até o diretório do root 'cd /root/' e usei o comando ls, após isso utilizei o comando cat root.txt e consegui a última flag. 