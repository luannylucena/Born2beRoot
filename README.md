# Born2beRoot

### Neste projeto, aprendi sobre virtualização, administração de sistemas e políticas de segurança para configurar meu primeiro servidor SSH básico! A máquina virtual foi configurada no Oracle VirtualBox. O sistema operacional escolhido foi a versão estável do Debian GNU/Linux, e utilizei o gerenciador de pacotes apt para instalar as ferramentas usadas para impor políticas mínimas de segurança, como:

- configuração de um firewall usando `UFW`
- configuração da administração do sistema com `sudo`
- implementação de uma política de senha forte usando `libpam-quality`
- configuração de uma tarefa `cron` para executar um script de monitoramento a cada 10 minutos

### Para configurar corretamente nosso Debian, utilizamos vários comandos que serão listados abaixo:

#### GERAL

- Para verificar as informações do sistema operacional: `cat /etc/os-release`
- Para verificar nossas partições: `lsblk`
- Para verificar se o gerenciador de pacotes está instalado: `apt --version`
- Para sair da sessão atual: `exit`
- Para conectar-se como um usuário diferente: `su other_username`
- Para reiniciar o sistema: `sudo systemctl reboot`

#### SUDO
- Para instalar o sudo: `apt install sudo (como root)`
- Para adicionar um usuário ao grupo sudo: `sudo usermod -aG sudo nome_do_usuário`
- Para alterar a configuração do sudo: `sudo visudo`

#### UFW 

- Para instalar ufw: `apt install ufw`
- Para ativar o ufw: `sudo ufw enable`
- Para verificar o status do ufw: `sudo ufw status verbose`
- Para criar uma regra:  `sudo ufw default deny/allow outgoing`
- Para criar uma regra de porta: `sudo ufw allow/deny 4242`
- Para remover uma regra: `sudo ufw delete allow/deny 8080`

#### SSH

- Para instalar o OpenSSH: `sudo apt install openssh-server`
- Para verificar se está em execução: `sudo systemctl status ssh`
- Para alterar as configurações do ssh: `sudo nano /etc/ssh/sshd_config`
- Para reiniciar o serviço ssh: `sudo systemctl restart ssh`
- Para acessar a máquina virtual via ssh: `ssh <nome_de_usuário_servidor>@<endereço_IP_do_servidor> -p <porta>`
- Para encerrar uma sessão ssh: `exit`

POLÍTICA DE SENHA FORTE

- Para alterar as regras de senha: `sudo nano /etc/login.defs`
- Para modificar os parâmetros de senha para o usuário root e usuários existentes: `sudo chage -M/-m/-W <nome_de_usuário/root>`
- Para instalar uma biblioteca para verificação de senha: `sudo apt install libpam-pwquality`
- Para editar o arquivo de configuração: `sudo nano /etc/security/pwquality.conf`
- Para alterar a senha: `sudo passwd <usuário/root>`

NOME DO HOST

- Para alterar o nome do host: `sudo hostnamectl set-hostname`
- Para verificar o nome do host atual: `hostnamectl status`

GERENCIAMENTO DE USUÁRIOS

- Para criar um novo usuário: `useradd`
- Para alterar os parâmetros do usuário: `usermod -l (para o nome de usuário) -c (para o nome completo)`
- Para excluir um usuário: `userdel -r`
- Para exibir todos os usuários no sistema: `cat /etc/passwd | cut -d ":" -f1`

GERENCIAMENTO DE GRUPOS

- Para criar um novo grupo: `groupadd`
- Para adicionar um usuário a um grupo: `gpasswd -a`
- Para remover um usuário de um grupo: `gpasswd -d`
- Para excluir um grupo: `groupdel <nome_do_grupo>`
- Para exibir uma lista de todos os usuários em um grupo: `getent group`

CRON / COMANDOS PARA O SCRIPT DE MONITORAMENTO

- Para configurar uma rotina no cron: `crontab -e`
- Para ver a arquitetura de um sistema operacional: `uname -a`
- Para ver o número de processadores físicos: `grep "physical id" /proc/cpuinfo | sort | uniq | wc -l`
- Para ver o número de processadores virtuais: `grep "^processor" /proc/cpuinfo | wc -l`
- Para ver a memória RAM disponível: `free -m | awk '$1 == "Mem:" {print $2}'`
- Para ver a memória RAM total: `free -m | awk '$1 == "Mem:" {print $3}'`
- Para calcular a porcentagem de memória RAM usada: `(free | awk '$1 == "Mem:" {printf("%.2f"), $3/$2*100}')`
- Para ver a memória disponível no servidor: `df -Bg | grep '^/dev/' | grep -v '/boot$' | awk '{ft += $4} END {print ft}'`
- Para ver a memória total: `df -Bg | grep '^/dev/' | grep -v '/boot$' | awk '{ut += $3} END {print ut}'`
- Para ver o uso da CPU: `top -bn1 | grep '^%Cpu' | cut -c 9- | awk '{printf("%.1f%%"), $1 + $2 + $3}'`
- Para ver a data e hora do último boot: `who -b | awk '$1 == "system" {print $3 " " $4}'`
- Para ver se o LVM está ativo ou não: `if [ $(lsblk | grep "lvm" | wc -l) -eq 0 ]; then echo no; else echo yes; fi`
- Para ver quantas conexões TCP estão estabelecidas: `cat /proc/net/sockstat{,6} | awk '$1 == "TCP:" {print $3}'`
- Para ver o número de usuários logados: `users | wc -w`
- Para ver o IP desta máquina: `hostname -I`
- Para ver o endereço MAC: `ip link show | awk '$1 == "link/ether" {print $2}'`
- Para contar quantos comandos com sudo foram usados na sessão atual: `journalctl _COMM=sudo | grep COMMAND | wc -l`

Este projeto também abrangeu o básico de criptografia, redes, particionamento de disco rígido e shell scripting.
