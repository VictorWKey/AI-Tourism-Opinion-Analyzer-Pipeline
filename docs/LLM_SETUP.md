# Configuración de LLM para Análisis de Opiniones Turísticas

## 📌 Opciones de LLM

El sistema soporta **dos modos** de funcionamiento:

### 🌐 Modo API (OpenAI)
- **Ventajas**: Mayor calidad de respuestas, sin requisitos de hardware
- **Desventajas**: Requiere API key de pago, costos por uso
- **Uso recomendado**: Producción con presupuesto disponible

### 💻 Modo Local (Ollama)
- **Ventajas**: Completamente gratuito, privacidad total, sin límites de uso
- **Desventajas**: Requiere instalación y recursos de hardware
- **Uso recomendado**: Desarrollo, pruebas, o producción sin presupuesto

---

## 🚀 Instalación Rápida

### 1. Instalar Dependencias Python

```bash
# Actualizar pip
pip install --upgrade pip

# Instalar dependencias
pip install -r requirements.txt

# O compilar desde requirements.in
pip-compile requirements.in
pip install -r requirements.txt
```

### 2. Configurar Variables de Entorno

```bash
# Copiar archivo de ejemplo
cp .env.example .env

# Editar .env con tu editor favorito
nano .env  # o vim, code, etc.
```

---

## ⚙️ Configuración por Modo

### 🌐 Configuración para Modo API (OpenAI)

#### 1. Obtener API Key de OpenAI
1. Visita: https://platform.openai.com/api-keys
2. Crea una cuenta o inicia sesión
3. Genera una nueva API key
4. Copia la clave (formato: `sk-proj-...`)

#### 2. Configurar `.env`
```env
LLM_MODE=api
OPENAI_API_KEY=sk-proj-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
OPENAI_MODEL=gpt-4o-mini
```

#### Modelos Recomendados
| Modelo | Costo | Calidad | Velocidad | Uso Recomendado |
|--------|-------|---------|-----------|-----------------|
| `gpt-4o-mini` | 💰 Bajo | ⭐⭐⭐⭐ | 🚀 Rápido | **Producción** (recomendado) |
| `gpt-3.5-turbo` | 💰 Muy bajo | ⭐⭐⭐ | 🚀🚀 Muy rápido | Desarrollo/Pruebas |
| `gpt-4o` | 💰💰💰 Alto | ⭐⭐⭐⭐⭐ | 🐌 Lento | Análisis críticos |

#### Costos Aproximados (Mayo 2024)
- **gpt-4o-mini**: ~$0.15 USD por 1M tokens de entrada
- **gpt-3.5-turbo**: ~$0.50 USD por 1M tokens de entrada

---

### 💻 Configuración para Modo Local (Ollama)

#### 1. Instalar Ollama

##### Linux
```bash
curl -fsSL https://ollama.ai/install.sh | sh
```

##### macOS
```bash
brew install ollama
```

##### Windows
Descarga el instalador desde: https://ollama.ai/download

#### 2. Iniciar el Servidor de Ollama
```bash
ollama serve
```
> **Nota**: Deja esta terminal abierta mientras uses el sistema

#### 3. Descargar un Modelo

```bash
# Opción 1: Modelo ligero y rápido (RECOMENDADO para empezar)
ollama pull llama3.2:3b

# Opción 2: Modelo muy ligero (para equipos con poca RAM)
ollama pull llama3.2:1b

# Opción 3: Modelo de mayor calidad (requiere más RAM)
ollama pull llama3.1:8b

# Opción 4: Alternativa ligera (Gemma)
ollama pull gemma2:2b
```

#### 4. Configurar `.env`
```env
LLM_MODE=local
OLLAMA_BASE_URL=http://localhost:11434
OLLAMA_MODEL=llama3.2:3b
```

#### Modelos Recomendados
| Modelo | RAM Req. | Velocidad | Calidad | Uso Recomendado |
|--------|----------|-----------|---------|-----------------|
| `llama3.2:1b` | 1 GB | 🚀🚀🚀 | ⭐⭐⭐ | Equipos limitados |
| `llama3.2:3b` | 2 GB | 🚀🚀 | ⭐⭐⭐⭐ | **Balanceado** (recomendado) |
| `llama3.1:8b` | 4.7 GB | 🚀 | ⭐⭐⭐⭐⭐ | Alta calidad |
| `gemma2:2b` | 1.6 GB | 🚀🚀 | ⭐⭐⭐⭐ | Alternativa ligera |

#### Requisitos de Hardware
- **Mínimo**: 4 GB RAM, CPU moderna
- **Recomendado**: 8 GB RAM, GPU NVIDIA (opcional, mejora velocidad)
- **Óptimo**: 16 GB RAM, GPU NVIDIA con CUDA

---

## 🧪 Verificar Instalación

### Verificar Ollama
```bash
# Listar modelos instalados
ollama list

# Probar un modelo
ollama run llama3.2:3b
>>> Hola, ¿cómo estás?
>>> /bye
```

### Verificar Python
```bash
# Dentro del directorio production/
python -c "from llm_provider import LLMProvider; print(LLMProvider.get_info())"
```

Salida esperada:
```json
{
  "modo": "local",
  "temperatura": 0.0,
  "max_tokens": 2000,
  "modelo": "llama3.2:3b",
  "base_url": "http://localhost:11434"
}
```

---

## 🔄 Cambiar entre Modos

### En Tiempo de Ejecución
No soportado actualmente. Debes reiniciar el programa.

### Cambiar Configuración
Edita el archivo `.env` y modifica `LLM_MODE`:

```env
# Para usar API de OpenAI
LLM_MODE=api

# Para usar Ollama local
LLM_MODE=local
```

---

## 🐛 Solución de Problemas

### Problema: "Error al inicializar Ollama"
**Solución**:
1. Verifica que Ollama esté ejecutándose:
   ```bash
   ollama serve
   ```
2. Verifica que el modelo esté descargado:
   ```bash
   ollama list
   ollama pull llama3.2:3b
   ```

### Problema: "OPENAI_API_KEY no está configurado"
**Solución**:
1. Verifica que el archivo `.env` existe en `/production/`
2. Verifica que contiene `OPENAI_API_KEY=sk-proj-...`
3. Reinicia el programa

### Problema: "No se puede conectar con Ollama"
**Solución**:
1. Verifica que el puerto 11434 esté libre:
   ```bash
   lsof -i :11434  # Linux/Mac
   netstat -ano | findstr :11434  # Windows
   ```
2. Verifica la URL en `.env`:
   ```env
   OLLAMA_BASE_URL=http://localhost:11434
   ```

### Problema: Respuestas de baja calidad con Ollama
**Solución**:
1. Prueba un modelo más grande:
   ```bash
   ollama pull llama3.1:8b
   ```
2. Actualiza `.env`:
   ```env
   OLLAMA_MODEL=llama3.1:8b
   ```

---

## 📊 Comparación de Rendimiento

| Aspecto | Modo API | Modo Local |
|---------|----------|------------|
| **Costo** | 💰 Por uso | ✅ Gratuito |
| **Calidad** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| **Velocidad** | 🚀🚀 | 🚀 (depende del hardware) |
| **Privacidad** | ⚠️ Datos enviados a OpenAI | ✅ 100% local |
| **Requisitos** | Internet, API key | Ollama instalado, RAM |
| **Escalabilidad** | ✅ Ilimitada | ⚠️ Limitada por hardware |

---

## 💡 Recomendaciones

### Para Desarrollo/Pruebas
- **Usa Ollama** con `llama3.2:3b`
- Gratis, rápido, suficiente calidad

### Para Producción con Presupuesto
- **Usa OpenAI API** con `gpt-4o-mini`
- Mejor calidad, sin requisitos de hardware

### Para Producción sin Presupuesto
- **Usa Ollama** con `llama3.1:8b`
- Requiere servidor dedicado con buena RAM

### Para Equipos Limitados
- **Usa Ollama** con `llama3.2:1b` o `gemma2:2b`
- Funciona en laptops con 4GB RAM

---

## 📝 Ejemplo de Uso

```python
from core.llm_provider import LLMProvider, crear_chain

# El sistema carga automáticamente la configuración desde .env
provider = LLMProvider()

# Ver configuración actual
print(provider.get_info())

# Crear una cadena simple
template = "Responde en español: {pregunta}"
chain = crear_chain(template)

# Invocar
respuesta = chain.invoke({"pregunta": "¿Qué es el turismo sostenible?"})
print(respuesta)
```

---

## 🆘 Soporte

Para más información sobre:
- **Ollama**: https://ollama.ai/docs
- **OpenAI API**: https://platform.openai.com/docs
- **Langchain**: https://python.langchain.com/docs

---

## 📄 Licencia

Este componente es parte del proyecto AI Tourism Opinion Analyzer.
