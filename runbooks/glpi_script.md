# Script de Backup do GLPI #
Fonte: https://www.youtube.com/watch?v=qjkglz0zgHQ


~~~bash
#!/bin/bash
 
# 1) Criar uma pasta chamada backup_glpi
BACKUP_DIR="/opt/sgp/www/backup_glpi/10.0.6"
GLPI_DIR="/opt/sgp/www/glpi"
NEW_GLPI_TGZ="https://github.com/glpi-project/glpi/releases/download/10.0.9/glpi-10.0.9.tgz"
 
mkdir -p "$BACKUP_DIR"
 
# 2) Logar no MySQL e fazer backup do banco de dados glpidb
DB_USER="glpi"
DB_PASSWORD="Glpi@sgp#9740"
DB_NAME="glpi"
 
mysqldump -u "$DB_USER" -p"$DB_PASSWORD" "$DB_NAME" > "$BACKUP_DIR/glpi_db_backup.sql"
 
# 3) Compactar e copiar todas as subpastas de files para backup_glpi, exceto as pastas _cron, _dumps, _cache, _lock, _locales, _log, _sessions, _rss
cd "$GLPI_DIR/files" && tar --exclude="_cron" --exclude="_dumps" --exclude="_cache" --exclude="_lock" --exclude="_locales" --exclude="_log" --exclude="_sessions" --exclude="_rss" -czvf "$BACKUP_DIR/files_selected_backup.tar.gz" *
 
# 4) Compactar e copiar a pasta plugins para backup_glpi
cd "$GLPI_DIR" && tar -czvf "$BACKUP_DIR/plugins_backup.tar.gz" "plugins"
 
# 5) Copiar o arquivo glpicrypt.key para backup_glpi
cp "/etc/glpi/glpicrypt.key" "$BACKUP_DIR/"
 
# 6) Compactar e copiar a pasta marketplace para backup_glpi
cd "$GLPI_DIR" && tar -czvf "$BACKUP_DIR/marketplace_backup.tar.gz" "marketplace"
 
# 7) Renomear a pasta glpi para glpi_old
mv "$GLPI_DIR" "${GLPI_DIR}-09_old"
 
# 8) Baixar e descompactar a versão atualizada do GLPI
wget -O "$BACKUP_DIR/glpi_latest.tgz" "$NEW_GLPI_TGZ"
tar -xzvf "$BACKUP_DIR/glpi_latest.tgz" -C "/opt/sgp/www/"
mv "/opt/sgp/www/glpi-10.0.9" "$GLPI_DIR"
 
# 9) Restaurar pastas e arquivos na nova instalação
mkdir -p "$GLPI_DIR/files"
tar -xzvf "$BACKUP_DIR/files_selected_backup.tar.gz" -C "$GLPI_DIR/files/"
tar -xzvf "$BACKUP_DIR/plugins_backup.tar.gz" -C "$GLPI_DIR/"
tar -xzvf "$BACKUP_DIR/marketplace_backup.tar.gz" -C "$GLPI_DIR/"
cp "$BACKUP_DIR/glpicrypt.key" "/etc/glpi/"
 
# 10) Dar permissão 777 na pasta glpi
chmod -R 777 "$GLPI_DIR"
 
echo "Atualização e restauração do GLPI concluídas com sucesso!"

~~~