# 🎉 Sistema de Setup Automático Completado

## ✅ Lo que se ha creado

### 📜 Script Principal: `setup_local_llm_completo.sh`

**Ubicación**: `/production/scripts/setup_local_llm_completo.sh`

**Funcionalidad**:
- ✅ Instalación automática de Ollama (Linux/macOS)
- ✅ Inicio automático del servicio Ollama
- ✅ Descarga interactiva de modelos (3 opciones)
- ✅ Configuración automática del archivo `.env`
- ✅ Verificación completa con `test_llm_setup.py`
- ✅ Manejo de backups (preserva configuración anterior)
- ✅ Mensajes informativos con colores
- ✅ Detección de errores y ayuda de diagnóstico

### 📚 Documentación Creada

1. **docs/SETUP_AUTOMATICO.md** - Guía completa del script
   - Explicación detallada de cada paso
   - Solución de problemas comunes
   - Requisitos y recomendaciones
   - Ejemplos de uso

2. **README.md** - Actualizado
   - Nueva sección "Setup Automático TODO-EN-UNO"
   - Estructura de carpetas actualizada
   - Referencias al nuevo script

## 🚀 Cómo Usar

### Uso Básico (TODO AUTOMÁTICO)

```bash
cd production
./scripts/setup_local_llm_completo.sh
```

**Eso es todo**. El script:
1. Te pregunta qué modelo quieres (3 opciones)
2. Hace toda la instalación y configuración
3. Prueba que todo funcione
4. Te dice si está listo o si hubo errores

### Modelos Disponibles

Durante la ejecución, elige:

- **Opción 1**: `llama3.2:3b` (Recomendado)
  - 4GB RAM
  - Rápido
  - Buena calidad
  - **Mejor para desarrollo**

- **Opción 2**: `llama3.1:8b` (Alta calidad)
  - 8GB RAM
  - Más lento
  - Mejor calidad
  - **Mejor para producción**

- **Opción 3**: `gemma2:2b` (Ligero)
  - 2GB RAM
  - Muy rápido
  - Calidad aceptable
  - **Mejor para equipos limitados**

## 🔧 Lo que hace el Script (Detalles Técnicos)

### Paso 1: Verificar/Instalar Ollama
```bash
# Detecta si ollama está instalado
command -v ollama

# Si no está, instala según el OS
# Linux: curl -fsSL https://ollama.com/install.sh | sh
# macOS: brew install ollama
```

### Paso 2: Iniciar Servicio
```bash
# Verifica si está corriendo
pgrep -x "ollama"

# Si no, lo inicia
nohup ollama serve > ollama.log 2>&1 &
```

### Paso 3: Descargar Modelo
```bash
# Pregunta al usuario qué modelo
read -p "Selecciona el modelo [1-3]"

# Descarga el modelo elegido
ollama pull llama3.2:3b  # (o el que elijas)
```

### Paso 4: Configurar .env
```bash
# Hace backup del .env actual
cp .env .env.backup.YYYYMMDD_HHMMSS

# Crea nuevo .env con configuración local
cat > .env << EOF
USE_API=false
OLLAMA_MODEL=llama3.2:3b
OLLAMA_BASE_URL=http://localhost:11434
...
EOF
```

### Paso 5: Verificar
```bash
# Ejecuta el test de configuración
python scripts/test_llm_setup.py

# Verifica que todos los tests pasen
```

## 📁 Archivos del Sistema

### Creados por el Script

```
production/
├── .env                      # Configuración (creado/actualizado)
├── .env.backup.20251108_123456  # Backup automático
├── ollama.log                # Log del servicio Ollama
│
└── scripts/
    ├── setup_local_llm_completo.sh  # 🆕 Script principal
    ├── setup_ollama.sh              # Script básico (ya existía)
    └── test_llm_setup.py            # Test de verificación
```

### Documentación

```
production/
└── docs/
    ├── SETUP_AUTOMATICO.md   # 🆕 Guía del script automático
    ├── LLM_SETUP.md          # Guía completa LLM (ya existía)
    └── CHANGELOG.md          # Historial de cambios
```

## ✨ Ventajas del Script Automático

### Para el Usuario

1. **Un Solo Comando**: Todo se hace con una ejecución
2. **Sin Configuración Manual**: No hay que editar archivos
3. **Verificación Automática**: Detecta errores inmediatamente
4. **Backups Automáticos**: Preserva configuración anterior
5. **Mensajes Claros**: Sabe exactamente qué está pasando
6. **Recuperación de Errores**: Sugiere soluciones si algo falla

### Para Desarrolladores

1. **Reproducible**: Mismo resultado cada vez
2. **Idempotente**: Se puede ejecutar múltiples veces
3. **Detección de Estado**: No reinstala si ya está listo
4. **Logging**: Guarda logs para debugging
5. **Portable**: Funciona en Linux y macOS
6. **Mantenible**: Código bien documentado

## 🎯 Casos de Uso

### 1. Primera Instalación
```bash
./scripts/setup_local_llm_completo.sh
# Hace TODO desde cero
```

### 2. Cambiar de Modelo
```bash
# El script detecta Ollama ya instalado
# Solo descarga el nuevo modelo y actualiza .env
./scripts/setup_local_llm_completo.sh
```

### 3. Reinstalar/Reparar
```bash
# Ejecutar nuevamente
# Verifica todo y arregla lo que esté roto
./scripts/setup_local_llm_completo.sh
```

### 4. Verificar Estado
```bash
# El script también sirve como diagnóstico
# Muestra qué está instalado y funcionando
./scripts/setup_local_llm_completo.sh
```

## 🔍 Verificación Post-Setup

Después de ejecutar el script exitosamente:

```bash
# 1. Verificar que Ollama esté corriendo
pgrep ollama
# Debe mostrar un número (PID)

# 2. Ver modelos instalados
ollama list
# Debe mostrar el modelo que elegiste

# 3. Verificar configuración
cat .env
# Debe mostrar USE_API=false y el modelo correcto

# 4. Probar LLM
python -c "from core.llm_provider import LLMProvider; print(LLMProvider.get_info())"
# Debe mostrar config del modo local

# 5. Ejecutar pipeline
python main.py
# Debe funcionar sin errores
```

## 📊 Comparación: Antes vs Ahora

### Antes (Setup Manual)

```bash
# 1. Instalar Ollama manualmente
curl -fsSL https://ollama.com/install.sh | sh

# 2. Iniciar servicio
ollama serve &

# 3. Descargar modelo
ollama pull llama3.2:3b

# 4. Copiar .env.example
cp .env.example .env

# 5. Editar .env manualmente
nano .env
# USE_API=false
# OLLAMA_MODEL=llama3.2:3b
# ...

# 6. Probar manualmente
python scripts/test_llm_setup.py

# 7. ¿Funcionó? Si no, debug manual...
```

**Tiempo**: ~10-15 minutos  
**Pasos**: 7 pasos manuales  
**Probabilidad de error**: Alta (varios puntos de fallo)

### Ahora (Setup Automático)

```bash
./scripts/setup_local_llm_completo.sh
# [Esperar 2-5 minutos]
# ¡Listo!
```

**Tiempo**: ~2-5 minutos  
**Pasos**: 1 comando  
**Probabilidad de error**: Baja (manejo automático de errores)

## 🛡️ Seguridad y Confiabilidad

### Backups Automáticos
- Antes de modificar `.env`, crea backup con timestamp
- Formato: `.env.backup.YYYYMMDD_HHMMSS`
- Fácil recuperación si algo sale mal

### Detección de Errores
- Verifica cada paso antes de continuar
- Mensajes claros si algo falla
- Sugerencias de solución automáticas

### No Destructivo
- No borra archivos existentes
- No sobrescribe sin backup
- Preserva modelos ya descargados

## 📝 Próximos Pasos Recomendados

Después de ejecutar el script:

1. **Ejecutar el Pipeline**
   ```bash
   python main.py
   ```

2. **Ver Logs si hay Problemas**
   ```bash
   cat ollama.log
   ```

3. **Explorar Otros Modelos** (opcional)
   ```bash
   ollama pull llama3.1:8b
   # Luego edita .env: OLLAMA_MODEL=llama3.1:8b
   ```

4. **Leer la Documentación Completa**
   ```bash
   cat docs/SETUP_AUTOMATICO.md
   cat docs/LLM_SETUP.md
   ```

## 🎓 Recursos Adicionales

- **Documentación de Ollama**: https://ollama.com/docs
- **Modelos Disponibles**: https://ollama.com/library
- **LangChain con Ollama**: https://python.langchain.com/docs/integrations/llms/ollama

## 📞 Soporte

Si tienes problemas:

1. **Revisa el log**: `cat production/ollama.log`
2. **Consulta la guía**: `docs/SETUP_AUTOMATICO.md`
3. **Ejecuta el test**: `python scripts/test_llm_setup.py`
4. **Verifica Ollama**: `pgrep ollama` y `ollama list`

---

**Creado**: Noviembre 8, 2025  
**Versión**: 1.0.0  
**Autor**: GitHub Copilot  
**Licencia**: Parte del proyecto AI-Tourism-Opinion-Analyzer
