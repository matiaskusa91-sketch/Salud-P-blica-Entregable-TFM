# 🌍 Perfiles Sanitarios Globales

> Análisis multifuente de indicadores de salud pública entre países mediante limpieza de datos, PCA, clustering K-Means e interpretación con SHAP para modelizar la esperanza de vida (2000–2019).

**Trabajo de Fin de Máster — Políticas de Salud Pública**

---

## 📋 Descripción

Este repositorio contiene el pipeline analítico completo de un TFM orientado a entender cómo distintos indicadores de salud pública y contexto socioeconómico se relacionan con la **esperanza de vida** y los **patrones de mortalidad** entre países.

El proyecto integra seis fuentes de datos internacionales y construye una secuencia analítica que va desde la depuración de datos brutos hasta recomendaciones concretas de política pública para los países con mayor vulnerabilidad sanitaria.

---

## 🎯 Objetivos

- Depurar y homogeneizar datasets internacionales con estructura país-año.
- Estudiar correlaciones relevantes mediante EDA y análisis bivariado.
- Sintetizar información redundante con **PCA** cuando varias variables medían un mismo fenómeno.
- Segmentar países en perfiles sanitarios comparables mediante **clustering K-Means**.
- Estimar el peso de cada variable sobre la esperanza de vida con **regresión lineal multivariante** e interpretarla con **SHAP**.

---

## 🗂️ Estructura del Repositorio

```
tfm-salud-publica-clustering/
│
├── data/
│   ├── raw/                        # Datasets originales sin modificar
│   └── processed/
│       └── df_para_regresion.csv   # Dataset final integrado (3.800 filas, 190 países)
│
├── notebooks/
│   ├── 1_Limpieza_y_PCA_vacunas_mortalidad.ipynb
│   ├── 2_EDA_gasto_en_salud_pbi.ipynb
│   ├── 3_Suicidios.ipynb
│   ├── 4_Merge_y_Clustering.ipynb
│   ├── 5_Regresion_y_SHAP.ipynb
│   └── 6_Recomendaciones_cluster_0.ipynb
│
├── visualizaciones/                # Gráficos exportados de cada notebook
│
├── informes/
│   └── Informe_tecnico_TFM.ipynb  # Informe técnico narrativo integrado
│
├── requirements.txt
└── README.md
```

---

## 🔄 Pipeline Analítico

```
Fuentes brutas (vacunación, esperanza de vida, gasto, suicidios, mortalidad)
        │
        ▼
   Limpieza y EDA          →   193 países · 2000–2019
        │
        ▼
     PCA vacunas           →   95.5% varianza con 1 componente
     PCA mortalidad        →   68.6% varianza con 1 componente
        │
        ▼
   Merge país-año          →   3.800 obs · 190 países
        │
        ▼
  Clustering K-Means       →   3 perfiles sanitarios
        │
        ▼
  Regresión multivariante  →   R² = 0.787 en test
        │
        ▼
  Interpretación SHAP      →   Mortalidad infecciosa: variable dominante
        │
        ▼
  Recomendaciones          →   Cluster 0: 44 países de alta vulnerabilidad
```

---

## 📊 Fuentes de Datos

| Dataset | Fuente | Cobertura |
|---|---|---|
| Cobertura vacunal (DTP3, MCV1, Pol3) | WHO / UNICEF | 193 países · 2000–2019 |
| Esperanza de vida | Our World in Data / WHO | Global |
| Gasto público en salud (% PIB) | World Bank | Global |
| PIB per cápita y población | World Bank | Global |
| Tasa de suicidios estandarizada | WHO | Global |
| Causas de muerte (22 categorías) | IHME / Our World in Data | Global |

---

## 🧪 Metodología

### Reducción de dimensionalidad

Se aplicaron dos PCA independientes:

- **PCA vacunas** — DTP3, MCV1 y Pol3 tenían correlación entre sí de ~0.95. Una sola componente captura el **95.5%** de la varianza y mejora la correlación con esperanza de vida de 0.623 a **0.638**.
- **PCA mortalidad infecciosa** — 9 causas infecciosas (VIH, tuberculosis, malaria, diarrea, etc.) reducidas a `Infectious_mortality_PC1`, que explica el **68.6%** de la varianza.

### Clustering

Se evaluaron soluciones K=2, K=3 y K=4 con métricas Silhouette y Davies-Bouldin. Se seleccionó **K=3** por mejor equilibrio entre separación estadística e interpretabilidad narrativa.

| Cluster | Países | Esp. de vida | Gasto salud % PIB | Carga infecciosa |
|---|:---:|:---:|:---:|:---:|
| Alta carga infecciosa | 44 | 57.97 | 1.26 | 2.82 |
| Transición sanitaria | 91 | 71.06 | 2.65 | -0.98 |
| Alta inversión y prevención | 55 | 76.93 | 5.74 | -1.59 |

### Modelo predictivo

Regresión lineal multivariante con corte temporal (train ≤ 2015, test 2016–2019):

| Split | RMSE | MAE | R² |
|---|:---:|:---:|:---:|
| Train | 3.67 | 2.65 | 0.841 |
| Test | 3.53 | 2.77 | **0.787** |

### Interpretación SHAP

| Variable | mean(\|SHAP\|) |
|---|:---:|
| Mortalidad infecciosa (PC1) | **3.853** |
| Neoplasias (tasa) | 3.373 |
| Mortalidad cardiovascular | 1.823 |
| Vacunación (PCA) | 0.285 |
| Gasto en salud (% PIB) | 0.001 |

---

## 🔑 Resultados Principales

- La **mortalidad infecciosa** fue la variable con mayor impacto en la esperanza de vida, tanto en el modelo global como en el análisis por cluster.
- El **gasto público en salud** mostró correlación de 0.865 con esperanza de vida cuando se controla por nivel de renta y se pondera por población.
- Los **44 países del cluster 0** concentran las mayores tasas de VIH/SIDA (115.6), trastornos neonatales (91.0), infecciones respiratorias (86.3) y enfermedades diarreicas (85.0) por 100.000 habitantes.
- El modelo lineal explica cerca del **79% de la variabilidad** futura de la esperanza de vida con solo 5 variables.

---

## 💡 Recomendaciones de Política Pública (Cluster 0)

Para los países con mayor vulnerabilidad estructural, el análisis apunta a seis prioridades de intervención:

| Área | Medidas clave |
|---|---|
| **VIH/SIDA** | Diagnóstico temprano, antirretrovirales, prevención focalizada |
| **Salud materno-infantil** | Atención prenatal, parto seguro, seguimiento neonatal |
| **Infecciones respiratorias** | Vacunación, atención primaria, acceso a antibióticos |
| **Enfermedades diarreicas** | Agua segura, saneamiento, higiene comunitaria |
| **Malaria** | Control vectorial, mosquiteras, quimioprofilaxis |
| **Tuberculosis** | Cribado, diagnóstico microbiológico, adherencia terapéutica |

> El hallazgo central es que el cluster 0 necesita un enfoque **integral y comunitario**, no exclusivamente hospitalario: prevención, vacunación, salud materno-infantil y saneamiento básico ofrecen el mayor retorno esperado.

---

## ⚙️ Instalación

```bash
git clone https://github.com/tu-usuario/tfm-salud-publica-clustering.git
cd tfm-salud-publica-clustering
pip install -r requirements.txt
```

### Dependencias principales

```
pandas
numpy
scikit-learn
shap
matplotlib
seaborn
jupyter
```

---

## 🚀 Uso

Ejecutar los notebooks en orden numérico. Cada uno genera los artefactos que consume el siguiente:

```bash
jupyter notebook notebooks/1_Limpieza_y_PCA_vacunas_mortalidad.ipynb
```

El dataset final integrado `df_para_regresion.csv` se genera automáticamente en `data/processed/` al ejecutar el notebook 4.

---

## 📄 Informe Técnico

El archivo `informes/Informe_tecnico_TFM.ipynb` documenta de forma narrativa todo el flujo analítico, las decisiones metodológicas y las conclusiones. Está pensado como documento de entrega académica.

---

## 📝 Licencia

Este proyecto se distribuye bajo licencia MIT. Ver `LICENSE` para más detalles.
