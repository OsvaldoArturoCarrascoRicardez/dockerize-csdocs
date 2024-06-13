````markdown
# Actualizar dependencias

```bash
sudo dnf update -y
```
````

Instala extensiones de PHP

```bash
sudo dnf install php php-common php-cli php-fpm php-gd php-json php-mbstring php-mysqlnd php-curl php-pear php-bcmath php-opcache php-pdo php-pecl-zip php-xml php-devel -y
sudo dnf install make
```

Resetea el módulo PHP

```bash
sudo dnf module reset php -y
```

Habilita el módulo de PHP 7.3 y establece la versión 7.3 como la predeterminada

```bash
sudo dnf module enable php:7.3 -y
sudo dnf update php\*
```

Verifica la lista de módulos PHP nuevamente para confirmar que el módulo de PHP 7.3 está habilitado y marcado como predeterminado

```bash
sudo dnf module list php
```

Finalmente, verifica la versión de PHP en tu sistema para confirmar que se ha cambiado a la versión 7.3

```bash
php -v
```

Eliminamos archivos temporales

```bash
sudo rm -rf /tmp/mongo-php-driver /usr/src/mongo-php-driver
```

Bajamos el driver de mongo para PHP y lo contruimos

```bash
sudo git clone -c advice.detachedHead=false -q -b '1.12.0' --single-branch https://github.com/mongodb/mongo-php-driver.git /tmp/mongo-php-driver
sudo mv /tmp/mongo-php-driver /usr/src/mongo-php-driver
cd /usr/src/mongo-php-driver
sudo git submodule -q update --init
sudo phpize
sudo ./configure --with-php-config=/usr/bin/php-config > /dev/null
sudo make clean > /dev/null
sudo make >/dev/null 2>&1
sudo make install
```

Localizamos el archivo php.ini

```bash
php -i | grep "Loaded Configuration File"
```

Agregamos la extensión al archivo ini

```bash
sudo vim /etc/php.ini  (agregar `extension=mongodb.so`)
```

Crea el archivo mongodb.ini en el directorio /etc/php.d/

```bash
sudo bash -c "echo 'extension=mongodb.so' > /etc/php.d/mongodb.ini"
```

Crea los enlaces simbólicos correspondientes para el archivo de configuración

```bash
sudo ln -s /etc/php.d/mongodb.ini /etc/php.d/20-mongodb.ini
```

Reinicia el servicio de PHP-FPM

```bash
sudo systemctl restart php-fpm
```

Verificamos extensión de mongo

```bash
php -m
```