
# Instrucciones para la instalación y configuración de Nginx en macOS

### 1. Instalar Xcode Command Line Tools
Este paso es necesario para obtener las utilidades necesarias para compilar software.

```bash
xcode-select --install
```

### 2. Instalar Homebrew
Homebrew es un gestor de paquetes para macOS. Puedes instalarlo usando el siguiente comando:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 3. Descargar y descomprimir el tarball de Nginx
Descarga la versión de Nginx que desees y descomprime el archivo tar.gz.

### 4. Ejecutar el archivo `configure` para Nginx
Dentro de la carpeta descomprimida de Nginx, ejecuta el siguiente comando para configurar el entorno de instalación. Cambia la ruta según donde quieras instalar Nginx:

```bash
./configure --prefix=/ruta/de/tu/elección
```

### 5. Compilar Nginx
Una vez configurado, compila Nginx con el siguiente comando:

```bash
make
```

### 6. Instalar Nginx
Para instalar Nginx en la ruta especificada:

```bash
make install
```

### 7. Iniciar Nginx
Navega a la carpeta `sbin` de tu instalación de Nginx y ejecuta el siguiente comando para iniciar el servidor:

```bash
./nginx
```

### 8. Detener Nginx
Si necesitas detener el servidor, puedes usar el siguiente comando:

```bash
./nginx -s stop
```

### 9. Cerrar todos los procesos de Nginx
Si deseas asegurarte de que todos los procesos de Nginx están cerrados:

```bash
sudo pkill nginx
```

### 10. Verificar si hay algún proceso de Nginx corriendo
Para comprobar si hay procesos de Nginx en ejecución:

```bash
ps aux | grep nginx
```

---

## Para incluir un proyecto Angular

Si quieres integrar un proyecto Angular con Nginx, sigue estos pasos adicionales:

### 1. Build del proyecto Angular
Asegúrate de que tu proyecto Angular esté listo para producción. Si no has generado el build, navega a tu proyecto Angular y ejecuta:

```bash
ng build
```

Esto generará los archivos compilados en la carpeta `dist/` dentro de tu proyecto.

### 2. Copiar los archivos de Angular al directorio HTML de Nginx
Copia el contenido de la carpeta `dist/` generada en el paso anterior al directorio HTML de Nginx:

```bash
cp -r /ruta/de/tu/proyecto-angular/dist/* /ruta/de/instalación/nginx/html/
```

### 3. Configuración adicional para manejar rutas en Angular
Edita el archivo `nginx.conf` en el directorio de instalación de Nginx. Dentro del bloque `server`, agrega lo siguiente:

```bash
location / {
    root   /ruta/completa/al/directorio/dist/angular/; # Reemplaza con la ruta absoluta del directorio dist de Angular
    index  index.html index.htm;
    try_files $uri $uri/ /index.html; # Angular maneja las rutas a través del index.html
}
```

Guarda los cambios y reinicia Nginx para que la configuración surta efecto.
