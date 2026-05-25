# Predicción de aceptación de depósito bancario — Bank Marketing

**Curso:** Aprendizaje de Máquina Aplicado — EAFIT 2026  
**Estudiantes:** Sofia Rodriguez · Mariana Gutierrez · Esteban Giraldo  
**Dataset:** Bank Marketing Dataset (UCI Machine Learning Repository)  
**Tarea:** Clasificación binaria supervisada  
**Semilla global:** `RANDOM_STATE = 42`

---

## Descripción

Proyecto orientado a predecir si un cliente bancario aceptará o no una oferta de
depósito a término a partir de variables demográficas, financieras y de interacción
con campañas de marketing previas, siguiendo el flujo de trabajo CRISP-DM.

El problema se formula como una tarea de **clasificación binaria supervisada**,
donde la variable objetivo `y` toma los valores:

- `yes` → el cliente acepta el depósito
- `no` → el cliente no acepta el depósito

**Pregunta de investigación:**  
¿Es posible predecir si un cliente aceptará un depósito a término a partir de
variables demográficas, financieras y de campañas previas, logrando un ROC-AUC
superior a 0.85 en el conjunto de prueba?

**Nota metodológica:** la variable `duration` (duración de la llamada) se excluye
de todos los modelos por introducir *data leakage* — solo se conoce después de
que ocurre la interacción, por lo que no estaría disponible en un sistema
predictivo real.

---

## Estructura del repositorio

```text
MLA-project/
├── README.md                              # Punto de entrada del repositorio
├── environment.yml                        # Entorno reproducible con dependencias
│
├── data/
│   └── bank-full.csv                      # Dataset principal (sep=';', formato UCI)
│
├── notebooks/
│   ├── eda_baseline.ipynb                # Entrega 1: carga, calidad, EDA y baselines
│   ├── model_validation.ipynb            # Entrega 2: comparación de modelos y validación
|   ├── final_model.ipynb                 # Entrega 3: modelo final, SHAP e interpretación
│   └── interpretability_shap_lime.ipynb  # Notebook de interpretabilidad
│
├── figures/                               # Figuras generadas automáticamente
│   │
│   ├── — Entrega 1 —
│   ├── fig1_target_dist.png               # Distribución de la variable objetivo
│   ├── fig2_numeric_dist.png              # Distribución de variables numéricas
│   ├── fig3_boxplots_by_class.png         # Variables numéricas por clase objetivo
│   ├── fig4_categorical_acceptance.png    # Tasa de aceptación por variable categórica
│   ├── fig5_correlation_matrix.png        # Matriz de correlaciones de Pearson
│   ├── fig6_confusion_matrix_lr.png       # Matriz de confusión — Logistic Regression
│   ├── fig7_baseline_comparison.png       # Comparación de métricas entre baselines
│   │
│   ├── — Entrega 2 —
│   ├── fig_c1_comparacion_base.png        # ROC-AUC y F1 por familia de modelos
│   ├── fig_c2_leakage.png                 # Impacto de duration (con vs sin leakage)
│   ├── fig_c3_desbalance_heatmap.png      # Heatmap 3x3: modelos x técnicas de desbalance
│   ├── fig_c3_f1_configs.png              # F1 por configuración (9 configs)
│   ├── fig_c4_umbral.png                  # Curva PR y F1 vs umbral
│   ├── fig_c5_confusion_final.png         # Matrices de confusión: default vs óptimo
│   ├── fig_c6_permutation_importance.png  # Permutation importance top-15
│   │
│   ├── — Entrega 3 —
│   ├── fig_e3_01_curvas_roc_pr.png        # Curvas ROC y PR vs Logistic Regression
│   ├── fig_e3_02_confusion_matrix.png     # Matriz de confusión final
│   ├── fig_e3_03_shap_bar.png             # SHAP importancia global (top 15)
│   ├── fig_e3_04_shap_beeswarm.png        # SHAP beeswarm: dirección e intensidad
│   ├── fig_e3_05_shap_waterfall.png       # SHAP waterfall: TP vs FN individual
│   ├── fig_e3_06_shap_dependence.png      # SHAP dependence: variable más importante
│   ├── fig_e3_07_learning_curves.png      # Curvas de aprendizaje
│   ├── fig_e3_08_threshold_sensitivity.png # Sensibilidad de métricas al umbral
│   ├── fig_e3_09_perfil_fn.png            # Tasa de FN por subgrupo categórico
│   └── fig_e3_10_prob_dist_tipos.png      # Distribución de probabilidades por tipo
│
├── report/
│   ├── datacard.md                        # Ficha técnica del dataset
│   ├── report1.pdf                        # Reporte técnico — Entrega 1
│   ├── Report2.pdf                        # Reporte técnico — Entrega 2
│   └── report3.pdf                        # Reporte técnico — Entrega 3 (final)
│
└── poster/
    └── poster_final.pdf                   # Síntesis visual del proyecto (Entrega 3)
```

---

## Prerequisitos

Antes de comenzar necesitas tener instalado:

- [conda](https://docs.anaconda.com/miniconda/) (Miniconda o Anaconda)

Para verificar que está disponible:

```bash
conda --version
```

---

## Cómo reproducir los resultados

### 1. Clona el repositorio

```bash
git clone https://github.com/Egiraldol/MLA_Project.git
cd MLA_Project
```

### 2. Crea y activa el entorno

```bash
conda env create -f environment.yml
conda activate mla-project
```

Deberías ver `(mla-project)` al inicio de tu terminal.  
Si el entorno ya existe y necesitas recrearlo:

```bash
conda env remove -n mla-project
conda env create -f environment.yml
```

### 3. Lanza Jupyter

```bash
jupyter notebook
```

Esto abre el navegador automáticamente. Si no abre, copia la URL que aparece en la terminal.

### 4. Ejecuta los notebooks en orden

Los notebooks deben ejecutarse en secuencia, ya que cada uno parte del estado establecido por el anterior:

```
eda_baseline.ipynb  →  model_validation.ipynb  →  final_model.ipynb
```

En cada notebook: **Kernel → Restart & Run All**

> **Importante:** el dataset `data/bank-full.csv` usa separador `;` (formato
> estándar UCI Bank Marketing). No modificar el delimitador al descargarlo.

Las figuras se guardan automáticamente en `figures/` al ejecutar cada notebook.

---

## Resultados por entrega

### Entrega 1 — EDA y Baselines

| Modelo | Accuracy | F1-score (yes) | ROC-AUC |
|---|---|---|---|
| DummyClassifier (most_frequent) | 0.88 | 0.00 | 0.50 |
| Logistic Regression (pipeline) | ~0.90 | ~0.35 | ~0.90 |

---

### Entrega 2 — Comparación de familias de modelos

Validación: 5-fold CV estratificada sobre X_train

**Capa 1 — Tres familias base (sin técnica de desbalance):**

| Modelo | ROC-AUC (CV) | F1 (CV) |
|---|---|---|
| Logistic Regression | 0.7628 ± 0.0030 | 0.2749 ± 0.0129 |
| Random Forest | 0.7807 ± 0.0056 | 0.3318 ± 0.0183 |
| LightGBM | **0.7871 ± 0.0051** | 0.3596 ± 0.0154 |

**Capa 3 — Experimento de desbalance (3 modelos × 3 técnicas):**

| Modelo | Técnica | ROC-AUC (CV) | F1 (CV) |
|---|---|---|---|
| LightGBM | Sin técnica | 0.7871 ± 0.0051 | 0.3596 ± 0.0154 |
| LightGBM | SMOTE | 0.7835 ± 0.0040 | 0.3822 ± 0.0194 |
| **LightGBM** | **class_weight** | 0.7831 ± 0.0048 | **0.4535 ± 0.0032** |

---

### Entrega 3 — Modelo final
 
Modelo: **LightGBM + is_unbalance=True** con umbral de decisión ajustado

| Métrica | 5-fold CV | Test (final) |
|---|---|---|
| ROC-AUC | 0.7831 ± 0.0048 | 0.7959 |
| F1-score | 0.4535 ± 0.0032 | 0.4816 |
| Recall | — | 0.5246 |
| Precision | — | 0.4451 |
| Accuracy | — | 0.8679 |

> **Nota sobre el objetivo:** la meta de ROC-AUC > 0.85 no se alcanzó con
> el conjunto de features disponibles (sin `duration`) y sin búsqueda de
> hiperparámetros. El modelo supera ampliamente el baseline aleatorio (0.50)
> y establece una base sólida para mejoras futuras (ver Sección 8 del notebook 03).

---

## Decisiones metodológicas clave

| Decisión | Justificación |
|---|---|
| Excluir `duration` | Data leakage: solo se conoce post-llamada. Incluirla infla ROC-AUC ~0.05–0.10 pts (evidenciado en Capa 2, Entrega 2) |
| Split 80/20 estratificado | Preserva proporción 88/12 en train y test; `random_state=42` garantiza reproducibilidad |
| 5-fold CV estratificada | Estimación estable sin usar test; std < 0.01 entre pliegues confirma robustez |
| LightGBM sobre RF y LR | Mayor ROC-AUC y F1 en comparación experimental de 3 familias (Entrega 2, Capa 1) |
| class_weight sobre SMOTE | F1 = 0.4535 vs 0.3822; pipeline más simple y sin riesgo de leakage por oversampling |
| Umbral ajustado (≠ 0.5) | Umbral default favorece clase mayoritaria; ajuste sobre curva PR mejora detección de `yes` |
| ROC-AUC como métrica principal | Independiente del umbral y robusta al desbalance; F1 como complementaria en clase minoritaria |

---

## Referencias

- Moro, S., Cortez, P., y Rita, P. (2014).
  *A Data-Driven Approach to Predict the Success of Bank Telemarketing.*
  Decision Support Systems, 62, 22–31.

- Pedregosa et al. (2011).
  *Scikit-learn: Machine Learning in Python.*
  JMLR, 12, 2825–2830.

- James, G., Witten, D., Hastie, T. y Tibshirani, R. (2021).
  *An Introduction to Statistical Learning.*
  Springer.

- UCI Machine Learning Repository.
  *Bank Marketing Dataset.*
  https://archive.ics.uci.edu/ml/datasets/Bank+Marketing
