# Creación de carpetas compartidas en un Synology NAS

### **`NAS DSM 7.1`**

Las carpetas compartidas son los directorios básicos donde puedes almacenar y gestionar archivos y carpetas en tu Synology NAS. Antes de almacenar cualquier archivo, deberás crear al menos una carpeta compartida en DSM.

## Para crear una carpeta compartida:

1. Ve a Panel de control > Carpeta compartida y haz clic en Crear > Crear carpeta compartida.

2. Especifica un nombre y una descripción para la carpeta compartida.

3. En el campo Ubicación, haz clic en el menú desplegable y selecciona un almacenamiento en el que crear la carpeta compartida. Omite este paso si solo existe un almacenamiento.

4. Modifica las siguientes opciones si es necesario.

- **Ocultar esta carpeta compartida en "Mis sitios de red"**: Evita que la carpeta compartida aparezca en "Red" en el Explorador de archivos de Windows. Esta opción no afecta los privilegios de acceso de la carpeta compartida. Los usuarios que tengan los derechos de acceso adecuados a la carpeta compartida aún podrán acceder a ella ingresando  
  `\\nombre del servidor\nombre` de la carpeta compartida.

- **Ocultar subcarpetas y archivos a los usuarios sin permisos**: Esta función solo es compatible con SMB, AFP y File Station. Cuando esta opción está habilitada, un usuario sin privilegios de lectura no podrá ver subcarpetas ni archivos dentro de la carpeta compartida. Esto evita que los usuarios encuentren archivos y subcarpetas a los que no tienen permiso cuando se conectan a su Synology NAS y se confunden.

- **Activar papelera de reciclaje**: Cuando se eliminan archivos en la carpeta compartida, se moverán a una carpeta llamada #recycle. El acceso a la papelera de reciclaje puede estar limitado a usuarios que pertenezcan al grupo de administradores.

5. En las siguientes páginas, añade una medida de seguridad a esta carpeta compartida si es necesario.

- **Omitir**: Si no necesitas una medida de seguridad adicional para esta carpeta compartida, puedes omitir este paso.

- **Proteger esta carpeta compartida mediante cifrado**: Puedes cifrar el contenido para una protección de datos mejorada. Haz clic en Siguiente y modifica los siguientes ajustes de cifrado.

  - Especifica y confirma una nueva clave de cifrado. La clave de cifrado no puede incluir signos de igual (=), comas (,) o dos puntos (:).
  - Si has inicializado previamente el almacén de claves, estará disponible la opción Agregar clave de cifrado al Administrador de claves. Puedes habilitar esta opción para montar la carpeta cifrada automáticamente cuando se inicie el sistema.


6. En las siguientes páginas, modifica las siguientes opciones si es necesario.

- **Activar suma de comprobación de datos para una integridad avanzada de datos**: Esta opción aprovecha la suma de comprobación CRC32 y la escritura en copia para proteger las carpetas compartidas y garantizar la integridad de los datos. Esta opción solo se puede habilitar durante el proceso de creación de la carpeta compartida y no se puede modificar una vez creada la carpeta compartida.
- **Activar compresión de archivos**: Los datos en la carpeta compartida creada se comprimirán automáticamente por el sistema de archivos Btrfs para ahorrar espacio de almacenamiento. Cuando se recuperen para su uso, los datos se descomprimirán automáticamente.

- **Activar cuota de carpeta compartida**: Para especificar la capacidad máxima para cada carpeta compartida, marca la casilla de verificación Activar cuota de carpeta compartida e introduce la capacidad máxima (por ejemplo, 10 GB) en el siguiente campo.

7. Revisa tus ajustes y haz clic en Aplicar para finalizar.
