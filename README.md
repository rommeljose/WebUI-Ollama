# Mini WebUI para Ollama (HTML + JavaScript)

Una interfaz WebUI minimalista, portátil y completamente offline para interactuar con modelos de **Ollama ejecutándose en WSL** (Windows Subsystem for Linux) desde cualquier navegador en Windows.

Este proyecto no usa frameworks, backend ni dependencias externas.  
Toda la lógica está implementada en un único archivo `index.html`.

---

## 🚀 Características principales

- Selección de modelos instalados en Ollama.
- Panel informativo con:
  - Número de parámetros (`parameter_size`)
  - Tamaño en disco (GB)
  - Quantization (`Q4`, `Q5`, `Q8`, etc.) + explicación automática
  - Latencia promedio del **primer token**
- Envío de prompts con **streaming palabra por palabra**.
- Botón para **detener streaming**.
- Botón para **limpiar historial**.
- Modo respuesta corta (<10 palabras).
- Modo forzar castellano.
- Modal de ayuda integrado.
- Funciona en Windows / WSL / Linux.
- Completamente offline una vez instalados los modelos.
- Sin dependencias externas.

---

## 📦 Requisitos del sistema

## 🖥️ Requisitos del sistema (Windows)

- 🪟 **Windows 10 / 11**  
- 🐧 **WSL** (Ubuntu recomendado)  
- 🐍 **Python 3**  
- 🌐 **Navegador web compatible:**  
  - 🦊 **Firefox** → Permite abrir `index.html` directamente *(sin servidor)*  
  - 🌐 **Chrome / Edge** → Requieren servidor local *(por políticas de seguridad)*  

---

## ❓ ¿Por qué Chrome y Edge necesitan un servidor Python?

Chrome y Edge **bloquean por razones de seguridad** cualquier intento de usar `fetch()` desde un archivo abierto localmente:

```
file://C:/ruta/index.html
```

cuando intenta comunicarse con:

```
http://localhost:11434     ← donde corre Ollama
```

Este bloqueo forma parte de las reglas del navegador conocidas como:

### 🔒 CORS + Same-Origin Policy

Estas políticas impiden que un archivo HTML local trate de hacer solicitudes HTTP a un origen distinto del suyo.  
Por eso obtienes el error:

```
TypeError: Failed to fetch
```

**No es un fallo de tu WebUI.**  
Es una protección del navegador.

---

## ✅ Solución: usar un servidor Python local

Chrome y Edge permiten solicitudes HTTP **solo si la página fue servida por un servidor real**, aunque sea local.

La forma más simple es:

```bash
python3 -m http.server 8000
```

Esto expone tus archivos en:

```
http://localhost:8000
```

Ahora sí tu WebUI puede comunicarse con:

```
http://localhost:11434   ← API de Ollama
```

Y todo funciona perfectamente.

---

## 📝 Resumen rápido

| Navegador | ¿Puede abrir index.html sin servidor? | Motivo |
|----------|----------------------------------------|--------|
| 🦊 **Firefox** | ✔️ Sí | Políticas menos estrictas para `file://` |
| 🌐 **Chrome**  | ❌ No | Bloqueo CORS/Same-Origin |
| 🟦 **Edge**    | ❌ No | Bloqueo CORS/Same-Origin |

---

## 💡 Nota Final

El servidor Python **solo entrega archivos estáticos**.  
No ejecuta código, no procesa la lógica.  

Toda la inteligencia ocurre en:

- 🧠 **Ollama corriendo en WSL**
- ⚙️ **API local: `http://localhost:11434`**
- 🖥️ **Tu WebUI HTML (index.html)**


## 🐧 Instalación de WSL

```
wsl --install
```

---

## 🤖 Instalación de Ollama dentro de WSL

```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama serve
```

API en:

```
http://localhost:11434
```

---

## 📥 Descargar modelos (el que le guste, o varios de ellos)

```bash
ollama pull gemma3:4b
ollama pull llama3.2:3b
ollama pull mistral:7b
```

---

## 🌐 Ejecutar la Mini WebUI

```
python3 -m http.server 8000
```

Entrar luego en:

```
http://localhost:8000
```

---

## 🔌 API usada

- `/api/tags`
- `/api/show`
- `/api/generate` (stream)

---

## 📝 Licencia MIT

Autor: **Rommel Contreras**  
Blog: https://tecnologiacumanesa.blogspot.com/

