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

### Windows
- Windows 10 / 11
- WSL (Ubuntu recomendado)
- Python 3
- Navegador (Chrome/Edge requiere servidor; Firefox puede abrir localmente)

---

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

## 📥 Descargar modelos

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

