# Ejecucion Docker ( Suite CSDocs )

### Construir el contenedor

```bash
docker compose build
```

### Levantar Contenedor

```bash
docker compose up -d
```

### Configuración y acceso de phpMyAdmin a MySQL

En NAS configurar fullText e Index

```bash
cp /tmp/latin1.xml /usr/share/mysql-8.0/charsets/
cp /tmp/Index.xml /usr/share/mysql-8.0/charsets/
```

Para entrar a la consola de MySQL usa:

```bash
mysql -u root -p
```

Para entrar a la consola de MySQL usa:

```bash
mysql -u root -p
```

Dentro de la consola de MySQL ejecuta:

```sql
use mysql;
select user, plugin, host FROM mysql.user;

ALTER USER 'root'@'%' IDENTIFIED WITH caching_sha2_password BY 'Admcs1234567@';

GRANT ALL PRIVILEGES ON *.* TO 'root'@'%';

FLUSH PRIVILEGES;
exit
```

Para salir del contenedor:

```bash
exit
```

Para reiniciar el contenedor:

```bash
docker restart mysql
```
