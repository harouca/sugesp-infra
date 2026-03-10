# Instalação do GPLI #

Este documento apresenta as instruções para a instalação do GLPI, com as adaptações ao servidor Buchenavia da Superintendência de Gestão de Pessoas (SUGESP). Entretanto, a versão já deve estar instalada, sendo este documento apenas para consulta, porém, com foco na atualização.

## Atenção ao atualizar ##
Antes de efetuar a atualização, é necessário entender e saber como está a atual estrutra e como está instalado o GLPI. 
No servidor hospedado ele está instalado em /opt/sgp/www no diretório GLPI. Seguimos o padrão da versão 9, da documentação oficial.

### Instalação atual ###
**Local**: /opt/sgp/www/glpi
**Local do HTML**: /opt/sgp/www/html

### Configuração do GLPI ###
/etc/glpi - Configurações do GLPI
/var/lib/glpi - Arquivos do GLPI - Variáveis
/var/log/glpi - Logs do GLPI

Para que o GLPI saiba onde estão os arquivos, eles são definidos no arquivo:
/opt/sgp/www/glpi/inc/downstream.php
'''
~~~php
<?php
define('GLPI_CONFIG_DIR', '/etc/glpi/');

if (file_exists(GLPI_CONFIG_DIR . '/local_define.php')) {
   require_once GLPI_CONFIG_DIR . '/local_define.php';
}
~~~

## Referências ##
https://glpi-install.readthedocs.io/pt/latest/ (Fonte oficial)
https://www.mindtek.com.br/2025/10/guia-de-instalacao-do-glpi-11/ (Fonte de consulta em Português)