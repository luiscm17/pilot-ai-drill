# **Work Methodologies Document - Pilot AI Drill Project**

Phase 0: Technical Strategy Definition

## **1. Executive Summary**

The **Pilot AI Drill** project aims to develop a Rate of Penetration (ROP) prediction system using Machine Learning techniques applied to geothermal drilling data. This document establishes the working methodologies that will guide technical development, ensuring an optimal balance between control, reproducibility, and efficiency while following standard ML lifecycle phases.

## **2. Implementation Methodologies**

### **2.1. Traditional Methodology (Code-First)**

**Objective:** Maximum control and transparency in domain-specific data processing.

**Technology Stack:**

- **LAS data processing:** `welly`, `lasio`
- **Data manipulation:** `pandas`, `numpy`
- **Visualization:** `matplotlib`, `seaborn`, `plotly`
- **Machine Learning:** `scikit-learn`, `xgboost`, `lightgbm`
- **Experiment tracking:** Manual `MLflow` or custom implementation

**Primary Use Cases:**

- Initial loading and validation of .LAS files
- Petroleum domain-specific transformations
- Feature engineering based on expert knowledge
- Custom algorithm development

### **2.2. ADS SDK Methodology (Oracle Accelerated Data Science)**

**Objective:** Automation and acceleration of ML workflow native to OCI.

**Key ADS SDK Components:**

- **`DatasetFactory`:** Unified data loading from multiple sources
- **`suggest_recommendations()`:** Automated data quality diagnosis
- **`auto_transform()`:** Automated preprocessing and cleaning
- **`show_in_notebook()`:** Automated EDA with integrated visualizations
- **`OracleAutoMLProvider`:** Automated model training and optimization
- **`ADSModel`:** Unified model and metadata management
- **`ModelCatalog`:** Automated versioning and registration in OCI

**Primary Use Cases:**

- Automated cleaning of generic data problems
- Rapid standardized exploratory analysis
- Automated model baselining via AutoML
- Simplified deployment to OCI Data Science
- Automated MLOps and monitoring

### **2.3. Hybrid Methodology (Recommended)**

**Objective:** Combine strengths of both approaches while maintaining strategic flexibility.

**Integrated Workflow:**

```yml
LAS Data → welly (Domain) → Cleaned DataFrame → ADS SDK (ML) → Models
```

**Key Integration Points:**

1. **Domain-specific data transformation** with traditional tools
2. **DataFrame conversion** as interface between methodologies
3. **Automated cleaning and EDA** with ADS SDK
4. **Dual experimentation** (manual + AutoML)
5. **Unified metric selection and validation**

## **3. Project Structure Aligned with ML Lifecycle**

```yml
Pilot_AI_Drill/
│
├── 00_documentation/                 # Project documentation
│   ├── project_charter.md
│   ├── methodology_document.md      # This document
│   └── technical_decisions_log.md
│
├── 01_data/
│   ├── raw/                         # Original .LAS data (gitignored)
│   │   ├── well_16-16B/
│   │   └── external_sources/
│   ├── processed/                   # Intermediate processed data
│   │   ├── domain_cleaned/
│   │   └── ads_transformed/
│   └── final/                       # Modeling-ready data
│
├── 02_data_processing/              # ML Lifecycle: Data Processing
│   ├── notebooks/
│   │   ├── 01_data_loading_welly.ipynb        # Traditional methodology
│   │   ├── 02_domain_specific_cleaning.ipynb  # Domain wrangling
│   │   └── 03_ads_automated_cleaning.ipynb    # ADS SDK methodology
│   └── src/
│       ├── las_loader.py
│       ├── data_quality_checks.py
│       └── domain_transformations.py
│
├── 03_eda/                          # ML Lifecycle: Exploratory Data Analysis
│   ├── notebooks/
│   │   ├── 04_traditional_eda.ipynb           # Manual EDA
│   │   └── 05_ads_automated_eda.ipynb         # ADS show_in_notebook()
│   └── src/
│       ├── visualization_utils.py
│       └── statistical_analysis.py
│
├── 04_feature_engineering/          # ML Lifecycle: Feature Engineering
│   ├── notebooks/
│   │   ├── 06_domain_feature_engineering.ipynb # Traditional
│   │   └── 07_ads_feature_selection.ipynb      # ADS automated
│   └── src/
│       ├── feature_creation.py
│       └── feature_selection.py
│
├── 05_modeling/                     # ML Lifecycle: Modeling & Evaluation
│   ├── notebooks/
│   │   ├── 08_automl_baseline.ipynb           # ADS SDK methodology
│   │   ├── 09_manual_model_development.ipynb  # Traditional methodology
│   │   ├── 10_hybrid_approach.ipynb           # Hybrid methodology
│   │   └── 11_model_comparison_evaluation.ipynb
│   └── src/
│       ├── model_training.py
│       ├── hyperparameter_tuning.py
│       └── model_evaluation.py
│
├── 06_deployment/                   # ML Lifecycle: Deployment Prep
│   ├── notebooks/
│   │   └── 12_final_pipeline.ipynb            # All methodologies
│   └── src/
│       ├── pipeline_creation.py
│       └── model_packaging.py
│
├── 07_models/
│   ├── traditional/                 # Traditional approach models
│   ├── automl/                      # AutoML models
│   └── hybrid/                      # Final hybrid models
│
├── 08_experiments/
│   ├── traditional_runs/            # Traditional experiment results
│   ├── automl_runs/                 # AutoML results
│   └── comparison_reports/          # Comparative analysis
│
├── 09_config/
│   ├── domain_params.yaml           # Domain-specific parameters
│   ├── ads_config.yaml              # ADS SDK configuration
│   └── project_settings.yaml        # General project settings
│
├── 10_utils/
│   ├── logging_config.py
│   ├── data_validators.py
│   └── visualization_helpers.py
│
├── requirements.txt                 # Traditional dependencies
├── ads_requirements.txt            # ADS-specific dependencies
├── environment.yml                 # Unified Conda environment
└── README.md
```

## **4. Methodology Workflow by ML Phase**

### **4.1. Data Processing Phase**

```python
# 02_data_processing/notebooks/01_data_loading_welly.ipynb
from src.las_loader import WellDataLoader
from src.domain_transformations import apply_domain_corrections

# Domain-specific loading
loader = WellDataLoader("data/raw/well_16-16B/")
well_data = loader.load_las_files()

# Manual data wrangling and cleaning
cleaned_data = apply_domain_corrections(well_data)
```

### **4.2. EDA Phase**

```python
# 03_eda/notebooks/05_ads_automated_eda.ipynb
from ads.dataset.factory import DatasetFactory

# Load from domain-processed data
ds = DatasetFactory.open("data/processed/domain_cleaned/well_data.csv")

# Automated exploratory analysis
ds.show_in_notebook()  # Comprehensive EDA with visualizations
```

### **4.3. Feature Engineering Phase**

```python
# 04_feature_engineering/notebooks/07_ads_feature_selection.ipynb
from ads.feature_engineering import FeatureEngineer

# Automated feature engineering and selection
engineer = FeatureEngineer(ds)
engineered_ds = engineer.auto_transform()

# Compare with domain-engineered features
domain_features = load_domain_features("04_feature_engineering/processed/")
```

### **4.4. Modeling & Evaluation Phase**

```python
# 05_modeling/notebooks/10_hybrid_approach.ipynb
from src.hybrid_integration.workflow_orchestrator import HybridWorkflow

# Orchestrated comparison
workflow = HybridWorkflow(
    traditional_config="09_config/domain_params.yaml",
    ads_config="09_config/ads_config.yaml"
)

# Parallel execution
traditional_results = workflow.run_traditional_pipeline()
automl_results = workflow.run_ads_automl_pipeline()

# Comprehensive evaluation
best_model = workflow.select_best_model(
    traditional_results, 
    automl_results
)
```

### **4.5. Deployment Preparation Phase**

```python
# 06_deployment/notebooks/12_final_pipeline.ipynb
from ads.model import ADSModel
from src.model_packaging import create_production_pipeline

# Package best model from hybrid approach
production_pipeline = create_production_pipeline(best_model)

# Register in OCI Model Catalog
ads_model = ADSModel.from_estimator(
    production_pipeline, 
    artifact_dir="07_models/hybrid/final/"
)
ads_model.save()
```

## **5. Success Criteria by Methodology**

### **Traditional Methodology:**

- ✅ Complete control over domain transformations
- ✅ Full transparency in preprocessing
- ✅ Portability across different environments
- ✅ Flexibility for custom algorithms

### **ADS SDK Methodology:**

- ✅ Reduced time-to-model by ≥60%
- ✅ Automated implementation of best practices
- ✅ Simplified OCI deployment
- ✅ Automated experiment documentation

### **Hybrid Methodology:**

- ✅ Optimal balance between control and speed
- ✅ Vendor lock-in mitigation
- ✅ Cross-validation of results
- ✅ Long-term maintainability

## **6. Dependencies and Environment Management**

### **6.1. Unified Environment**

```yaml
# environment.yml
name: pilot_ai_drill
channels:
  - conda-forge
  - defaults
dependencies:
  # Traditional dependencies
  - python=3.9
  - pandas>=1.5
  - numpy>=1.21
  - scikit-learn>=1.0
  - xgboost>=1.5
  - welly>=0.5
  - lasio>=0.30
  
  # ADS dependencies
  - oracle-ads>=2.8
  - oci>=2.10
  
  # Visualization
  - matplotlib>=3.5
  - seaborn>=0.11
  - plotly>=5.10
```

### **6.2. ADS SDK Configuration**

```yaml
# 09_config/ads_config.yaml
ads_config:
  log_level: INFO
  execution:
    use_conda: true
    conda_pack: "pilot_ai_drill"
  
  automl:
    time_budget: 3600
    algorithms:
      - xgboost
      - random_forest
      - gradient_boosting
    metric: "rmse"
  
  deployment:
    infrastructure:
      shape: "VM.Standard2.4"
      bandwidth: 10
```

## **7. Versioning and Reproducibility Strategy**

### **7.1. Version Control**

- **Data:** DVC for processed data and models
- **Code:** Git with semantic commit convention
- **Experiments:** MLflow for run tracking
- **Models:** OCI Model Catalog for versioning

### **7.2. Reproducibility**

- Random seeds configured in `09_config/project_settings.yaml`
- Data snapshots at each processing phase
- Complete metadata of applied transformations
- Versioned environment containers
