# Passive Liveness CLI

Una herramienta de línea de comandos para evaluar imágenes con servicios de liveness, utilizando tanto APIs SaaS como SDKs locales.

## Características

- Evaluación de imágenes individuales o directorios completos
- Integración con servicios SaaS (Identity Platform) y SDK local
- Soporte para múltiples versiones del SDK (hasta 3)
- Generación de informes en formato Markdown
- Interfaz interactiva y modo de línea de comandos
- Procesamiento paralelo para mayor velocidad

## Instalación

1. Clona este repositorio:
   ```bash
   git clone https://github.com/Facephi-Backend-Support/liveness-cli.git
   cd liveness-cli
   ```

2. Instala las dependencias:
   ```bash
   pip install -r requirements.txt
   ```

## Uso

### Modo Interactivo

La forma más fácil de usar el CLI es en modo interactivo:

```bash
python liveness_cli.py --interactive
```

Esto iniciará un asistente que te guiará a través de todas las opciones.

### Modo Línea de Comandos

También puedes usar el CLI directamente desde la línea de comandos:

```bash
# Evaluar una imagen individual con el servicio SaaS
python liveness_cli.py --image ruta/a/imagen.jpg --use-saas --output informe.md

# Evaluar un directorio de imágenes con el servicio SDK en el puerto 8080
python liveness_cli.py --directory ruta/a/imagenes --use-sdk --sdk-port 8080 --sdk-version "6.12" --output informe.md

# Evaluar con SaaS y múltiples versiones de SDK
python liveness_cli.py --directory ruta/a/imagenes --use-saas --use-sdk --sdk-port 8080 9090 --sdk-version "6.12" "6.5" --output informe.md
```

## Opciones

### Configuración de Imágenes
- `--image`, `-img`: Ruta a una imagen individual para evaluar
- `--directory`, `-dir`: Directorio que contiene imágenes para evaluar

### Configuración de SaaS
- `--use-saas`: Usar el servicio SaaS para la evaluación
- `--saas-api-key`: API key para el servicio SaaS

### Configuración de SDK
- `--use-sdk`: Usar el servicio SDK local para la evaluación
- `--sdk-port`: Puerto(s) donde se ejecuta el servicio SDK local (máximo 3)
- `--sdk-version`: Versión(es) del SDK correspondiente a cada puerto

### Configuración del Informe
- `--output`, `-o`: Ruta donde guardar el informe generado

### Otras Opciones
- `--workers`, `-w`: Número de workers para procesamiento paralelo
- `--verbose`, `-v`: Mostrar información detallada durante la ejecución
- `--interactive`, `-i`: Ejecutar en modo interactivo

## Estructura del Código

El código está organizado de la siguiente manera:

- `liveness_cli.py`: Punto de entrada principal
- `config.py`: Constantes y configuración
- `image_processor.py`: Procesamiento y evaluación de imágenes
- `report_generator.py`: Generación de informes
- `cli_interface.py`: Interfaz de línea de comandos

Esta estructura modular sigue los principios de Clean Code, separando las responsabilidades en diferentes componentes.

## Formato del Informe

El informe generado es un archivo Markdown con una tabla que incluye:

- Título de la imagen
- Imagen (miniatura)
- Resolución
- Tamaño
- Diagnóstico SaaS (si se habilitó)
- Diagnóstico SDK para cada versión (si se habilitó)

## Requisitos

- Python 3.7 o superior
- Dependencias listadas en `requirements.txt`
- Para la evaluación con SDK: servicio SDK funcionando en los puertos especificados
- Para la evaluación con SaaS: conexión a Internet y API key válida

## Ejemplos

### Evaluación Básica
```bash
python liveness_cli.py -i
```

### Evaluación Avanzada
```bash
python liveness_cli.py --directory ./imagenes_test --use-saas --use-sdk --sdk-port 8080 9090 --sdk-version "6.12" "6.5" --output ./informes/informe_$(date +%Y%m%d).md --workers 10 --verbose
```

## Solución de Problemas

- **Error de conexión al SDK**: Asegúrate de que el servicio SDK esté ejecutándose en el puerto especificado.
- **Error en la API SaaS**: Verifica que la API key sea válida y tengas conexión a Internet.
- **Imágenes no encontradas**: Verifica las rutas proporcionadas para las imágenes o el directorio.
