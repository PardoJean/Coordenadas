# 🚀 Desplegar en Streamlit Cloud

Tu aplicación ahora tiene una versión web lista para usar en el navegador. Aquí te muestro cómo desplegarla en **Streamlit Cloud** (gratis y sin configuración).

## Opción 1: Despliegue Automático (Recomendado) ⭐

### Paso 1: Crear cuenta en Streamlit Cloud
1. Ve a https://streamlit.io/cloud
2. Haz clic en **"Sign up"** y usa tu cuenta de GitHub
3. Autoriza a Streamlit Cloud para acceder a tus repositorios

### Paso 2: Desplegar tu aplicación
1. En Streamlit Cloud, haz clic en **"New app"**
2. Completa los campos:
   - **Repository:** `PardoJean/Coordendas`
   - **Branch:** `main`
   - **Main file path:** `streamlit_app.py`
3. Haz clic en **"Deploy"**

¡Eso es todo! Streamlit generará un link público automáticamente.

### Tu link será algo como:
```
https://coordendas.streamlit.app
```

## Opción 2: Ejecutar Localmente

Si quieres probar la app web en tu máquina antes de desplegar:

```bash
# Instala dependencias (una sola vez)
pip install -r requirements-streamlit.txt

# Ejecuta la app web
streamlit run streamlit_app.py
```

Se abrirá automáticamente en `http://localhost:8501`

## Características de la Versión Web

✅ **Sin descargas:** Tus compañeros solo abren el link  
✅ **OCR en tiempo real:** Procesa imágenes al instante  
✅ **Tabla editable:** Pueden corregir datos directamente  
✅ **Exportación:** Descargan Excel o CSV al terminar  
✅ **Responsive:** Funciona en móvil, tablet y escritorio  

## Cómo Compartir el Link

1. Una vez desplegado, copia el link público
2. Comparte con tus compañeros:

```
Hola compañeros, aquí está la app:
https://coordendas.streamlit.app

Pueden:
1. Subir imágenes de topografía
2. Editar los datos extraídos
3. Descargar Excel/CSV listo para usar
```

## Requisito: Tesseract OCR en el Servidor

⚠️ **Importante:** Para que el OCR funcione en Streamlit Cloud, necesitas usar **pytesseract con Google Vision API** o una **alternativa sin Tesseract**.

Si Tesseract no está disponible en Streamlit Cloud, deberás:

### Opción A: Usar PaddleOCR (Sin Tesseract)
Reemplaza en `streamlit_app.py`:
```python
# En lugar de pytesseract, usa:
# pip install paddleocr

from paddleocr import PaddleOCR
ocr = PaddleOCR(use_angle_cls=True, lang='es')
resultado = ocr.ocr(imagen, cls=True)
```

### Opción B: Desplegar en Render o Railway (Soportan Tesseract)

- **Render:** https://render.com (tiene Tesseract pre-instalado)
- **Railway:** https://railway.app (soporta dependencias del sistema)

## Solución Rápida: Dockerfile para Render

Si quieres usar Tesseract, crea un archivo `Dockerfile`:

```dockerfile
FROM python:3.11-slim

RUN apt-get update && apt-get install -y \
    tesseract-ocr \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements-streamlit.txt .
RUN pip install -r requirements-streamlit.txt

COPY . .

CMD ["streamlit", "run", "streamlit_app.py"]
```

Luego desplega en Render o Railway.

## Troubleshooting

### Error: "Tesseract no encontrado"
→ Usa PaddleOCR en lugar de Tesseract (ver Opción A arriba)

### Error: "No permission to upload file"
→ Comprueba que el archivo `streamlit_app.py` esté en la raíz del repositorio

### La app es lenta la primera vez
→ Streamlit Cloud puede ser lento al iniciar. Espera 30 segundos.

---

**¿Necesitas ayuda?** Contacta al equipo de soporte de Streamlit en https://discuss.streamlit.io
