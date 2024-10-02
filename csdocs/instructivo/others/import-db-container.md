### Resumen de comandos:

```bash
sudo mysqldump -u control_gestion -p --routines -h 10.14.1.95 controlgestion | gzip -9 > dump_20230714.sql.gz
```

1. Copiar archivo al contenedor:

   ```bash
   docker cp dump_20240927.sql.gz <nombre_o_id_contenedor>:/tmp/dump_20240927.sql.gz
   ```

2. Acceder al contenedor:

   ```bash
   docker exec -it <nombre_o_id_contenedor> bash
   ```

3. Descomprimir archivo:

   ```bash
   cd /tmp
   gunzip dump_20240927.sql.gz
   ```

4. Crear base de datos (si es necesario):

   ```bash
   mysql -u root -p -e "CREATE DATABASE controlgestion_fnz;"

   mysql -u root -p -e "SET GLOBAL log_bin_trust_function_creators = 1;"
   ```

5. Importar volcado:

   ```bash
   mysql -u root -p controlgestion_fnz < /tmp/dump_20240927.sql
   ```

   Regresar config

   ```bash
   mysql -u root -p -e "SET GLOBAL log_bin_trust_function_creators = 0;"
   ```

Con esto, tu base de datos `controlgestion_fnz` debería estar restaurada en tu contenedor Docker.

Actualizar password de prueba a todos los usuarios, (12345)

```bash
UPDATE user
SET password = '$2y$10$DfGAcow9yDR88aaMqojOLu5DZtjMWXRtImhzIjC.NnU1QNl9gGi.K';
```
