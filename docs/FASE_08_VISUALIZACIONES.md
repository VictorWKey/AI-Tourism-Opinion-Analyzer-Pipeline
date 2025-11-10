# 🎨 FASE 08: GENERACIÓN DE VISUALIZACIONES

## 📋 **DESCRIPCIÓN GENERAL**

La Fase 08 es el módulo de **visualización inteligente y adaptativa** del AI Tourism Opinion Analyzer Pipeline. Su objetivo es generar visualizaciones profesionales, informativas y accionables que permitan a turismólogos y gestores de destinos turísticos identificar:

- ✅ **Percepciones** de los turistas sobre el destino
- ✅ **Fortalezas** del destino (aspectos mejor valorados)
- ✅ **Debilidades** del destino (aspectos problemáticos)
- ✅ **Tendencias temporales** en la percepción turística
- ✅ **Patrones** en sentimientos, categorías y sub-tópicos

**Características principales:**
- 🧠 **Sistema adaptativo**: Valida el volumen de datos y renderiza solo visualizaciones significativas
- 📊 **40 visualizaciones potenciales**: Desde análisis ejecutivos hasta detalles granulares
- 💾 **Exportación a PNG**: Todas las visualizaciones se guardan en `data/visualizaciones/`
- 🎨 **Diseño profesional**: Gráficos con paletas de colores elegantes y tipografía clara
- ⚡ **Optimizado**: No genera visualizaciones vacías o poco representativas

---

## 📁 **ESTRUCTURA DE ARCHIVOS**

```
production/
├── core/
│   └── fase_08_visualizaciones.py          # Módulo principal (NUEVO)
│
├── data/
│   └── visualizaciones/                     # Carpeta de salida (NUEVA)
│       ├── 01_dashboard/
│       │   ├── dashboard_ejecutivo.png
│       │   ├── kpis_principales.png
│       │   └── resumen_validacion.png
│       │
│       ├── 02_sentimientos/
│       │   ├── distribucion_sentimientos.png
│       │   ├── evolucion_temporal_sentimientos.png
│       │   ├── sentimientos_por_calificacion.png
│       │   ├── wordcloud_positivo.png
│       │   ├── wordcloud_neutro.png
│       │   ├── wordcloud_negativo.png
│       │   ├── top_palabras_comparacion.png
│       │   └── sentimiento_vs_subjetividad.png
│       │
│       ├── 03_categorias/
│       │   ├── top_categorias.png
│       │   ├── sentimientos_por_categoria.png
│       │   ├── fortalezas_vs_debilidades.png
│       │   ├── radar_chart_360.png
│       │   ├── matriz_coocurrencia.png
│       │   ├── calificacion_por_categoria.png
│       │   ├── evolucion_categorias.png
│       │   └── wordclouds_por_categoria.png
│       │
│       ├── 04_topicos/
│       │   ├── sunburst_jerarquico.png
│       │   ├── treemap_subtopicos.png
│       │   ├── top_subtopicos_mencionados.png
│       │   ├── top_subtopicos_problematicos.png
│       │   ├── distribucion_subtopicos.png
│       │   └── wordcloud_subtopicos.png
│       │
│       ├── 05_temporal/
│       │   ├── volumen_opiniones_tiempo.png
│       │   ├── evolucion_sentimientos.png
│       │   ├── calendar_heatmap.png
│       │   ├── tendencia_calificacion.png
│       │   └── estacionalidad_categorias.png
│       │
│       ├── 06_texto/
│       │   ├── wordcloud_general.png
│       │   ├── distribucion_longitud.png
│       │   ├── top_bigramas.png
│       │   └── top_trigramas.png
│       │
│       └── 07_combinados/
│           ├── sentimiento_subjetividad_categoria.png
│           ├── calificacion_categoria_sentimiento.png
│           ├── volumen_vs_sentimiento_scatter.png
│           ├── correlacion_calificacion_sentimiento.png
│           └── distribucion_categorias_calificacion.png
│
└── main.py                                   # Incluirá llamada a Fase 08
```

---

## 🎯 **CATÁLOGO COMPLETO DE VISUALIZACIONES**

### **SECCIÓN 1: DASHBOARD Y RESUMEN (3 visualizaciones)**

#### **1.1. Resumen de Validación del Dataset**
- **Tipo**: Panel informativo
- **Contenido**:
  - Total de opiniones analizadas
  - Rango de fechas (si aplica)
  - Categorías identificadas
  - Cobertura de tópicos
  - Visualizaciones generadas vs omitidas
  - Recomendaciones para mejorar el análisis
- **Validación**: Siempre se genera
- **Archivo**: `01_dashboard/resumen_validacion.png`

#### **1.2. Dashboard Ejecutivo**
- **Tipo**: Panel de 4 cuadrantes
- **Cuadrantes**:
  1. Distribución de sentimientos (donut chart)
  2. Top 5 categorías más mencionadas (horizontal bars)
  3. Top 5 fortalezas del destino (lista verde con ✓)
  4. Top 5 debilidades del destino (lista roja con ✗)
- **Validación**: Siempre (adaptativo según volumen)
- **Archivo**: `01_dashboard/dashboard_ejecutivo.png`

#### **1.3. KPIs Principales**
- **Tipo**: Cards con métricas clave
- **Métricas**:
  - Total opiniones analizadas
  - % Sentimiento positivo global
  - Calificación promedio
  - Categoría mejor valorada
  - Categoría más problemática
  - Sub-tópico más mencionado
- **Validación**: Siempre se genera
- **Archivo**: `01_dashboard/kpis_principales.png`

---

### **SECCIÓN 2: ANÁLISIS DE SENTIMIENTOS (8 visualizaciones)**

#### **2.1. Distribución General de Sentimientos**
- **Tipo**: Donut chart
- **Colores**: 🟢 Verde (Positivo), ⚫ Gris (Neutro), 🔴 Rojo (Negativo)
- **Contenido**: Porcentajes + valores absolutos
- **Validación**: Siempre (mínimo 5 opiniones)
- **Archivo**: `02_sentimientos/distribucion_sentimientos.png`

#### **2.2. Evolución Temporal de Sentimientos**
- **Tipo**: Gráfico de área apilada / líneas múltiples
- **Ejes**: 
  - X: Tiempo (meses/trimestres)
  - Y: Cantidad de opiniones
- **Series**: 3 líneas/áreas (Positivo, Neutro, Negativo)
- **Validación**: 
  - ✅ Requiere fechas válidas
  - ✅ Mínimo 30 opiniones
  - ✅ Rango temporal > 60 días
- **Archivo**: `02_sentimientos/evolucion_temporal_sentimientos.png`

#### **2.3. Sentimientos por Calificación**
- **Tipo**: Heatmap o Stacked Bar Chart
- **Ejes**:
  - X: Calificación (1-5 estrellas)
  - Y: Sentimiento
- **Color**: Intensidad de frecuencia
- **Validación**: Mínimo 30 opiniones
- **Archivo**: `02_sentimientos/sentimientos_por_calificacion.png`

#### **2.4. Distribución de Calificaciones por Sentimiento**
- **Tipo**: Violin Plot o Box Plot
- **Grupos**: 3 violines (Positivo, Neutro, Negativo)
- **Validación**: 
  - ✅ Mínimo 50 opiniones para Violin Plot
  - ⚠️ Si <50: usar Box Plot
  - ❌ Si <30: omitir
- **Archivo**: `02_sentimientos/distribucion_calificaciones_sentimiento.png`

#### **2.5-2.7. Nubes de Palabras por Sentimiento**
- **Tipo**: Word Cloud (3 archivos separados)
- **Configuración**:
  - Stopwords multilingües (español, inglés, portugués, francés, italiano)
  - Max words: 100-150
  - Colormap: Greens (positivo), Greys (neutro), Reds (negativo)
- **Validación**: Mínimo 15 opiniones por sentimiento
- **Archivos**:
  - `02_sentimientos/wordcloud_positivo.png`
  - `02_sentimientos/wordcloud_neutro.png`
  - `02_sentimientos/wordcloud_negativo.png`

#### **2.8. Top Palabras: Positivas vs Negativas**
- **Tipo**: Diverging Horizontal Bar Chart
- **Layout**: 
  - Izquierda: Top 15 palabras negativas (rojo)
  - Derecha: Top 15 palabras positivas (verde)
- **Validación**: Mínimo 20 opiniones (10 por sentimiento)
- **Archivo**: `02_sentimientos/top_palabras_comparacion.png`

#### **2.9. Sentimiento vs Subjetividad**
- **Tipo**: Stacked Bar Chart
- **Grupos**: Subjetiva | Mixta
- **Breakdown**: Sentimientos por grupo
- **Validación**: Mínimo 20 opiniones
- **Archivo**: `02_sentimientos/sentimiento_vs_subjetividad.png`

---

### **SECCIÓN 3: ANÁLISIS DE CATEGORÍAS (8 visualizaciones)**

#### **3.1. Top Categorías Mencionadas**
- **Tipo**: Horizontal Bar Chart
- **Ordenamiento**: Mayor a menor frecuencia
- **Validación**: Siempre (mínimo 5 opiniones)
- **Archivo**: `03_categorias/top_categorias.png`

#### **3.2. Sentimientos por Categoría** ⭐⭐⭐
- **Tipo**: Stacked Horizontal Bar Chart (100%)
- **Categorías**: 12 barras (filtradas según menciones)
- **Segmentos**: Positivo, Neutro, Negativo
- **Insight clave**: Identifica categorías problemáticas
- **Validación**: Mínimo 10 opiniones, mostrar solo categorías con >3 menciones
- **Archivo**: `03_categorias/sentimientos_por_categoria.png`

#### **3.3. Fortalezas vs Debilidades** ⭐⭐⭐
- **Tipo**: Diverging Bar Chart
- **Layout**:
  - Izquierda: % sentimiento negativo (rojo)
  - Centro: Nombre de categoría
  - Derecha: % sentimiento positivo (verde)
- **Insight**: Balance visual inmediato
- **Validación**: Mínimo 10 opiniones, categorías con >5 menciones
- **Archivo**: `03_categorias/fortalezas_vs_debilidades.png`

#### **3.4. Radar Chart 360° del Destino** ⭐
- **Tipo**: Spider/Radar Chart
- **Ejes**: 12 ejes (1 por categoría, filtrado si necesario)
- **Líneas superpuestas**:
  - 🟢 % opiniones positivas
  - 🔴 % opiniones negativas
  - 🔵 Promedio calificación (normalizado)
- **Validación**: Mínimo 50 opiniones, al menos 4 categorías con >5 menciones
- **Archivo**: `03_categorias/radar_chart_360.png`

#### **3.5. Matriz de Co-ocurrencia de Categorías**
- **Tipo**: Heatmap 12x12
- **Color**: Frecuencia de co-aparición
- **Insight**: "Gastronomía y Alojamiento aparecen juntas en 45% de casos"
- **Validación**: 
  - ✅ Mínimo 100 opiniones
  - ✅ Al menos 3 categorías activas
  - ❌ Si <100: omitir
- **Archivo**: `03_categorias/matriz_coocurrencia.png`

#### **3.6. Calificación por Categoría**
- **Tipo**: Box Plot múltiple
- **Boxes**: Uno por categoría (filtrado)
- **Validación**: Mínimo 30 opiniones, mostrar categorías con >10 menciones
- **Archivo**: `03_categorias/calificacion_por_categoria.png`

#### **3.7. Evolución Temporal por Categoría**
- **Tipo**: Gráfico de líneas múltiples
- **Series**: Top 6 categorías más mencionadas
- **Ejes**:
  - X: Tiempo (meses)
  - Y: Cantidad de menciones
- **Validación**: Mínimo 60 opiniones con fechas
- **Archivo**: `03_categorias/evolucion_categorias.png`

#### **3.8. Nubes de Palabras por Categoría**
- **Tipo**: Grid de Word Clouds (layout adaptativo)
- **Layout**: 
  - Si 6 categorías: 3x2
  - Si 4 categorías: 2x2
  - Si 2-3 categorías: vertical
- **Validación**: Mínimo 50 opiniones total, categorías con >15 menciones
- **Archivo**: `03_categorias/wordclouds_por_categoria.png`

---

### **SECCIÓN 4: ANÁLISIS JERÁRQUICO DE TÓPICOS (6 visualizaciones)**

#### **4.1. Sunburst Chart Jerárquico** ⭐⭐⭐
- **Tipo**: Sunburst (gráfico circular jerárquico)
- **Niveles**:
  - Centro: Categorías
  - Anillos externos: Sub-tópicos
- **Tamaño**: Frecuencia de menciones
- **Color**: Sentimiento dominante del sub-tópico
- **Validación**: 
  - ✅ Mínimo 50 opiniones
  - ✅ Al menos 3 categorías con tópicos
  - ✅ Columna 'Topico' no vacía en >50%
  - ⚠️ Si <50: usar Treemap simple
- **Archivo**: `04_topicos/sunburst_jerarquico.png`

#### **4.2. Treemap de Sub-tópicos**
- **Tipo**: Treemap (rectángulos anidados)
- **Rectángulos grandes**: Categorías
- **Rectángulos pequeños**: Sub-tópicos
- **Color**: Sentimiento promedio
- **Validación**: Mínimo 30 opiniones con tópicos
- **Archivo**: `04_topicos/treemap_subtopicos.png`

#### **4.3. Top 10 Sub-tópicos Más Mencionados**
- **Tipo**: Horizontal Bar Chart
- **Información**: Sub-tópico + categoría padre
- **Color**: Por sentimiento dominante
- **Validación**: Mínimo 20 opiniones con tópicos
- **Archivo**: `04_topicos/top_subtopicos_mencionados.png`

#### **4.4. Top 10 Sub-tópicos Problemáticos** ⭐
- **Tipo**: Tabla visual con iconos 🔴
- **Columnas**:
  - Categoría padre
  - Sub-tópico
  - % Sentimiento negativo
  - N° opiniones
- **Ordenamiento**: Por % negativo descendente
- **Validación**: Mínimo 20 opiniones con tópicos y sentimiento negativo
- **Archivo**: `04_topicos/top_subtopicos_problematicos.png`

#### **4.5. Distribución de Sub-tópicos por Categoría**
- **Tipo**: Bar Chart
- **Ejes**:
  - X: Categorías
  - Y: Cantidad de sub-tópicos únicos
- **Insight**: Diversidad temática por categoría
- **Validación**: Mínimo 50 opiniones, 3+ categorías con múltiples tópicos
- **Archivo**: `04_topicos/distribucion_subtopicos.png`

#### **4.6. Nube de Sub-tópicos**
- **Tipo**: Word Cloud donde las "palabras" son nombres de sub-tópicos
- **Tamaño**: Frecuencia del sub-tópico
- **Color**: Categoría padre
- **Validación**: Mínimo 30 sub-tópicos únicos
- **Fallback**: Si <30, mostrar tabla en lugar de nube
- **Archivo**: `04_topicos/wordcloud_subtopicos.png`

---

### **SECCIÓN 5: ANÁLISIS TEMPORAL (5 visualizaciones)**

**NOTA**: Esta sección completa requiere columna 'FechaEstadia' válida

#### **5.1. Volumen de Opiniones en el Tiempo**
- **Tipo**: Bar Chart / Line Chart
- **Ejes**:
  - X: Tiempo (meses/días según rango)
  - Y: Cantidad de opiniones
- **Validación**: 
  - ✅ Fechas válidas
  - ✅ Mínimo 20 opiniones con fechas
  - ✅ Rango temporal > 30 días
  - ⚠️ Si <30 días: agrupar por día
- **Archivo**: `05_temporal/volumen_opiniones_tiempo.png`

#### **5.2. Evolución Temporal de Sentimientos**
- **Tipo**: Área apilada o líneas múltiples
- **Series**: Positivo, Neutro, Negativo
- **Validación**: Mínimo 30 opiniones, rango > 60 días
- **Archivo**: `05_temporal/evolucion_sentimientos.png`

#### **5.3. Calendar Heatmap (Mapa de Calor Temporal)**
- **Tipo**: Heatmap estilo calendario
- **Layout**:
  - Filas: Años
  - Columnas: Meses
- **Color**: Sentimiento promedio del mes
- **Validación**: 
  - ✅ Mínimo 100 opiniones
  - ✅ Rango > 90 días (preferible > 6 meses)
  - ❌ Si <100: omitir
- **Archivo**: `05_temporal/calendar_heatmap.png`

#### **5.4. Tendencia de Calificación Promedio**
- **Tipo**: Line chart con banda de confianza
- **Ejes**:
  - X: Tiempo
  - Y: Calificación promedio (1-5)
- **Línea de tendencia**: Suavizada (rolling average)
- **Validación**: Mínimo 50 opiniones, rango > 60 días
- **Archivo**: `05_temporal/tendencia_calificacion.png`

#### **5.5. Estacionalidad de Categorías**
- **Tipo**: Heatmap
- **Ejes**:
  - Filas: Categorías
  - Columnas: Meses
- **Color**: Frecuencia de mención
- **Insight**: "Naturaleza pica en verano"
- **Validación**: Mínimo 100 opiniones, rango > 6 meses
- **Archivo**: `05_temporal/estacionalidad_categorias.png`

---

### **SECCIÓN 6: ANÁLISIS DE TEXTO (4 visualizaciones)**

#### **6.1. Nube de Palabras General**
- **Tipo**: Word Cloud
- **Fuente**: Todas las opiniones
- **Filtros**: Stopwords multilingües
- **Validación**: Mínimo 20 opiniones
- **Archivo**: `06_texto/wordcloud_general.png`

#### **6.2. Distribución de Longitud de Opiniones**
- **Tipo**: Histograma con breakdown por sentimiento
- **Ejes**:
  - X: Longitud (número de palabras)
  - Y: Frecuencia
- **Histogramas**: 3 superpuestos (Positivo, Neutro, Negativo)
- **Validación**: Mínimo 30 opiniones
- **Archivo**: `06_texto/distribucion_longitud.png`

#### **6.3. Top Bigramas**
- **Tipo**: Horizontal Bar Chart
- **Contenido**: Top 15 bigramas más frecuentes
- **Ejemplo**: "servicio al cliente", "muy limpio", "buena ubicación"
- **Validación**: Mínimo 100 opiniones
- **Archivo**: `06_texto/top_bigramas.png`

#### **6.4. Top Trigramas**
- **Tipo**: Horizontal Bar Chart
- **Contenido**: Top 15 trigramas más frecuentes
- **Validación**: Mínimo 100 opiniones
- **Fallback**: Si <100, omitir
- **Archivo**: `06_texto/top_trigramas.png`

---

### **SECCIÓN 7: ANÁLISIS COMBINADOS (5 visualizaciones)**

#### **7.1. Sentimiento × Subjetividad × Categoría**
- **Tipo**: Faceted Bar Chart (pequeños múltiples)
- **Grid**: Categorías principales
- **Panel**: Breakdown Sentimiento por Subjetividad
- **Validación**: 
  - ✅ Mínimo 100 opiniones
  - ⚠️ Si <100: simplificar a 2D (Sentimiento × Categoría)
- **Archivo**: `07_combinados/sentimiento_subjetividad_categoria.png`

#### **7.2. Calificación por Categoría y Sentimiento**
- **Tipo**: Grouped Bar Chart
- **Ejes**:
  - X: Categorías
  - Y: Calificación promedio
- **Grupos**: 3 barras por categoría (Positivo, Neutro, Negativo)
- **Validación**: Mínimo 50 opiniones
- **Archivo**: `07_combinados/calificacion_categoria_sentimiento.png`

#### **7.3. Volumen vs Sentimiento por Categoría**
- **Tipo**: Scatter Plot con burbujas
- **Ejes**:
  - X: % Opiniones positivas
  - Y: % Opiniones negativas
- **Tamaño burbuja**: Volumen de opiniones
- **Etiquetas**: Categorías
- **Validación**: Mínimo 50 opiniones, 5+ categorías
- **Fallback**: Si <5 categorías, usar bar chart
- **Archivo**: `07_combinados/volumen_vs_sentimiento_scatter.png`

#### **7.4. Correlación Calificación-Sentimiento**
- **Tipo**: Scatter Plot con línea de regresión
- **Ejes**:
  - X: Calificación (1-5)
  - Y: Score sentimiento (numérico)
- **Insight**: Verificar coherencia calificación-sentimiento
- **Validación**: Mínimo 50 opiniones
- **Archivo**: `07_combinados/correlacion_calificacion_sentimiento.png`

#### **7.5. Distribución de Categorías por Calificación**
- **Tipo**: Stacked Area Chart
- **Ejes**:
  - X: Calificación (1-5)
  - Y: Proporción (0-100%)
- **Áreas**: Categorías apiladas
- **Validación**: Mínimo 100 opiniones
- **Archivo**: `07_combinados/distribucion_categorias_calificacion.png`

---

## 🔧 **ARQUITECTURA TÉCNICA**

### **Clase Principal: `GeneradorVisualizaciones`**

```python
class GeneradorVisualizaciones:
    """
    Generador adaptativo de visualizaciones para análisis turístico.
    """
    
    def __init__(self, dataset_path='data/dataset.csv', output_dir='data/visualizaciones'):
        self.dataset_path = dataset_path
        self.output_dir = Path(output_dir)
        self.df = None
        self.validador = None
        self.visualizaciones_generadas = []
        self.visualizaciones_omitidas = []
        
    def procesar(self):
        """Pipeline principal de generación."""
        # 1. Cargar datos
        self._cargar_datos()
        
        # 2. Validar dataset
        self._validar_dataset()
        
        # 3. Crear estructura de carpetas
        self._crear_carpetas()
        
        # 4. Generar visualizaciones por sección
        self._generar_dashboard()
        self._generar_analisis_sentimientos()
        self._generar_analisis_categorias()
        self._generar_analisis_topicos()
        self._generar_analisis_temporal()
        self._generar_analisis_texto()
        self._generar_analisis_combinados()
        
        # 5. Generar resumen de validación
        self._generar_resumen_validacion()
        
        # 6. Reporte final
        self._generar_reporte_final()
```

### **Sistema de Validación**

```python
class ValidadorVisualizaciones:
    """
    Valida el dataset y decide qué visualizaciones renderizar.
    """
    
    def __init__(self, df):
        self.df = df
        self.n_opiniones = len(df)
        self.tiene_fechas = self._validar_fechas()
        self.tiene_topicos = self._validar_topicos()
        self.categorias_validas = self._validar_categorias()
        self.rango_temporal = self._calcular_rango_temporal()
        self.diversidad_sentimientos = self._calcular_diversidad()
        
    def puede_renderizar(self, viz_name: str) -> bool:
        """Determina si una visualización es viable."""
        reglas = {
            'evolucion_temporal': self.tiene_fechas and self.n_opiniones >= 30,
            'sunburst_topicos': self.tiene_topicos and self.n_opiniones >= 50,
            'matriz_coocurrencia': self.n_opiniones >= 100,
            # ... más reglas
        }
        return reglas.get(viz_name, True)
```

---

## 🎨 **ESPECIFICACIONES DE DISEÑO**

### **Paleta de Colores**

```python
COLORES = {
    'positivo': '#4CAF50',      # Verde
    'neutro': '#9E9E9E',        # Gris
    'negativo': '#F44336',      # Rojo
    'primario': '#2196F3',      # Azul
    'secundario': '#FF9800',    # Naranja
    'fondo': '#FFFFFF',         # Blanco
    'texto': '#212121',         # Gris oscuro
    'grid': '#E0E0E0',          # Gris claro
}

# Paletas por categoría (12 colores únicos)
PALETA_CATEGORIAS = [
    '#1f77b4', '#ff7f0e', '#2ca02c', '#d62728',
    '#9467bd', '#8c564b', '#e377c2', '#7f7f7f',
    '#bcbd22', '#17becf', '#aec7e8', '#ffbb78'
]
```

### **Tipografía y Estilos**

```python
ESTILOS = {
    'titulo': {
        'fontsize': 16,
        'fontweight': 'bold',
        'color': COLORES['texto']
    },
    'subtitulo': {
        'fontsize': 12,
        'fontweight': 'normal',
        'color': COLORES['texto']
    },
    'etiquetas': {
        'fontsize': 10,
        'color': COLORES['texto']
    },
    'figura': {
        'facecolor': COLORES['fondo'],
        'dpi': 300  # Alta resolución para PNG
    }
}
```

### **Configuración de Exportación PNG**

```python
CONFIG_EXPORT = {
    'format': 'png',
    'dpi': 300,
    'bbox_inches': 'tight',
    'facecolor': 'white',
    'edgecolor': 'none',
    'transparent': False
}
```

---

## 📦 **DEPENDENCIAS REQUERIDAS**

```python
# Visualización
import plotly.express as px
import plotly.graph_objects as go
from plotly.subplots import make_subplots
import matplotlib.pyplot as plt
import seaborn as sns

# Nubes de palabras
from wordcloud import WordCloud

# Procesamiento
import pandas as pd
import numpy as np
from collections import Counter
from ast import literal_eval

# Texto
from sklearn.feature_extraction.text import CountVectorizer
import nltk
from nltk.corpus import stopwords

# Utilidades
from pathlib import Path
import json
import warnings
```

### **Instalación**

```bash
pip install plotly kaleido matplotlib seaborn wordcloud scikit-learn nltk
```

---

## 🚀 **INTEGRACIÓN CON EL PIPELINE**

### **Actualización de `main.py`**

```python
def main():
    """Ejecuta el pipeline completo de procesamiento."""
    
    # ... Fases 01-06 existentes ...
    
    # Fase 08: Generación de Visualizaciones
    print("\n[Fase 08] Generación de Visualizaciones")
    generador_viz = GeneradorVisualizaciones()
    generador_viz.procesar()
    
    print("\n" + "="*60)
    print("✅ Pipeline completado exitosamente")
    print("="*60)
```

### **Actualización de `core/__init__.py`**

```python
from .fase_08_visualizaciones import GeneradorVisualizaciones

__all__ = [
    # ... exportaciones existentes ...
    'GeneradorVisualizaciones',
]
```

---

## 📊 **SISTEMA DE REPORTES**

### **Reporte de Generación**

Al finalizar, se genera un archivo JSON con el resumen:

```json
{
  "fecha_generacion": "2025-11-09T15:30:00",
  "dataset": {
    "total_opiniones": 485,
    "rango_fechas": ["2024-01-01", "2025-09-01"],
    "categorias_identificadas": 12,
    "cobertura_topicos": 0.87
  },
  "visualizaciones": {
    "total_generadas": 32,
    "total_omitidas": 8,
    "por_seccion": {
      "dashboard": 3,
      "sentimientos": 8,
      "categorias": 7,
      "topicos": 6,
      "temporal": 4,
      "texto": 2,
      "combinados": 2
    }
  },
  "omitidas": [
    {
      "nombre": "calendar_heatmap",
      "razon": "Datos insuficientes: requiere >100 opiniones"
    }
  ],
  "recomendaciones": [
    "Para análisis temporal robusto, se recomiendan >100 opiniones",
    "Agregar más opiniones mejoraría la granularidad de tópicos"
  ]
}
```

**Archivo**: `data/visualizaciones/reporte_generacion.json`

---

## ✅ **VALIDACIONES Y FALLBACKS**

### **Matriz de Validaciones**

| Visualización | Mínimo Opiniones | Requisitos Adicionales | Fallback |
|--------------|------------------|------------------------|----------|
| Dashboard Ejecutivo | 10 | - | Simplificar a 2 cuadrantes |
| Distribución Sentimientos | 5 | - | Siempre renderizar |
| Evolución Temporal | 30 | Fechas válidas, rango >60 días | Omitir |
| Sunburst Tópicos | 50 | Tópicos identificados >50% | Treemap simple |
| Matriz Co-ocurrencia | 100 | 3+ categorías | Omitir |
| Word Cloud por Categoría | 50 | 15+ menciones por categoría | Filtrar categorías |
| Calendar Heatmap | 100 | Fechas, rango >90 días | Omitir |
| Violin Plot | 50 | - | Box Plot |
| Bigramas/Trigramas | 100 | - | Omitir |

---

## 🎯 **MENSAJES AL USUARIO**

### **Consola durante ejecución:**

```
[Fase 08] Generación de Visualizaciones
   • Dataset cargado: 485 opiniones
   • Rango temporal: 2024-01-01 a 2025-09-01
   • Categorías válidas: 12

   [Dashboard] Generando 3 visualizaciones...
   ✓ Resumen de validación generado
   ✓ Dashboard ejecutivo generado
   ✓ KPIs principales generados

   [Sentimientos] Generando 8 visualizaciones...
   ✓ Distribución de sentimientos
   ✓ Evolución temporal
   ✓ Nubes de palabras (3)
   ✓ Top palabras comparación
   ✓ Sentimiento vs subjetividad

   [Categorías] Generando 7 visualizaciones...
   ✓ Top categorías
   ✓ Sentimientos por categoría
   ✓ Fortalezas vs debilidades
   ✓ Radar chart 360°
   ⚠️  Matriz co-ocurrencia omitida: se requieren >100 opiniones
   
   [Tópicos] Generando 6 visualizaciones...
   ✓ Sunburst jerárquico
   ✓ Treemap sub-tópicos
   ✓ Top sub-tópicos mencionados
   ✓ Top sub-tópicos problemáticos
   
   [Temporal] Generando 4 visualizaciones...
   ✓ Volumen opiniones
   ✓ Evolución sentimientos
   ⚠️  Calendar heatmap omitido: rango temporal <6 meses
   
   [Texto] Generando 3 visualizaciones...
   ✓ Nube general
   ✓ Distribución longitud
   ⚠️  Bigramas/trigramas omitidos: se requieren >100 opiniones
   
   [Combinados] Generando 3 visualizaciones...
   ✓ Calificación por categoría y sentimiento
   ✓ Volumen vs sentimiento
   ✓ Correlación calificación-sentimiento

✅ Visualizaciones generadas exitosamente
   • Total generadas: 32/40
   • Guardadas en: data/visualizaciones/
   • Reporte: data/visualizaciones/reporte_generacion.json
```

---

## 🔮 **PRÓXIMOS PASOS (FUTURAS FASES)**

### **Fase 09: Generación de PDF (Futuro)**
- Compilar todas las visualizaciones PNG en un PDF profesional
- Incluir resúmenes LLM de la Fase 06
- Tabla de contenidos
- Portada personalizable
- Anexos con estadísticas

### **Fase 10: Interfaz Gráfica (Futuro)**
- Streamlit/Gradio para carga de CSV
- Visualización interactiva (Plotly HTML)
- Descarga de PDF
- Configuración de parámetros

---

## 📝 **NOTAS TÉCNICAS**

### **Manejo de Memoria**
- Las visualizaciones se generan y guardan una a una
- Se libera memoria después de cada guardado
- Ideal para datasets grandes (>10k opiniones)

### **Formato PNG vs HTML**
- **PNG**: Para inclusión en PDF (Fase 09)
- **HTML interactivo**: Posible en Fase 10 (interfaz web)

### **Personalización**
- Todos los colores, estilos y umbrales son configurables
- Fácil agregar nuevas visualizaciones al catálogo
- Sistema modular y extensible

---

## 🏆 **RESUMEN EJECUTIVO**

**Fase 08** implementa un **sistema inteligente de visualización** que:

✅ **Genera hasta 40 visualizaciones profesionales**  
✅ **Valida automáticamente** qué gráficos tienen sentido según los datos  
✅ **Exporta todo a PNG** de alta calidad (300 DPI)  
✅ **Organiza por carpetas** temáticas para fácil navegación  
✅ **Proporciona feedback claro** sobre lo generado y omitido  
✅ **Escalable**: Funciona desde 10 hasta 100,000+ opiniones  
✅ **Accionable**: Identifica claramente fortalezas/debilidades del destino  

**Resultado**: Un conjunto completo de visualizaciones listas para análisis profesional, presentaciones ejecutivas y futuro reporte PDF.

---

## 📞 **SOPORTE Y DOCUMENTACIÓN**

Para más información sobre cada visualización específica, consultar:
- Código fuente: `core/fase_08_visualizaciones.py`
- Configuración: `config/config.py`
- Ejemplos visuales: `data/visualizaciones/`

---

**Versión**: 1.0  
**Fecha**: Noviembre 2025  
**Autor**: AI Tourism Opinion Analyzer Team
