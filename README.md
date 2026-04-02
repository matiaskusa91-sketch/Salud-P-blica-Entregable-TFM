<p align="center">
  <img src="Notebooks/visualizaciones/logo.png" alt="logo" width="400"/>
</p>

# TFM - Políticas de Salud Pública

Proyecto de análisis de datos sobre políticas de salud pública, con notebooks de EDA, correlaciones, clustering, regresión con SHAP y recomendaciones por cluster.

---

## Objetivo del proyecto

El objetivo principal de este TFM es estudiar cómo distintos indicadores de salud pública y contexto socioeconómico se relacionan con la esperanza de vida y con distintos patrones de mortalidad entre países. Para ello, el proyecto integra información sobre cobertura vacunal, gasto público en salud, PIB, suicidios y causas de muerte, con el fin de identificar relaciones relevantes y construir una segmentación de países que permita interpretar mejor sus diferencias estructurales.

Además del análisis exploratorio, el proyecto busca generar valor analítico en tres niveles: comprender las correlaciones entre variables clave, agrupar países con características similares mediante clustering y estimar el peso relativo de cada variable en la esperanza de vida usando modelos de regresión e interpretabilidad con SHAP. Finalmente, se incluye un bloque de recomendaciones orientadas a la lectura de resultados por cluster.

---

## Estructura del proyecto

```
tfm-salud-publica-clustering/
│
├── Notebooks/
│   ├── 1 EDAs y Correlaciones/
│   ├── 2 Merge y Clustering/
│   ├── 3 Regresión y SHAP/
│   ├── 4 Recomendaciones y KPIs/
│   └── visualizaciones/         ← imágenes extraídas y ordenadas por notebook
│
├── requirements.txt
└── README.md
```

---

## Notebooks incluidos

| # | Notebook | Descripción |
|---|---|---|
| 1 | `Limpieza_y_PCA_vacunas_mortalidad.ipynb` | Análisis de cobertura vacunal, esperanza de vida y construcción de variables derivadas |
| 2 | `EDA gasto en salud-pbi.ipynb` | Análisis exploratorio de gasto público en salud, PIB y esperanza de vida |
| 3 | `suicidios.ipynb` | Análisis de la relación entre suicidios y esperanza de vida |
| 4 | `Merge_y_Clustering.ipynb` | Integración de datasets y segmentación de países mediante clustering |
| 5 | `Regresión_y_SHAP.ipynb` | Modelo de regresión e interpretabilidad con SHAP |
| 6 | `Recomendaciones_cluster_0.ipynb` | Visualización y recomendaciones para el cluster 0 |

---

## Visualizaciones

Se generó una carpeta por notebook dentro de `Notebooks/visualizaciones/`:

```
Notebooks/visualizaciones/
├── Limpieza_y_PCA_vacunas_mortalidad/
├── EDA_gasto_en_salud_pbi/
├── suicidios/
├── Merge_y_Clustering/
├── Regresion_y_SHAP/
└── Recomendaciones_cluster_0/
```

Cada carpeta contiene las figuras extraídas de las salidas de los notebooks para poder revisarlas sin reejecutar el análisis.

---

## Requisitos recomendados

- Python `3.11`
- `pip` actualizado

Instalación recomendada en entorno virtual:

```bash
python -m venv .venv
```

**En Windows:**

```bash
.venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt
```

**En macOS o Linux:**

```bash
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

---

## Cómo ejecutar los notebooks

1. Mantener la estructura completa de carpetas del proyecto.
2. Abrir Jupyter Lab o Jupyter Notebook desde la raíz del proyecto.
3. Ejecutar los notebooks en este orden recomendado:

```
Notebooks/1 EDAs y Correlaciones/Cobertura de vacunas y Causas de muerte/Limpieza_y_PCA_vacunas_mortalidad.ipynb
Notebooks/1 EDAs y Correlaciones/Gasto publico en salud en relacion al PIB/EDA gasto en salud-pbi.ipynb
Notebooks/1 EDAs y Correlaciones/Tasa de suicidios/suicidios.ipynb
Notebooks/2 Merge y Clustering/Merge_y_Clustering.ipynb
Notebooks/3 Regresión y SHAP/Regresión_y_SHAP.ipynb
Notebooks/4 Recomendaciones y KPIs/Recomendaciones_cluster_0.ipynb
```

---

## Compatibilidad de rutas

Los notebooks fueron ajustados para evitar rutas absolutas del autor original. Ahora buscan los datasets de forma portable dentro del proyecto, por lo que se pueden:

- descargar y ejecutar localmente
- subir a Google Drive
- abrir en Google Colab manteniendo la misma estructura de carpetas
