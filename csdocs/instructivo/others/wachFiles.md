Para lograr esto en Python, puedes utilizar el módulo `watchdog`, que te permite monitorear los cambios en un directorio y detectar cuándo se agregan nuevos archivos. Además, puedes llevar un registro de los archivos ya procesados para evitar procesar los repetidos.

### Pasos generales:
1. **Monitorear el directorio**: Usa `watchdog` para detectar cuándo se agregan archivos nuevos.
2. **Registrar archivos procesados**: Mantén una lista o un archivo con los nombres de los archivos que ya han sido procesados.
3. **Procesar nuevos archivos**: Al detectar un archivo nuevo, verifica si ya ha sido procesado, si no, procesa el archivo y agrega su nombre a la lista de procesados.

### Instalación de `watchdog`
Primero, instala la librería `watchdog` si no la tienes:
```bash
pip install watchdog
```

### Código de ejemplo
A continuación, te muestro un ejemplo básico para monitorear un directorio y procesar solo los archivos nuevos:

```python
import time
import os
from watchdog.observers import Observer
from watchdog.events import FileSystemEventHandler

# Ruta al directorio que quieres monitorear
DIRECTORY_TO_WATCH = "/ruta/a/tu/directorio"

# Archivo donde se guardan los nombres de archivos ya procesados
PROCESSED_FILES_LOG = "processed_files.txt"

# Función para leer los archivos ya procesados
def load_processed_files():
    if os.path.exists(PROCESSED_FILES_LOG):
        with open(PROCESSED_FILES_LOG, "r") as file:
            return set(line.strip() for line in file)
    return set()

# Función para agregar un archivo al log de procesados
def save_processed_file(filename):
    with open(PROCESSED_FILES_LOG, "a") as file:
        file.write(f"{filename}\n")

# Función para procesar el archivo (puedes extraer el texto aquí)
def process_file(filepath):
    print(f"Procesando archivo: {filepath}")
    # Aquí puedes implementar la lógica para extraer el texto
    # Por ejemplo, leer el archivo, extraer contenido, etc.

# Clase para manejar eventos de archivos
class FileEventHandler(FileSystemEventHandler):
    def __init__(self, processed_files):
        self.processed_files = processed_files

    def on_created(self, event):
        # Si el archivo no está en la lista de procesados
        if not event.is_directory and event.src_path not in self.processed_files:
            filename = os.path.basename(event.src_path)
            process_file(event.src_path)
            self.processed_files.add(event.src_path)
            save_processed_file(filename)

if __name__ == "__main__":
    # Cargar archivos ya procesados
    processed_files = load_processed_files()

    # Procesar los archivos existentes al iniciar
    for filename in os.listdir(DIRECTORY_TO_WATCH):
        filepath = os.path.join(DIRECTORY_TO_WATCH, filename)
        if filepath not in processed_files:
            process_file(filepath)
            processed_files.add(filepath)
            save_processed_file(filename)

    # Monitorear el directorio para archivos nuevos
    event_handler = FileEventHandler(processed_files)
    observer = Observer()
    observer.schedule(event_handler, DIRECTORY_TO_WATCH, recursive=False)

    # Iniciar la observación
    observer.start()
    try:
        while True:
            time.sleep(1)
    except KeyboardInterrupt:
        observer.stop()
    observer.join()
```

### Explicación del código:

1. **Cargar archivos procesados**:
   - `load_processed_files`: Lee los nombres de archivos que ya han sido procesados de un archivo de log (`processed_files.txt`) y los almacena en un conjunto para evitar duplicados.

2. **Procesar archivos existentes**:
   - Antes de comenzar a monitorear el directorio, el programa procesa todos los archivos que ya están presentes en la carpeta y que no han sido procesados previamente.

3. **Monitoreo en tiempo real**:
   - La clase `FileEventHandler` es la encargada de manejar los eventos del sistema de archivos. Cuando se detecta la creación de un nuevo archivo, se verifica si ya ha sido procesado.
   - Si el archivo es nuevo, lo procesa y lo agrega a la lista de procesados.

4. **Guardado de archivos procesados**:
   - Cada vez que se procesa un archivo, se registra en `processed_files.txt` para evitar volver a procesarlo en futuras ejecuciones.

### Notas adicionales:
- **Reinicio seguro**: Al reiniciar el programa, este ya sabe cuáles archivos ha procesado gracias a `processed_files.txt`.
- **Extensibilidad**: Puedes personalizar la función `process_file` para extraer el texto de los archivos o realizar cualquier procesamiento adicional que necesites.
- **Optimización**: Si procesas grandes cantidades de archivos o necesitas optimizar el tiempo de procesamiento, podrías implementar procesos paralelos o en segundo plano para manejar el procesamiento de archivos de forma más eficiente.

Este programa básico te permitirá monitorear una carpeta y procesar solo los archivos nuevos.