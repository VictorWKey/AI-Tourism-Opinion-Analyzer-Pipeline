# 🚀 Guía Rápida: Setup Automático de LLM Local

## ¿Qué hace este script?

`setup_local_llm_completo.sh` es un script **TODO-EN-UNO** que configura completamente tu LLM local en minutos.

## ✨ Características

- ✅ **Instalación Automática**: Detecta tu sistema e instala Ollama
- ✅ **Descarga de Modelos**: Te permite elegir el modelo que mejor se adapte a tu hardware
- ✅ **Configuración Automática**: Crea y configura el archivo `.env` por ti
- ✅ **Verificación Completa**: Prueba que todo funcione antes de terminar
- ✅ **Sin Intervención**: Solo ejecutas una vez y el script hace todo

## 🎯 Uso

### Ejecución Básica

```bash
cd production
./scripts/setup_local_llm_completo.sh
```

### Opciones de Modelos

Durante la ejecución, el script te preguntará qué modelo quieres:

1. **llama3.2:3b** - Recomendado (4GB RAM, rápido, buena calidad)
2. **llama3.1:8b** - Mejor calidad (8GB RAM, más lento)
3. **gemma2:2b** - Más ligero (2GB RAM, muy rápido, menor calidad)

**Solo presiona el número y Enter**. Si no eliges nada, usa llama3.2:3b automáticamente.

## 📋 Proceso Completo

El script ejecuta estos 5 pasos:

### Paso 1: Verificar/Instalar Ollama
- Detecta si ya tienes Ollama instalado
- Si no, lo instala automáticamente (Linux/macOS)

### Paso 2: Iniciar Servicio Ollama
- Verifica si Ollama está corriendo
- Si no, lo inicia en segundo plano
- Crea archivo de log en `production/ollama.log`

### Paso 3: Descargar Modelo LLM
- Te muestra las opciones disponibles
- Descarga el modelo que elijas
- Verifica que se instaló correctamente

### Paso 4: Configurar .env
- Hace backup de tu `.env` actual (si existe)
- Crea nuevo `.env` configurado para modo local
- Establece todas las variables necesarias

### Paso 5: Probar Configuración
- Ejecuta `scripts/test_llm_setup.py`
- Verifica que todo funcione correctamente
- Te muestra un resumen final

## 📊 Salida Esperada

```
============================================================
  CONFIGURACIÓN COMPLETA DE LLM LOCAL (OLLAMA)
============================================================

[PASO 1/5] Verificando instalación de Ollama...
✓ Ollama ya está instalado

[PASO 2/5] Iniciando servicio Ollama...
✓ Ollama ya está corriendo

[PASO 3/5] Descargando modelo de LLM...
Modelos disponibles:
  1. llama3.2:3b  - Recomendado para desarrollo (4GB RAM, rápido)
  2. llama3.1:8b  - Mejor calidad (8GB RAM, más lento)
  3. gemma2:2b    - Más ligero (2GB RAM, muy rápido)

Selecciona el modelo [1-3]: 1
✓ Modelo llama3.2:3b descargado correctamente

[PASO 4/5] Configurando archivo .env...
✓ Archivo .env configurado para modo local

[PASO 5/5] Probando configuración...
✅ CONFIGURACIÓN COMPLETA EXITOSA
```

## ⚠️ Requisitos Previos

### Mínimos
- **Sistema**: Linux o macOS
- **RAM**: 4GB mínimo (8GB recomendado)
- **Disco**: 3-6GB libres para Ollama + modelo
- **Python**: 3.10+ instalado
- **Dependencias Python**: `pip install -r requirements.txt`

### Verificar antes de ejecutar

```bash
# Verificar Python
python --version  # Debe ser 3.10+

# Verificar pip
pip --version

# Verificar espacio en disco
df -h ~
```

## 🐛 Solución de Problemas

### Error: "Sistema operativo no soportado"

**Windows no está soportado** por el script automático. Opciones:

1. Usar WSL2 (Windows Subsystem for Linux)
2. Instalar Ollama manualmente desde https://ollama.com/download
3. Usar modo API en lugar de local

### Error: "Error al iniciar Ollama"

```bash
# Ver el log de errores
cat production/ollama.log

# Intentar iniciar manualmente
ollama serve
```

### Error: "Error al descargar el modelo"

```bash
# Verificar conexión a internet
ping -c 3 ollama.com

# Intentar descargar manualmente
ollama pull llama3.2:3b

# Listar modelos descargados
ollama list
```

### Error: "Módulos Python no encontrados"

```bash
# Instalar dependencias
pip install -r requirements.txt

# Verificar instalación
pip list | grep langchain
```

### El test final falla

```bash
# Verificar que Ollama esté corriendo
pgrep ollama

# Probar conexión manual
curl http://localhost:11434/api/tags

# Ver configuración actual
cat .env

# Ejecutar test manualmente
python scripts/test_llm_setup.py
```

## 🔄 Cambiar de Modelo Después

Si quieres cambiar el modelo más tarde:

```bash
# 1. Descargar nuevo modelo
ollama pull llama3.1:8b

# 2. Editar .env
nano .env
# Cambiar: OLLAMA_MODEL=llama3.1:8b

# 3. Probar
python scripts/test_llm_setup.py
```

## 📝 Archivos Creados/Modificados

El script crea o modifica estos archivos:

- **`.env`**: Configuración principal (backup del anterior)
- **`.env.backup.YYYYMMDD_HHMMSS`**: Backup de tu .env anterior
- **`ollama.log`**: Log del servicio Ollama

## 🎓 Siguiente Paso

Después de ejecutar el script exitosamente:

```bash
# Ejecutar el pipeline completo
python main.py
```

## 📚 Documentación Relacionada

- [README.md](../README.md) - Documentación principal del proyecto
- [docs/LLM_SETUP.md](../docs/LLM_SETUP.md) - Guía completa de configuración LLM
- [docs/CHANGELOG.md](../docs/CHANGELOG.md) - Historial de cambios

## 💡 Consejos

### Para Desarrollo
- Usa `llama3.2:3b` - Perfecto balance entre velocidad y calidad
- Consume ~4GB RAM
- Respuestas en 2-5 segundos

### Para Producción
- Usa `llama3.1:8b` si tienes recursos
- Mejor calidad de respuestas
- Requiere servidor con 8GB+ RAM

### Para Equipos Limitados
- Usa `gemma2:2b` 
- Solo 2GB RAM necesarios
- Calidad aceptable para pruebas

## 🆘 Soporte

Si tienes problemas:

1. **Revisa la sección de Solución de Problemas** arriba
2. **Consulta el log**: `cat production/ollama.log`
3. **Ejecuta el test**: `python scripts/test_llm_setup.py`
4. **Documentación de Ollama**: https://ollama.com/docs

## 🔐 Privacidad

Al usar Ollama local:
- ✅ Tus datos **NUNCA** salen de tu computadora
- ✅ Sin envío de información a terceros
- ✅ Control total sobre tus datos
- ✅ Ideal para datos sensibles o confidenciales

---

**Última actualización**: Noviembre 2025  
**Versión del script**: 1.0.0
