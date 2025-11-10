# 📦 Instalación de Dependencias

Este directorio contiene todo lo necesario para ejecutar el **Pipeline de Producción** de forma independiente.

## 🚀 Instalación Rápida (Recomendado)

### Opción Automática

```bash
../scripts/install_dependencies.sh
```

Este script:
- ✅ Verifica Python y pip
- ✅ Actualiza pip a la última versión
- ✅ Instala todas las dependencias desde `requirements.txt`
- ✅ Descarga datos necesarios de NLTK
- ✅ Muestra un resumen del estado

### Opción Manual

```bash
# 1. Actualizar pip
pip install --upgrade pip

# 2. Instalar dependencias
pip install -r requirements.txt

# 3. Descargar datos de NLTK
python -c "import nltk; nltk.download('stopwords'); nltk.download('punkt')"
```

## 📋 Dependencias Incluidas

### Core Data Science
- **pandas** - Manipulación de datos
- **numpy** - Operaciones numéricas

### Machine Learning
- **torch** - Deep Learning framework
- **transformers** - Modelos BERT y HuggingFace
- **sentence-transformers** - Embeddings de texto
- **scikit-learn** - Algoritmos ML clásicos

### Topic Modeling
- **bertopic** - Modelado de tópicos con BERT
- **umap-learn** - Reducción de dimensionalidad
- **hdbscan** - Clustering jerárquico

### NLP
- **nltk** - Toolkit de procesamiento de lenguaje natural

### LLM & LangChain
- **langchain** - Framework para LLMs
- **langchain-core** - Core de LangChain
- **langchain-openai** - Integración con OpenAI
- **langchain-ollama** - Integración con Ollama (local)

### Utilidades
- **pydantic** - Validación de datos
- **python-dotenv** - Gestión de variables de entorno
- **tqdm** - Barras de progreso

## 🎯 Instalación por Entorno

### Conda (Recomendado)

```bash
# Crear entorno
conda create -n tourism-analyzer python=3.10

# Activar entorno
conda activate tourism-analyzer

# Instalar dependencias
../scripts/install_dependencies.sh
```

### venv (Alternativa)

```bash
# Crear entorno virtual
python -m venv venv

# Activar entorno
source venv/bin/activate  # Linux/macOS
# o
venv\Scripts\activate     # Windows

# Instalar dependencias
pip install -r requirements.txt
```

### Docker (Avanzado)

```dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["python", "main.py"]
```

## 🔧 Configuraciones Especiales

### GPU (NVIDIA CUDA)

Si tienes GPU NVIDIA, instala PyTorch con soporte CUDA:

```bash
# Desinstalar PyTorch CPU
pip uninstall torch

# Instalar PyTorch GPU (CUDA 11.8)
pip install torch --index-url https://download.pytorch.org/whl/cu118

# Verificar CUDA
python -c "import torch; print(f'CUDA disponible: {torch.cuda.is_available()}')"
```

### Versión Ligera (Sin GPU)

Si no necesitas GPU o tienes espacio limitado:

```bash
pip install torch --index-url https://download.pytorch.org/whl/cpu
```

### macOS con Apple Silicon (M1/M2)

```bash
# PyTorch con soporte MPS (GPU de Apple)
pip install torch torchvision torchaudio
```

## ✅ Verificar Instalación

### Verificación Rápida

```bash
python -c "
import pandas, numpy, torch, transformers
import langchain, pydantic, dotenv
print('✅ Dependencias principales instaladas')
"
```

### Verificación Completa

```bash
python -c "
import sys
deps = ['pandas', 'numpy', 'torch', 'transformers', 'sentence_transformers',
        'sklearn', 'bertopic', 'umap', 'hdbscan', 'nltk', 
        'langchain', 'langchain_core', 'langchain_openai', 'langchain_ollama',
        'pydantic', 'dotenv', 'tqdm']

missing = []
for dep in deps:
    try:
        __import__(dep)
    except ImportError:
        missing.append(dep)

if not missing:
    print('✅ Todas las dependencias instaladas correctamente')
else:
    print(f'❌ Faltan: {missing}')
    sys.exit(1)
"
```

### Verificar Versiones

```bash
pip list | grep -E 'pandas|numpy|torch|transformers|langchain'
```

## 🐛 Solución de Problemas

### Error: "No module named 'X'"

```bash
# Reinstalar la dependencia específica
pip install --upgrade nombre-del-paquete

# O reinstalar todo
pip install --force-reinstall -r requirements.txt
```

### Error: "Could not build wheels"

```bash
# Instalar herramientas de compilación
# Ubuntu/Debian
sudo apt-get install python3-dev build-essential

# macOS
xcode-select --install

# Luego reinstalar
pip install -r requirements.txt
```

### Error de Memoria durante Instalación

```bash
# Instalar paquetes uno por uno
while read req; do pip install "$req"; done < requirements.txt

# O aumentar el límite de memoria de pip
pip install --no-cache-dir -r requirements.txt
```

### Conflictos de Versiones

```bash
# Limpiar caché de pip
pip cache purge

# Crear entorno limpio
python -m venv venv_clean
source venv_clean/bin/activate
pip install -r requirements.txt
```

## 📊 Tamaño de Instalación

Espacio en disco aproximado:

- **Dependencias Python**: ~2-3 GB
- **Modelos BERT (descargados en uso)**: ~400 MB por modelo
- **Modelos Ollama** (opcional): 2-5 GB por modelo
- **Datos NLTK**: ~50 MB

**Total aproximado**: 4-10 GB dependiendo de la configuración

## 🔄 Actualizar Dependencias

### Actualizar Todo

```bash
pip install --upgrade -r requirements.txt
```

### Actualizar Paquetes Específicos

```bash
# Actualizar LangChain
pip install --upgrade langchain langchain-core langchain-openai langchain-ollama

# Actualizar transformers
pip install --upgrade transformers sentence-transformers
```

### Verificar Actualizaciones Disponibles

```bash
pip list --outdated
```

## 📚 Documentación Relacionada

- **README.md** - Guía principal del proyecto
- **docs/LLM_SETUP.md** - Configuración de LLM
- **docs/SETUP_AUTOMATICO.md** - Guía del script automático

## 🆘 Soporte

Si tienes problemas con la instalación:

1. **Revisa los logs de error** para identificar el paquete problemático
2. **Busca el error específico** en Google o Stack Overflow
3. **Verifica la versión de Python**: Debe ser 3.10+
4. **Intenta en un entorno limpio** (nuevo venv o conda)

---

**Última actualización**: Noviembre 2025  
**Python soportado**: 3.10, 3.11, 3.12
