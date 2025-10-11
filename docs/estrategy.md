# **Metodologías de Trabajo - Proyecto Pilot AI Drill**

Fase 0: Definición de Estrategia Técnica

## **1. Resumen Ejecutivo**

El proyecto **Pilot AI Drill** tiene como objetivo desarrollar un sistema de predicción de Rate of Penetration (ROP) mediante técnicas de Machine Learning aplicadas a datos de perforación geotérmica. Este documento establece las metodologías de trabajo que guiarán el desarrollo técnico, asegurando un balance óptimo entre control, reproducibilidad y eficiencia.

## **2. Metodologías de Implementación**

### **2.1. Metodología Tradicional (Code-First)**

**Objetivo:** Máximo control y transparencia en el procesamiento de datos de dominio específico.

**Stack Tecnológico:**

- **Procesamiento de datos LAS:** `welly`, `lasio`
- **Manipulación de datos:** `pandas`, `numpy`
- **Visualización:** `matplotlib`, `seaborn`, `plotly`
- **Machine Learning:** `scikit-learn`, `xgboost`, `lightgbm`
- **Tracking de experimentos:** `MLflow` manual o personalizado

**Casos de Uso Prioritarios:**

- Carga y validación inicial de archivos .LAS
- Transformaciones específicas del dominio petrolero
- Ingeniería de características basada en conocimiento experto
- Desarrollo de algoritmos personalizados

### **2.2. Metodología ADS SDK (Oracle Accelerated Data Science)**

**Objetivo:** Automatización y aceleración del flujo de trabajo de ML nativo en OCI.

**Componentes Clave del ADS SDK:**

- **`DatasetFactory`:** Carga unificada de datos desde múltiples fuentes
- **`suggest_recommendations()`:** Diagnóstico automatizado de calidad de datos
- **`auto_transform()`:** Preprocesamiento y limpieza automática
- **`show_in_notebook()`:** EDA automatizado con visualizaciones integradas
- **`OracleAutoMLProvider`:** Entrenamiento y optimización automática de modelos
- **`ADSModel`:** Gestión unificada de modelos y metadata
- **`ModelCatalog`:** Versionado y registro automático en OCI

**Casos de Uso Prioritarios:**

- Limpieza automática de problemas genéricos en datos
- Análisis exploratorio rápido y estandarizado
- Baseline automático de modelos mediante AutoML
- Despliegue nativo en OCI Data Science
- MLOps y monitoreo automatizado

### **2.3. Metodología Híbrida (Recomendada)**

**Objetivo:** Combinar las fortalezas de ambos enfoques manteniendo flexibilidad estratégica.

**Flujo de Trabajo Integrado:**

```yml
Datos .LAS → welly (Dominio) → DataFrame limpio → ADS SDK (ML) → Modelos
```

**Puntos de Integración Clave:**

1. **Transformación de datos específicos** con herramientas tradicionales
2. **Conversión a DataFrame** como interfaz entre metodologías
3. **Limpieza y EDA automatizado** con ADS SDK
4. **Experimentación dual** (manual + AutoML)
5. **Selección y validación** con métricas unificadas

## **3. Estructura de Proyecto para Notebooks**

```yml
pilot-ai-drill/
│
├── 00_docs/                  # Documentación del proyecto
│   ├── project_charter.md
│   ├── methodology_document.md       # Este documento
│   └── technical_decisions_log.md
│
├── 01_data/
│   ├── raw/                          # Datos originales .LAS (gitignored)
│   │   ├── well_16-16B/
│   │   └── external_sources/
│   ├── processed/                    # Datos intermedios procesados
│   │   ├── domain_cleaned/
│   │   └── ads_transformed/
│   └── final/                        # Datos listos para modelado
│
├── 02_notebooks/
│   ├── 01_data_loading_welly.ipynb   # Metodología tradicional
│   ├── 02_domain_transformations.ipynb
│   ├── 03_ads_automated_cleaning.ipynb # Metodología ADS SDK
│   ├── 04_automl_baseline.ipynb
│   ├── 05_manual_model_development.ipynb # Metodología híbrida
│   ├── 06_model_comparison.ipynb
│   └── 07_final_pipeline.ipynb
│
├── 03_src/
│   ├── domain_processing/            # Código metodología tradicional
│   │   ├── las_loader.py
│   │   ├── geophysical_transforms.py
│   │   └── quality_checks.py
│   ├── ads_workflows/               # Código metodología ADS SDK
│   │   ├── auto_cleaner.py
│   │   ├── automl_runner.py
│   │   └── model_deployer.py
│   └── hybrid_integration/          # Código metodología híbrida
│       ├── workflow_orchestrator.py
│       └── result_comparator.py
│
├── 04_models/
│   ├── traditional/                 # Modelos enfoque tradicional
│   ├── automl/                      # Modelos AutoML
│   └── hybrid/                      # Modelos finales híbridos
│
├── 05_experiments/
│   ├── traditional_runs/            # Resultados experimentos tradicionales
│   ├── automl_runs/                 # Resultados AutoML
│   └── comparison_reports/          # Análisis comparativos
│
├── 06_config/
│   ├── domain_params.yaml           # Parámetros dominio específico
│   ├── ads_config.yaml              # Configuración ADS SDK
│   └── project_settings.yaml        # Configuración general proyecto
│
├── 07_utils/
│   ├── logging_config.py
│   ├── data_validators.py
│   └── visualization_helpers.py
│
├── requirements.txt                 # Dependencias tradicionales
├── ads_requirements.txt            # Dependencias específicas ADS
├── environment.yml                 # Entorno Conda unificado
└── README.md
```

## **4. Flujo de Trabajo por Metodología**

### **4.1. Metodología Tradicional**

```python
# notebooks/01_data_loading_welly.ipynb
from src.domain_processing.las_loader import WellDataLoader
from src.domain_processing.geophysical_transforms import apply_domain_corrections

# Carga específica de dominio
loader = WellDataLoader("data/raw/well_16-16B/")
well_data = loader.load_las_files()

# Transformaciones manuales basadas en conocimiento experto
corrected_data = apply_domain_corrections(well_data)
```

### **4.2. Metodología ADS SDK**

```python
# notebooks/03_ads_automated_cleaning.ipynb
from ads.dataset.factory import DatasetFactory
from ads.automl.provider import OracleAutoMLProvider

# Carga desde datos ya procesados del dominio
ds = DatasetFactory.open("data/processed/domain_cleaned/well_data.csv")

# Automatización de limpieza y EDA
ds.suggest_recommendations()
ds.auto_transform()
ds.show_in_notebook()

# AutoML para baseline
automl = OracleAutoMLProvider(ds)
baseline_model = automl.train()
```

### **4.3. Metodología Híbrida**

```python
# notebooks/05_manual_model_development.ipynb
from src.hybrid_integration.workflow_orchestrator import HybridWorkflow

# Orquestación inteligente
workflow = HybridWorkflow(
    traditional_config="config/domain_params.yaml",
    ads_config="config/ads_config.yaml"
)

# Ejecución paralela de ambos enfoques
traditional_results = workflow.run_traditional_pipeline()
automl_results = workflow.run_ads_automl_pipeline()

# Comparación y selección
best_model = workflow.select_best_model(
    traditional_results, 
    automl_results
)
```

## **5. Criterios de Éxito por Metodología**

### **Metodología Tradicional:**

- ✅ Control total sobre transformaciones de dominio
- ✅ Transparencia completa en preprocesamiento
- ✅ Portabilidad entre diferentes entornos
- ✅ Flexibilidad para algoritmos personalizados

### **Metodología ADS SDK:**

- ✅ Time-to-model reducido en ≥60%
- ✅ Implementación de best practices automatizadas
- ✅ Despliegue en OCI simplificado
- ✅ Documentación automática de experimentos

### **Metodología Híbrida:**

- ✅ Balance óptimo entre control y velocidad
- ✅ Mitigación de vendor lock-in
- ✅ Validación cruzada de resultados
- ✅ Mantenibilidad a largo plazo

## **6. Gestión de Dependencias y Entornos**

### **6.1. Entorno Unificado**

```yaml
# environment.yml
name: pilot_ai_drill
channels:
  - conda-forge
  - defaults
dependencies:
  # Dependencias tradicionales
  - python=3.9
  - pandas>=1.5
  - numpy>=1.21
  - scikit-learn>=1.0
  - xgboost>=1.5
  - welly>=0.5
  - lasio>=0.30
  
  # Dependencias ADS
  - oracle-ads>=2.8
  - oci>=2.10
  
  # Visualización
  - matplotlib>=3.5
  - seaborn>=0.11
  - plotly>=5.10
```

### **6.2. Configuración ADS SDK**

```yaml
# config/ads_config.yaml
ads_config:
  log_level: INFO
  execution:
    use_conda: True
    conda_pack: "pilot_ai_drill"
  
  automl:
    time_budget: 3600
    algorithms:
      - xgboost
      - random_forest
      - logistic_regression
    metric: "rmse"
  
  deployment:
    infrastructure:
      shape: "VM.Standard2.4"
      bandwidth: 10
```

## **7. Estrategia de Versionado y Reproducibilidad**

### **7.1. Control de Versiones**

- **Datos:** DVC para datos procesados y modelos
- **Código:** Git con convención de commits semántica
- **Experimentos:** MLflow para tracking de corridas
- **Modelos:** Model Catalog de OCI para versionado

### **7.2. Reproducibilidad**

- Semillas aleatorias configuradas en `config/project_settings.yaml`
- Snapshots de datos en cada fase de procesamiento
- Metadata completa de transformaciones aplicadas
- Environment containers versionados
