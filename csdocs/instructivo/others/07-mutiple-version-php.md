# Usar Multiples Versiones de PHP Ubuntu 22.04

### **`Multiple Version`**

Instalar las versiones de PHP necesarias junto con sus extensiones, seguiar guias de instalacion correspondientes:

1. **Crear archivo de configuracion por cada version de PHP**:

```bash
sudo vim /usr/local/bin/php81
```

2. **Pegar**:

```bash
#!/bin/bash
update-alternatives --set php /usr/bin/php8.1
```

3. **Asignar Permisos**:

```bash
sudo chmod 777 /usr/local/bin/php81
```

4. **Repetir por cada versiond e PHP Instalada**:

Para usar comando de composer y artisan hay que cambiar de version ejecutando, sea el caso de la version a utilizar:

```bash
sudo php81 -v
```

Esto hara un swich de version, test

```bash
php -v
```

Vera que esta en uso la nueva version, con esto ya podra ejecutar composer y artisan en sus proyectos que lo requieran

**NOTA**:

Si se actualiza un proyecto hay que cambiar la version de /var/run/php/php8.1-fpm.sock, en el archivo de nginx, sea el caso de uso.

```bash
sudo systemctl restart nginx
```
