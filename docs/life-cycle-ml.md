# 🚀 Guía Práctica: Ciclo de Vida de un Proyecto de Machine Learning

```yml
mi_proyecto_ml/
│
├── data/                           # Datos
│   ├── raw/                        # Datos crudos (inmutables)
│   ├── processed/                  # Datos procesados
│   └── external/                   # Datos de fuentes externas
│
├── notebooks/                      # Jupyter notebooks
│   ├── 01_eda.ipynb               # Análisis exploratorio
│   ├── 02_feature_engineering.ipynb
│   └── 03_model_experimentation.ipynb
│
├── src/                            # Código fuente (Python modules)
│   ├── __init__.py
│   ├── data/                       # Scripts para procesar datos
│   │   ├── make_dataset.py
│   │   └── preprocess.py
│   ├── features/                   # Ingeniería de características
│   │   ├── build_features.py
│   │   └── feature_selection.py
│   ├── models/                     # Entrenamiento y predicción
│   │   ├── train.py
│   │   ├── predict.py
│   │   └── model_dispatcher.py     # Mapeo de modelos
│   └── visualization/              # Visualizaciones
│       └── visualize.py
│
├── models/                         # Modelos entrenados
│   ├── experiment_001/
│   └── experiment_002/
│
├── metrics/                        # Resultados y métricas
│   ├── experiment_001/
│   └── experiment_002/
│
├── config/                         # Archivos de configuración
│   ├── config.yaml
│   └── params.yaml
│
├── tests/                          # Tests unitarios
│   ├── test_data.py
│   └── test_models.py
│
├── requirements.txt               # Dependencias
├── environment.yml               # Environment de conda
├── README.md                     # Documentación
└── .gitignore                    # Archivos a ignorar en Git
```

## 📋 **FASE 0: PREPARACIÓN Y DEFINICIÓN**

### **🎯 Definición del Problema**

```python
# Antes de codificar, responde:
business_problem = "¿Qué problema de negocio resolvemos?"
success_metrics = "¿Cómo medimos el éxito? (AUC > 0.85, MAE < 1000, etc.)"
available_data = "¿Qué datos tenemos disponibles?"
constraints = "¿Limitaciones de tiempo/recursos?"
```

### **🛠️ Setup del Entorno**

```bash
# Estructura mínima viable
mkdir -p {data/{raw,processed},notebooks,src/{data,models,features},models,metrics,config}
touch requirements.txt README.md .gitignore
```

**requirements.txt inicial:**

```txt
pandas>=1.5.0
scikit-learn>=1.0.0
jupyter>=1.0.0
matplotlib>=3.5.0
seaborn>=0.11.0
```

---

## 🔍 **FASE 1: ANÁLISIS EXPLORATORIO (EDA)**

### **📊 Objetivos del EDA**

```python
# notebooks/01_eda.ipynb
"""
✅ Entender la distribución de variables
✅ Identificar valores nulos y outliers
✅ Analizar correlaciones
✅ Formular hipótesis iniciales
"""
```

### **🔧 Técnicas Esenciales**

```python
# Código típico de EDA
def basic_eda(df):
    print("Forma del dataset:", df.shape)
    print("\nValores nulos:")
    print(df.isnull().sum())
    print("\nEstadísticas descriptivas:")
    print(df.describe())
    
    # Visualizaciones clave
    df.hist(figsize=(12, 10))
    plt.show()
    
    # Matriz de correlación
    plt.figure(figsize=(10, 8))
    sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
    plt.show()
```

---

## 🧹 **FASE 2: PREPROCESAMIENTO**

### **🎯 Crear Pipeline de Datos**

```python
# src/data/make_dataset.py
def create_processing_pipeline():
    numerical_features = ['age', 'income', 'score']
    categorical_features = ['category', 'city']
    
    numerical_transformer = Pipeline(steps=[
        ('imputer', SimpleImputer(strategy='median')),
        ('scaler', StandardScaler())
    ])
    
    categorical_transformer = Pipeline(steps=[
        ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
        ('onehot', OneHotEncoder(handle_unknown='ignore'))
    ])
    
    preprocessor = ColumnTransformer(
        transformers=[
            ('num', numerical_transformer, numerical_features),
            ('cat', categorical_transformer, categorical_features)
        ])
    
    return preprocessor
```

### **📝 Checklist de Preprocesamiento**

- [ ] Manejo de valores nulos
- [ ] Codificación de variables categóricas
- [ ] Escalado/normalización
- [ ] Manejo de outliers
- [ ] Feature engineering básico
- [ ] División train/validation/test

---

## 🤖 **FASE 3: MODELADO Y EXPERIMENTACIÓN**

### **📈 Estrategia de Experimentación**

```python
# src/models/train.py
def run_baseline_models(X_train, y_train, X_val, y_val):
    models = {
        'logistic_regression': LogisticRegression(random_state=42),
        'random_forest': RandomForestClassifier(n_estimators=100, random_state=42),
        'xgboost': XGBClassifier(random_state=42),
        'svm': SVC(probability=True, random_state=42)
    }
    
    results = {}
    for name, model in models.items():
        model.fit(X_train, y_train)
        y_pred = model.predict_proba(X_val)[:, 1]
        auc_score = roc_auc_score(y_val, y_pred)
        results[name] = auc_score
    
    return results
```

### **🎛️ Configuración de Hiperparámetros**

```yaml
# config/params.yaml
random_forest:
  n_estimators: [50, 100, 200]
  max_depth: [5, 10, 15]
  min_samples_split: [2, 5, 10]

xgboost:
  learning_rate: [0.01, 0.1, 0.3]
  n_estimators: [100, 200, 300]
  max_depth: [3, 6, 9]
```

---

## 📊 **FASE 4: EVALUACIÓN Y SELECCIÓN**

### **📋 Métricas por Tipo de Problema**

```python
def evaluate_model(model, X_test, y_test, problem_type='classification'):
    if problem_type == 'classification':
        y_pred = model.predict(X_test)
        y_proba = model.predict_proba(X_test)[:, 1] if hasattr(model, 'predict_proba') else None
        
        metrics = {
            'accuracy': accuracy_score(y_test, y_pred),
            'precision': precision_score(y_test, y_pred),
            'recall': recall_score(y_test, y_pred),
            'f1': f1_score(y_test, y_pred),
            'roc_auc': roc_auc_score(y_test, y_proba) if y_proba is not None else None
        }
    
    elif problem_type == 'regression':
        y_pred = model.predict(X_test)
        metrics = {
            'mae': mean_absolute_error(y_test, y_pred),
            'mse': mean_squared_error(y_test, y_pred),
            'rmse': np.sqrt(mean_squared_error(y_test, y_pred)),
            'r2': r2_score(y_test, y_pred)
        }
    
    return metrics
```

---

## 🚀 **FASE 5: DESPLIEGUE Y DOCUMENTACIÓN**

### **📦 Empaquetado del Modelo Final**

```python
# src/models/predict.py
def save_final_pipeline(model, preprocessor, feature_names):
    pipeline = Pipeline([
        ('preprocessor', preprocessor),
        ('model', model)
    ])
    
    # Guardar pipeline completo
    joblib.dump(pipeline, 'models/final_pipeline.joblib')
    
    # Guardar metadata
    metadata = {
        'feature_names': feature_names,
        'model_version': '1.0',
        'training_date': datetime.now().isoformat(),
        'metrics': final_metrics
    }
    
    with open('models/metadata.json', 'w') as f:
        json.dump(metadata, f, indent=2)
```

### **📖 Documentación Esencial**

```markdown
# README.md

## Resumen del Proyecto
- **Problema**: Clasificación de riesgo crediticio
- **Mejor modelo**: XGBoost (AUC: 0.89)
- **Features principales**: income, credit_history, debt_ratio

## Cómo reproducir
1. Instalar dependencias: `pip install -r requirements.txt`
2. Ejecutar pipeline: `python src/models/train.py`
3. Resultados en: `metrics/final/`

## Estructura
```

proyecto/
├── data/           # Datos crudos y procesados
├── notebooks/      # Análisis exploratorio
├── src/           # Código fuente
├── models/        # Modelos entrenados
└── metrics/       # Resultados y evaluaciones

```
```

---

## ⚡ **PLANTILLA DE GITIGNORE**

```gitignore
# Datos
data/raw/
data/processed/

# Modelos
models/
*.joblib
*.pkl

# Notebooks
notebooks/.ipynb_checkpoints/

# Entornos virtuales
venv/
.env

# Archivos temporales
*.tmp
*.log
```

---

## 🎯 **CHECKLIST DE ENTREGA**

### **✅ Antes de Empezar**

- [ ] Objetivo de negocio claro definido
- [ ] Métricas de éxito establecidas
- [ ] Estructura de proyecto creada
- [ ] Entorno de desarrollo configurado

### **✅ Durante Desarrollo**

- [ ] EDA completo documentado
- [ ] Pipeline de preprocesamiento robusto
- [ ] Múltiples algoritmos probados
- [ ] Hiperparámetros optimizados
- [ ] Validación cruzada implementada

### **✅ Al Finalizar**

- [ ] Modelo final seleccionado y guardado
- [ ] Métricas de evaluación reportadas
- [ ] Código documentado y organizado
- [ ] README con instrucciones claras
- [ ] Repositorio versionado y limpio

---

## 📊 **GESTIÓN DEL TIEMPO RECOMENDADA**

| Fase | Tiempo Estimado | Actividades Clave |
|------|-----------------|-------------------|
| **Preparación** | 10% | Definición, setup, EDA |
| **Preprocesamiento** | 30% | Limpieza, feature engineering |
| **Modelado** | 40% | Experimentación, tuning |
| **Evaluación** | 15% | Validación, selección |
| **Documentación** | 5% | Empaquetado, reportes |
