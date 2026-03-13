# Instalação / Atualização do GPLI #

Este documento apresenta as instruções para a instalação ou atualização do GLPI, com as adaptações ao servidor Buchenavia da Superintendência de Gestão de Pessoas (SUGESP). Entretanto, a versão já deve estar instalada, sendo este documento apenas para consulta, porém, com foco na atualização.

## Atenção ao atualizar ##
Antes de efetuar a atualização, é necessário entender e saber como está a atual estrutra e como está instalado o GLPI. 
No servidor hospedado ele está instalado em /opt/sgp/www no diretório GLPI. Seguimos o padrão da versão 9, da documentação oficial.

### Instalação atual ###
**Local**: /opt/sgp/www/glpi  
**Local do HTML**: /opt/sgp/www/html  

### Configuração do GLPI ###
**/etc/glpi** - Configurações do GLPI  
**/var/lib/glpi** - Arquivos do GLPI - Variáveis  
**/var/log/glpi** - Logs do GLPI  

Para que o GLPI saiba onde estão os arquivos, eles são definidos no arquivo:
**/opt/sgp/www/glpi/inc/downstream.php**

**Conteúdo do arquivo downstream.php**  
~~~php
<?php
define('GLPI_CONFIG_DIR', '/etc/glpi/');

if (file_exists(GLPI_CONFIG_DIR . '/local_define.php')) {
   require_once GLPI_CONFIG_DIR . '/local_define.php';
}
~~~

No diretório **/etc/glpi** encontra-se o arquivo **local_define.php**, que define as variáveis que o GLPI precisa para saber onde estão os arquivos. Na atualização é importante manter e ter o backup por segurança.

### Permissões de Arquivos e Pastas ###
Para que os serviços do GLPI funcionem corretamente, é necessário que as permissões dos arquivos e pastas estejam corretas. Principalmente para que o Apache e o PHP saibam ler e escrever nos arquivos e pastas necessários.

~~~bash
# O código‑fonte permanece de propriedade do root
chown root:root /opt/sgp/www/html/glpi/ -R

# Conceder controle ao usuário do Apache (www-data) sobre os diretórios variáveis
chown www-data:www-data /etc/glpi    -R
chown www-data:www-data /var/lib/glpi -R
chown www-data:www-data /var/log/glpi -R
chown www-data:www-data /opt/sgp/www/html/glpi/marketplace -Rf

# Ajustar permissões de arquivos (0644) e diretórios (0755)
find /opt/sgp/www/glpi/ -type f -exec chmod 0644 {} \;
find /opt/sgp/www/glpi/ -type d -exec chmod 0755 {} \;
find /etc/glpi -type f -exec chmod 0644 {} \;
find /etc/glpi -type d -exec chmod 0755 {} \;
find /var/lib/glpi -type f -exec chmod 0644 {} \;
find /var/lib/glpi -type d -exec chmod 0755 {} \;
find /var/log/glpi -type f -exec chmod 0644 {} \;
find /var/log/glpi -type d -exec chmod 0755 {} \;

~~~

## Resumo para atualização ##
A cada processo de atualização, você deve fazer backup dos dados antes de iniciar qualquer atualização:

    * backup do seu banco de dados;  
    * backup do diretório de configuração;
    * backup dos diretórios que que contém os arquivos de usuários, plugins e arquivos gerados, tipo pdf, imagens, etc.;
    * backup dos diretórios **marketplace** e **plugins**;

## Referências ##
https://glpi-install.readthedocs.io/pt/latest/ (Fonte oficial)
https://www.mindtek.com.br/2025/10/guia-de-instalacao-do-glpi-11/ (Fonte de consulta em Português)