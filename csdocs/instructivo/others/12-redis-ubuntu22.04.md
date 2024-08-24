# Instalacion y Configuracion Redis Ubuntu 22.04

Para instalar y configurar Redis para trabajar con Laravel 10, sigue estos pasos. Te guiaré a través de la instalación de Redis en Ubuntu, la configuración de Redis para Laravel, y la instalación del paquete PHP para Redis.

### 1. Instalar Redis en Ubuntu

1. **Actualizar los índices de paquetes**:

   Abre una terminal y ejecuta:

   ```bash
   sudo apt-get update
   ```

2. **Instalar Redis**:

   Ejecuta el siguiente comando para instalar Redis:

   ```bash
   sudo apt-get install redis-server
   ```

3. **Verificar la instalación de Redis**:

   Para asegurarte de que Redis está corriendo, puedes usar el comando:

   ```bash
   redis-cli ping
   ```

   Deberías obtener la respuesta `PONG`.

4. **Configurar Redis para que se inicie automáticamente**:

   Asegúrate de que Redis se inicie automáticamente al arrancar el sistema:

   ```bash
   sudo systemctl enable redis-server
   ```
