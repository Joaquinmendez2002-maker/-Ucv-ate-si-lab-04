# Lab 4 - API de Visión por Computadora

Proyecto de una API REST construida con **FastAPI** para analizar imágenes usando **OpenCV**.

## 📁 Estructura del proyecto

- `src/lab4_api_cv/api/main.py` - Servidor FastAPI con un endpoint para subir y analizar imágenes.
- `src/lab4_api_cv/services/image_service.py` - Lógica de análisis de imagen con OpenCV.
- `src/lab4_api_cv/pyproject.toml` - Dependencias y configuración del proyecto.
- `tests/test_api.py` - Pruebas básicas del proyecto.
- `data/` - Carpeta usada para almacenar temporalmente las imágenes cargadas.

## 🚀 Requisitos

- Python 3.14+
- Poetry (recomendado) o pip

## ⚙️ Instalación con Poetry

1. Abrir la terminal en la carpeta raíz del proyecto.
2. Instalar dependencias:
   ```bash
   poetry install
   ```

## 🧪 Ejecución del servidor

Desde la raíz del proyecto, ejecutar:

```bash
poetry run uvicorn src.lab4_api_cv.api.main:app --reload --host 0.0.0.0 --port 8000
```

Luego abrir en el navegador:

- `http://127.0.0.1:8000/docs` para la documentación interactiva Swagger

## 📡 Uso del endpoint

Endpoint principal:

- `POST /analyze-image`

Parámetros:

- `file` - Archivo de imagen a cargar (multipart/form-data).

Ejemplo con `curl`:

```bash
curl -X POST "http://127.0.0.1:8000/analyze-image" -F "file=@ruta/a/tu/imagen.jpg"
```

Respuesta de ejemplo:

```json
{
  "mensaje": "Procesamiento exitoso",
  "resultado": {
    "alto": 480,
    "ancho": 640,
    "bordes_detectados": 1
  }
}
```

## 🧠 Qué hace el análisis

El servicio realiza lo siguiente:

- Carga la imagen en escala de grises.
- Aplica detección de bordes con el algoritmo `Canny` de OpenCV.
- Devuelve las dimensiones de la imagen y un indicador si se detectaron bordes.

## 🧪 Pruebas

Para ejecutar las pruebas con Poetry:

```bash
poetry run pytest
```

## 🔧 Notas

- La carpeta `data/` se utiliza para guardar temporalmente el archivo subido. Asegúrate de que exista y tenga permisos de escritura.
- Si usas `pip`, instala las dependencias listadas en `src/lab4_api_cv/pyproject.toml`.
