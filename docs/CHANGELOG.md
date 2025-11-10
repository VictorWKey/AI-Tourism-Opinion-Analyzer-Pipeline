# Changelog - Sistema LLM Flexible

## [2.0.0] - 2025-11-08

### 🎯 Cambios Principales

#### Nuevo Sistema de LLM Abstracto
- **Soporte para múltiples proveedores de LLM**:
  - ✅ OpenAI API (modo `api`)
  - ✅ Ollama Local (modo `local`)
  
- **Configuración centralizada** mediante variables de entorno:
  - Archivo `.env` para configuración
  - Cambio de modo sin modificar código
  
- **Módulo `llm_provider.py`** para abstracción de LLM:
  - Interfaz unificada para ambos modos
  - Patrón Singleton para reutilización de conexiones
  - Funciones de conveniencia para crear chains

#### Archivos Nuevos

##### Configuración
- `config.py`: Configuración centralizada del sistema
- `.env.example`: Plantilla de configuración con documentación
- `.gitignore`: Exclusión de archivos sensibles

##### Documentación
- `LLM_SETUP.md`: Guía completa de instalación y configuración
- `README.md`: Documentación del pipeline de producción
- `CHANGELOG.md`: Este archivo

##### Scripts
- `setup_ollama.sh`: Instalación automática de Ollama (Linux/macOS)
- `test_llm_setup.py`: Script de prueba de configuración

#### Archivos Modificados

##### Fase 05 - Análisis Jerárquico de Tópicos (`fase_05_analisis_jerarquico_topicos.py`)
- ✅ Migrado de `langchain_openai.ChatOpenAI` a `llm_provider.crear_chain()`
- ✅ Eliminadas dependencias directas de OpenAI
- ✅ Soporta ambos modos de LLM (API/Local)

##### Fase 06 - Resumen Inteligente (`fase_06_resumen_inteligente.py`)
- ✅ Migrado de `langchain_openai.ChatOpenAI` a `llm_provider.get_llm()`
- ✅ Refactorización de métodos de generación de resúmenes
- ✅ Soporta ambos modos de LLM (API/Local)

##### Pipeline Principal (`main.py`)
- ✅ Agregada visualización de configuración LLM al inicio
- ✅ Validación de configuración antes de ejecutar
- ✅ Mensajes de error informativos

##### Dependencias (`requirements.in`)
- ✅ Agregado `langchain-ollama` para soporte local
- ✅ Agregados `nltk` y `spacy` (antes faltaban)
- ✅ Corregido formato de `fastopic` a URL de GitHub

---

## Compatibilidad con Versiones Anteriores

### ⚠️ BREAKING CHANGES

#### Variables de Entorno Requeridas
**Antes**: Solo se necesitaba `OPENAI_API_KEY`

**Ahora**: Se requiere archivo `.env` con al menos:
```env
LLM_MODE=api  # o 'local'
```

#### Dependencias Adicionales
**Antes**: Solo `langchain-openai`

**Ahora**: 
- `langchain-openai` (para modo API)
- `langchain-ollama` (para modo local)

### 🔄 Migración desde v1.x

1. **Crear archivo `.env`**:
   ```bash
   cp .env.example .env
   ```

2. **Configurar modo API** (comportamiento anterior):
   ```env
   LLM_MODE=api
   OPENAI_API_KEY=tu-api-key
   OPENAI_MODEL=gpt-4o-mini
   ```

3. **Instalar nuevas dependencias**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Ejecutar prueba**:
   ```bash
   python test_llm_setup.py
   ```

---

## Beneficios del Nuevo Sistema

### 🆓 Modo Local (Ollama)
- ✅ **Costo cero**: Sin cargos por uso
- ✅ **Privacidad total**: Datos 100% locales
- ✅ **Sin límites**: Procesamiento ilimitado
- ⚠️ Requiere hardware (2-8 GB RAM según modelo)

### 🌐 Modo API (OpenAI)
- ✅ **Sin requisitos de hardware**: Funciona en cualquier equipo
- ✅ **Alta calidad**: Mejores modelos disponibles
- ✅ **Escalabilidad**: Procesamiento en la nube
- ⚠️ Costo por uso (~$0.15 por 1M tokens con gpt-4o-mini)

### 🔧 Flexibilidad
- ✅ Cambio de modo sin modificar código
- ✅ Configuración por variables de entorno
- ✅ Fácil integración de nuevos proveedores
- ✅ Abstracción unificada para ambos modos

---

## Ejemplos de Uso

### Ejemplo 1: Usar con Ollama Local
```bash
# 1. Configurar
echo "LLM_MODE=local" > .env
echo "OLLAMA_MODEL=llama3.2:3b" >> .env

# 2. Instalar Ollama
./setup_ollama.sh

# 3. Ejecutar
python main.py
```

### Ejemplo 2: Usar con OpenAI API
```bash
# 1. Configurar
echo "LLM_MODE=api" > .env
echo "OPENAI_API_KEY=sk-proj-..." >> .env

# 2. Ejecutar
python main.py
```

### Ejemplo 3: Uso Programático
```python
from llm_provider import crear_chain, LLMProvider

# Ver configuración
print(LLMProvider.get_info())

# Crear chain
chain = crear_chain("Analiza: {texto}")

# Invocar
resultado = chain.invoke({"texto": "Excelente hotel"})
```

---

## Próximas Mejoras (Roadmap)

### v2.1.0 (Planificado)
- [ ] Soporte para más proveedores (Anthropic Claude, Google Gemini)
- [ ] Cache de respuestas LLM para optimización
- [ ] Modo híbrido (combinar local + API)
- [ ] Panel de configuración interactivo

### v2.2.0 (Planificado)
- [ ] Métricas de costo y uso por sesión
- [ ] Comparación automática de calidad entre modelos
- [ ] Fine-tuning de modelos locales con datos propios
- [ ] Soporte para modelos cuantizados (GGUF)

---

## Recursos

### Documentación
- [LLM_SETUP.md](./LLM_SETUP.md): Guía completa de configuración
- [README.md](./README.md): Documentación del pipeline

### Enlaces Externos
- [Ollama](https://ollama.ai): Instalación y modelos
- [OpenAI Platform](https://platform.openai.com): API keys y documentación
- [Langchain](https://python.langchain.com): Framework LLM

---

## Contribuciones

Este sistema fue diseñado para ser extensible. Para agregar un nuevo proveedor:

1. Implementar método en `LLMProvider` (ej: `_inicializar_anthropic()`)
2. Agregar configuración en `ConfigLLM`
3. Actualizar documentación
4. Crear tests

---

## Créditos

**Desarrollado por**: VictorWKey  
**Fecha**: 8 de Noviembre, 2025  
**Proyecto**: AI Tourism Opinion Analyzer  
