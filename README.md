# Predicción de aceptación de depósito bancario — Bank Marketing

**Curso:** Aprendizaje de Máquina Aplicado — EAFIT 2026  
**Estudiantes:** Sofia Rodriguez · Mariana Gutierrez · Esteban Giraldo  
**Dataset:** Bank Marketing Dataset (UCI Machine Learning Repository)  
**Tarea:** Clasificación binaria supervisada  
**Semilla global:** `RANDOM_STATE = 42`

---

## Descripción

Proyecto orientado a predecir si un cliente bancario aceptará o no
una oferta de depósito a término a partir de variables demográficas,
financieras y de interacción con campañas de marketing previas,
siguiendo el flujo de trabajo CRISP-DM.

El problema se formula como una tarea de clasificación binaria supervisada,
donde la variable objetivo `y` toma los valores:

- `yes` → el cliente acepta el depósito
- `no` → el cliente no acepta el depósito

**Pregunta de investigación:**  
¿Es posible predecir si un cliente aceptará un depósito a término
a partir de variables demográficas, financieras y de campañas previas,
logrando un ROC-AUC superior a 0.85 en el conjunto de prueba?

---

## Estructura del repositorio

```text
MLA-project/
├── README.md                  # Punto de entrada del repositorio.
│                              # Explica el proyecto, cómo reproducirlo
│                              # y el estado de cada entrega
│
├── environment.yml            # Entorno reproducible con dependencias
│                              # necesarias para ejecutar el proyecto
│
├── data/
│   ├── bank-full.csv               # Dataset principal utilizado en el proyecto
│   └── README.md              # Información sobre el dataset y su origen
│
├── notebooks/
│   └── eda_baseline.ipynb  # Notebook principal de la Entrega 1:
│                              # carga de datos, limpieza inicial,
│                              # EDA, separación train/test y baseline
│
├── figures/                   # Figuras generadas automáticamente
│   ├── fig1_target_dist.png       # Distribución de la variable objetivo
│   ├── fig2_features_dist.png     # Distribución de variables numéricas
│   ├── fig3_correlations.png       # Matriz de correlaciones
│   └── fig4_map.png       # 
│
├── report/
│   ├── datacard.md            # Descripción estructurada del dataset:
│   │                          # variables, limitaciones y riesgos
│   └── reporte_entrega1.pdf   # Reporte técnico completo
│
└── poster/                    # Vacío por ahora. Contendrá la síntesis visual 
                               # del proyecto para la Entrega 3

```

---

## Prerequisitos

Antes de comenzar necesitas tener instalado:

- [conda](https://docs.anaconda.com/miniconda/) (Miniconda o Anaconda)
Con esta herramienta gestionamos el entorno y las dependencias.

Para verificar que los tienes disponibles ejecuta:

    conda --version

## Cómo reproducir los resultados

### 1. Clona el repositorio
```bash
git clone https://github.com/Egiraldol/MLA_Project.git
```

### 2. Crea y activa el entorno
```bash
    conda env create -f environment.yml
    conda activate mla-project
```

Deberías ver (mla-project) al inicio de tu terminal.
Si el entorno ya existe y quieres recrearlo:
    conda env remove -n mla-project
    conda env create -f environment.yml

### 3. Lanza Jupyter
    jupyter notebook

Esto abre el navegador automáticamente.
Si no abre, copia la URL que aparece en la terminal.

### 4. Ejecuta el notebook
Abre notebooks/eda_baseline.ipynb
Ejecuta todas las celdas con Kernel > Restart & Run All

Las figuras se guardan automáticamente en figures/

---

## Resultados por entrega

### Entrega 1 — Baseline
| Modelo           | Accuracy   | F1-score   | ROC-AUC |
|------------------|------------|------------|---------|
| DummyClassifier  | ~0.88      | 0.00       | 0.50    |

### Entrega 2 — Comparación de modelos
| Modelo    |  Accuracy   | F1-score   | ROC-AUC |
|-----------|-------------|------------|---------|
| *Pendiente* | — | —  | —  |

### Entrega 3 — Modelo final
| Modelo    |  Accuracy   | F1-score   | ROC-AUC |
|-----------|-----|------|----|
| *Pendiente* | — | —  | —  |

---

## Próximos pasos

En las siguientes etapas del proyecto se explorarán:

- Regresión logística
- Árboles de decisión
- Random Forest
- Gradient Boosting

También se evaluarán técnicas para:

- manejo de desbalance,
- validación cruzada,
- codificación de variables categóricas,
- escalado,
- selección de variables,
- reducción de leakage.

---

## Referencias

- Moro, S., Cortez, P., y Rita, P. (2014).
  A Data-Driven Approach to Predict the Success of Bank Telemarketing.
  Decision Support Systems, 62, 22–31.

- Pedregosa et al. (2011).
  Scikit-learn: Machine Learning in Python.
  JMLR, 12, 2825–2830.

- James, G., Witten, D., Hastie, T. y Tibshirani, R. (2021).
  An Introduction to Statistical Learning.
  Springer.
  
- UCI Machine Learning Repository.
  Bank Marketing Dataset.