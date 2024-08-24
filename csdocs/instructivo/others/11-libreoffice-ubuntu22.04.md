# Instalacion y Configuracion LibreOffice Ubuntu 22.04


Para instalar los paquetes adicionales `dconf-gsettings-backend`, `dconf-cli`, `libgconf-2-4` y `libreoffice` en tu ambiente de Ubuntu 22.04.

### Pasos para Instalar en Ubuntu 22.04

1. **Actualizar los índices de paquetes de `apt`**:

   Antes de instalar nuevos paquetes, asegúrate de que tu lista de paquetes esté actualizada.

   ```bash
   sudo apt-get update
   ```

2. **Instalar los paquetes necesarios**:

   Ejecuta el siguiente comando para instalar `dconf-gsettings-backend`, `dconf-cli`, `libgconf-2-4`, y `libreoffice`:

   ```bash
   sudo apt-get install -y dconf-gsettings-backend dconf-cli libgconf-2-4 libreoffice
   ```

   - **`dconf-gsettings-backend`**: Es un backend para GSettings, que proporciona una manera para que las aplicaciones almacenen y recuperen configuraciones de usuario.
   - **`dconf-cli`**: Herramienta de línea de comandos para interactuar con el sistema de configuración `dconf`.
   - **`libgconf-2-4`**: Biblioteca de compatibilidad para el viejo sistema GConf utilizado en aplicaciones GNOME más antiguas.
   - **`libreoffice`**: Conjunto de productividad de oficina que incluye Writer, Calc, Impress, y otros.

3. **Crear directorios de caché y configuración**:

   Crear los directorios y ajusta los permisos con los siguientes comandos:

   ```bash
   mkdir -p /var/www/.config /var/www/.cache/dconf
   sudo chown -R www-data:www-data /var/www/.config /var/www/.cache/dconf
   ```

   - **`mkdir -p /var/www/.config /var/www/.cache/dconf`**: Crea los directorios necesarios para almacenar configuraciones y cachés.
   - **`sudo chown -R www-data:www-data /var/www/.config /var/www/.cache/dconf`**: Cambia la propiedad de estos directorios al usuario y grupo `www-data`.

### Verificación de la Instalación

Para asegurarte de que todo se ha instalado correctamente, puedes verificar cada componente:

- **LibreOffice**:

  ```bash
  libreoffice --version
  ```

  Esto debería mostrar la versión de LibreOffice instalada.
