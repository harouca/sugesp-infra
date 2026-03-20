**Servidor:** Zabbix
**IP:** 10.15.0.5
**Porta:** 10050 (Zabbix)
**Sistema:** Debian 13

**Serviços instalados:**
- Zabbix
- Apache/2.4.66 (Debian) [Apache](/runbooks/apache.md)
- MariaDB

** Token ID **: zabbix@pve!zabbix
** Secret **: 0891b386-3d81-4525-9958-b3a0fee8e3ab

** Configurações MariaDB **:
- Usuário: zabbix
- Senha: zabbix

** Melhorias realizadas no sistema para desempenho no Zabbix**
- /etc/sysctl.conf

~~~bash
vm.swappiness=10
fs.file-max=100000
~~~

** Apache2 **
Document Root: /var/www/html

** MariaDB **
Login: Root
Password: .Nti...(Padrão GTI)

Login: zabbix
Password: Pass@zabbix26

** PHP 8.2 ***
~~~bash
apt install -y php php-mysql php-gd php-xml php-bcmath php-mbstring php-ldap php-json php-curl php-zip libapache2-mod-php

~~~



