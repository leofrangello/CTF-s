# Simple CTF
 - Difficulty: Easy

### Task 1
- Pela primeira pergunta, já sei que terei que utilizar o nmap para realizar o port scan, então utilizarei nmap -sV -sC <ip_alvo> para realizar um scan nos serviços (e suas respectivas versões) e utilizar scripts padrões para verificar alguma vulnerabilidade

- Com o resultado do scan mostrado acima, conseguiremos responder as 2 primeiras perguntas.
- Sabendo que há uma porta 80 com um serviço web, utilizei o gobuster (gobuster dir -w <caminho para a wordlist> -u http://<ip maquina>/ -t 30) para encontrar diretórios úteis

- Como podemos ver, um único diretório recebeu o status 301, então, entrei no <ip maquina>/simple/ para ver o que havia lá dentro. O resultado está logo abaixo.

- Verifiquei se a versão do CMS Simple foi divulgada no site e sim, ela foi. 

- Então fazendo uma busca por CMS Simple 2.2.8 CVE, podemos responder as 2 próximas perguntas.

- No searchsploit procurei pelo Simple 2.2.8, e encontrei o código para o SQLi. Então, utilizei o locate para o nome do arquivo python (46635.py) e utilizei a seguinte linha de comando: python <caminho para o arquivo .py> -u <url>/simple --crack -w <caminho para wordlist> e o resultado será mostrado a seguir:

- E com isso conseguiremos responder as perguntas 5 e 6.

- Após isso, iremos conseguir nos conectar via ssh utilizando o usuário mitch. Então utilizamos o comando ssh mitch@<ip maquina> -p 2222 (como foi mostrado no portscan) como mostrado logo abaixo:

- Utilizei o comando ls e encontrei a flag do usuário, respondendo assim a pergunta 7
- Para responder a pergunta número 8, basta utilizar o comando cd /home e em seguida utilizar o comando ls. 
- Utilizando o comando sudo -l, percebi que o usuário mitch pode utilizar o /usr/bin/vim, e pela pergunta sabemos que será por esse meio que escalaremos o privilégio para root. Então fui até o GTFOBins encontrei o seguinte comando:

- Após rodar o comando, utilizei o sudo su - e pronto estamos como root. Utilizei o comando ls e está lá a flag do root.

