# 🎯 Control de Ejecución de Fases

## Descripción

El pipeline ahora incluye un sistema inteligente de control de ejecución de fases que permite:

- ✅ **Re-ejecutar selectivamente** fases específicas sin procesar todo el pipeline
- ✅ **Detectar automáticamente** si una fase ya fue ejecutada
- ✅ **Omitir fases completadas** para ahorrar tiempo y recursos
- ✅ **Garantizar integridad** ejecutando automáticamente fases nunca procesadas

## 📋 Configuración

En el archivo `main.py`, encontrarás el diccionario `CONFIG_FASES`:

```python
CONFIG_FASES = {
    'fase_01': True,   # Procesamiento Básico
    'fase_02': True,   # Análisis de Sentimientos
    'fase_03': True,   # Análisis de Subjetividad
    'fase_04': True,   # Clasificación de Categorías
    'fase_05': True,   # Análisis Jerárquico de Tópicos
    'fase_06': True,   # Resumen Inteligente
    'fase_07': True,   # Generación de Visualizaciones
}
```

## 🔧 Comportamiento

### Valor `True`
La fase se **ejecuta siempre**, incluso si ya fue procesada anteriormente.

**Uso:** Cuando necesitas regenerar los resultados de una fase específica.

```python
CONFIG_FASES = {
    'fase_01': False,
    'fase_02': False,
    'fase_03': False,
    'fase_04': False,
    'fase_05': False,
    'fase_06': True,   # ← Re-generar resúmenes
    'fase_07': False,
}
```

### Valor `False`
La fase se **omite SI ya fue ejecutada previamente**.

**Uso:** Para ahorrar tiempo cuando ya tienes los resultados de una fase.

```python
CONFIG_FASES = {
    'fase_01': False,  # Ya procesado, omitir
    'fase_02': False,  # Ya procesado, omitir
    'fase_03': False,  # Ya procesado, omitir
    'fase_04': False,  # Ya procesado, omitir
    'fase_05': False,  # Ya procesado, omitir
    'fase_06': False,  # Ya procesado, omitir
    'fase_07': True,   # ← Solo generar visualizaciones
}
```

### 🧠 Detección Inteligente

**Importante:** Si una fase **NO ha sido ejecutada nunca**, se ejecutará automáticamente **sin importar** el valor de configuración.

Esto garantiza que:
- No se omitan fases críticas por error
- El pipeline siempre funcione correctamente
- Los datos estén completos para fases posteriores

## 📊 Detección de Ejecución por Fase

Cada fase detecta automáticamente si ya fue ejecutada verificando:

| Fase | Método de Detección |
|------|---------------------|
| **Fase 01** | Existe columna `TituloReview` en dataset |
| **Fase 02** | Existe columna `Sentimiento` en dataset |
| **Fase 03** | Existe columna `Subjetividad` en dataset |
| **Fase 04** | Existe columna `Categorias` en dataset |
| **Fase 05** | Existe columna `Topico` en dataset |
| **Fase 06** | Existe archivo `data/shared/resumenes.json` |
| **Fase 07** | Existe directorio `data/visualizaciones/` con archivos PNG |

## 💡 Ejemplos de Uso

### Ejemplo 1: Primera Ejecución Completa

```python
# main.py
CONFIG_FASES = {
    'fase_01': True,
    'fase_02': True,
    'fase_03': True,
    'fase_04': True,
    'fase_05': True,
    'fase_06': True,
    'fase_07': True,
}
```

**Resultado:** Todas las fases se ejecutan desde cero.

---

### Ejemplo 2: Solo Re-generar Visualizaciones

```python
# main.py
CONFIG_FASES = {
    'fase_01': False,
    'fase_02': False,
    'fase_03': False,
    'fase_04': False,
    'fase_05': False,
    'fase_06': False,
    'fase_07': True,   # ← Solo esta se ejecuta
}
```

**Resultado:** 
- Fases 01-06: Se omiten (ya ejecutadas)
- Fase 07: Se ejecuta (regenera visualizaciones)

---

### Ejemplo 3: Re-procesar desde Análisis de Tópicos

```python
# main.py
CONFIG_FASES = {
    'fase_01': False,
    'fase_02': False,
    'fase_03': False,
    'fase_04': False,
    'fase_05': True,   # ← Re-ejecutar desde aquí
    'fase_06': True,
    'fase_07': True,
}
```

**Resultado:**
- Fases 01-04: Se omiten (ya ejecutadas)
- Fases 05-07: Se ejecutan (re-procesan desde tópicos)

---

### Ejemplo 4: Optimización para Desarrollo

Durante desarrollo de Fase 07, omite todas las anteriores:

```python
# main.py
CONFIG_FASES = {
    'fase_01': False,  # Omitir
    'fase_02': False,  # Omitir
    'fase_03': False,  # Omitir
    'fase_04': False,  # Omitir
    'fase_05': False,  # Omitir
    'fase_06': False,  # Omitir
    'fase_07': True,   # ← En desarrollo
}
```

**Resultado:** Ciclo de desarrollo rápido, solo regenera visualizaciones.

---

## 🚀 Ventajas

### ⚡ Ahorro de Tiempo
- No re-procesa fases ya completadas
- Ideal para iteraciones rápidas en desarrollo
- Reduce tiempo de ejecución de horas a minutos

### 💾 Ahorro de Recursos
- Evita carga innecesaria de modelos ML
- Reduce consumo de CPU/GPU
- Minimiza llamadas a LLM (ahorra costos en modo API)

### 🔒 Seguridad
- Detecta automáticamente fases faltantes
- Garantiza ejecución de fases no procesadas
- Previene errores por datos incompletos

### 🧪 Desarrollo Iterativo
- Facilita pruebas de fases individuales
- Permite experimentación sin re-procesar todo
- Acelera ciclo de desarrollo

## 🎓 Mejores Prácticas

1. **Primera Ejecución:** Usa `True` en todas las fases
2. **Desarrollo:** Usa `False` en fases estables, `True` en la que desarrollas
3. **Re-procesamiento:** Usa `True` desde la fase que quieres re-ejecutar
4. **Producción:** Usa `True` en todas para garantizar datos frescos

## 🔄 Cambio de Nombre: Fase 08 → Fase 07

**Cambio realizado:** La fase de visualizaciones fue renombrada de "Fase 08" a "Fase 07" ya que es la séptima fase del pipeline.

### Archivos Actualizados

- ✅ `core/fase_07_visualizaciones.py` (renombrado)
- ✅ `core/__init__.py` (import actualizado)
- ✅ `main.py` (referencias actualizadas)
- ✅ `scripts/test_fase_07.py` (renombrado)
- ✅ Mensajes del sistema actualizados

### Retrocompatibilidad

Si tienes scripts personalizados que importan `fase_08_visualizaciones`, debes actualizarlos:

```python
# ❌ Antiguo (ya no funciona)
from core.fase_08_visualizaciones import GeneradorVisualizaciones

# ✅ Nuevo (correcto)
from core.fase_07_visualizaciones import GeneradorVisualizaciones

# ✅ O mejor aún (recomendado)
from core import GeneradorVisualizaciones
```

---

**Última actualización:** Noviembre 2025  
**Versión del Pipeline:** 2.0
