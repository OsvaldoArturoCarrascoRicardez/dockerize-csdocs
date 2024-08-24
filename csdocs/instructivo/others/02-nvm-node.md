# Instalacion y Configuracion NVM NODE y NPM

### **`NODE y NPM`**

Para instalar NVM (Node Version Manager) en Ubuntu 22.04, sigue estos pasos:

### 1. **Actualizar el sistema**

Antes de comenzar, asegúrate de que tu sistema esté actualizado:

```bash
sudo apt update && sudo apt upgrade -y
```

### 2. **Instalar dependencias necesarias**

NVM necesita algunas dependencias para funcionar correctamente. Instálalas ejecutando:

```bash
sudo apt install curl build-essential libssl-dev -y
```

### 3. **Descargar e instalar NVM**

Descarga e instala NVM usando `curl`. La versión más reciente de NVM se puede encontrar en su [repositorio de GitHub](https://github.com/nvm-sh/nvm). El siguiente comando descarga e instala la versión más reciente de NVM:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
```

> **Nota:** Asegúrate de que la versión `v0.39.5` sea la más reciente al momento de la instalación. Puedes verificar la versión más reciente en el [repositorio de NVM en GitHub](https://github.com/nvm-sh/nvm).

### 4. **Cargar NVM en tu terminal**

Después de instalar NVM, necesitas cargarlo en tu sesión de terminal actual. Esto se hace agregando los scripts de inicialización al archivo de configuración de tu terminal.

Para `bash`, ejecuta:

```bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

Para que estos cambios sean permanentes, agrégalos al final de tu archivo `~/.bashrc`:

```bash
echo 'export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"' >> ~/.bashrc
echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> ~/.bashrc
echo '[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"' >> ~/.bashrc
```

Luego, recarga tu terminal:

```bash
source ~/.bashrc
```

Si estás utilizando `zsh` o `fish`, asegúrate de agregar estas líneas a tu archivo de configuración correspondiente (`~/.zshrc` para `zsh` o `~/.config/fish/config.fish` para `fish`).

### 5. **Verificar la instalación de NVM**

Para verificar que NVM se haya instalado correctamente, ejecuta:

```bash
nvm --version
```

Deberías ver un número de versión de NVM si la instalación fue exitosa.

### 6. **Instalar Node.js usando NVM**

Ahora que NVM está instalado, puedes instalar cualquier versión de Node.js. Por ejemplo, para instalar la versión LTS más reciente de Node.js, usa:

```bash
nvm install --lts
```

Para instalar una versión específica de Node.js (por ejemplo, la versión 18):

```bash
nvm install 18
```

### 7. **Verificar la instalación de Node.js**

Una vez instalada, puedes verificar la versión de Node.js y npm ejecutando:

```bash
node -v
npm -v
```

### 8. **Cambiar entre versiones de Node.js**

Puedes cambiar fácilmente entre diferentes versiones de Node.js que hayas instalado usando NVM. Para ver las versiones instaladas, usa:

```bash
nvm list
```

Para cambiar a una versión específica de Node.js:

```bash
nvm use <version>
```

Por ejemplo:

```bash
nvm use 18
```

### ¡Listo!

Has instalado con éxito NVM en Ubuntu 22.04 y ahora puedes gestionar fácilmente diferentes versiones de Node.js.