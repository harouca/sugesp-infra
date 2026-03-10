# Infraestrutura da SUGESP

Este repositório contém a infraestrutura da SUGESP. Repositório com a finalidade de documentar as alterações em servidores e demais ativos de inraesrtutura, conforme as boas práticas de Gestão de Infraestrutura e Governança de TI.

O princípi básico é que toda alteração em infraestrutura deve ser documentada neste repositório, seguindo o layout básico e padronizado, conforme abaixo:

* Data e hora
* Responsável
* Servidor afetado
* O que foi alterado
* Motivo da alteração
* Como reverter (rollback)

### Exemplo simples de registro

**Data:** 09/03/2026 \n
**Servidor:** web01 \n
**Responsável:** Humberto \n

**Alteração:**
Atualização do PHP de 8.2.26 para 8.2.30

**Motivo:**
Correção de vulnerabilidade de segurança.

**Procedimento:**
```
apt update
apt upgrade php8.2*
```

**Impacto:**
Reinicialização do Apache.

**Roll back:**
```
apt install php8.2=8.2.26
```

# Servidores (links)

* [buchenavia](/Servidores/buchenavia.md) - VM dentro do Datacenter, hospeda o GLPI SUGESP (SIMAP) e VISIT.

# Incidentes e Problemas (links)
* [Incidentes e Problemas](incidentes.md)
