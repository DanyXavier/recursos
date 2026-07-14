# Detección de fraude en tarjetas de crédito mediante aprendizaje automático supervisado

Trabajo de Fin de Máster — comparación de modelos de aprendizaje automático supervisado (Regresión Logística, Árbol de Decisión, Random Forest, XGBoost y LightGBM) combinados con estrategias de resampling (sin tratamiento, SMOTE, ADASYN) para la detección de fraude en tarjetas de crédito, con una validación externa del protocolo sobre un segundo dataset de dominio distinto.

## Datasets utilizados

Los datasets no se incluyen en este repositorio por su tamaño (están excluidos vía `.gitignore`). Se descargan directamente desde Kaggle:

- **ULB Credit Card Fraud Detection**: 284.807 transacciones, 0,173 % de fraude, 28 variables anonimizadas mediante PCA (V1–V28) más `Time` y `Amount`.
  https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud
- **IEEE-CIS Fraud Detection**: 590.540 transacciones de comercio electrónico, 3,5 % de fraude, 434 variables (`train_transaction.csv` + `train_identity.csv`).
  https://www.kaggle.com/c/ieee-fraud-detection

Tras descargarlos, coloca `creditcard.csv` en la raíz de `recursos/` y los archivos de IEEE-CIS en `recursos/ieee_cis/`.

## Estructura del repositorio

```
recursos/
├── notebook_01_EDA.ipynb                          Análisis exploratorio del dataset ULB
├── notebook_02_preprocesamiento.ipynb              División train/test y escalado
├── notebook_03_modelos_ULB.ipynb                   Entrenamiento y comparativa de los 5 modelos x 3 estrategias sobre ULB
├── notebook_04_SHAP.ipynb                          Interpretabilidad: análisis SHAP de los 2 modelos finalistas
├── notebook_05_generalizacion_IEEE_CIS_v2.ipynb    Validación externa del protocolo sobre IEEE-CIS (versión final)
├── notebook_05_generalizacion_IEEE_CIS.ipynb       Versión previa del experimento de validación externa (se conserva como referencia)
├── data_splits/                                    Particiones train/test de ULB ya generadas (csv ignorados en git)
├── ieee_cis/                                       Dataset IEEE-CIS (csv ignorados en git)
├── resultados/                                     Figuras, tablas y modelos entrenados (.pkl ignorados en git)
├── fig01_distribucion_clases.png … fig06_outliers.png   Figuras del EDA (dataset ULB)
└── requirements / entorno técnico ver más abajo
```

## Flujo de trabajo (orden de ejecución)

1. **`notebook_01_EDA.ipynb`** — Análisis exploratorio del dataset ULB: desbalance de clases, distribución temporal, variable `Amount`, variables PCA más discriminativas, correlaciones y outliers.
   Genera: `fig01_distribucion_clases.png`, `fig02_distribucion_temporal.png`, `fig03_distribucion_amount.png`, `fig04_top10_variables_pca.png`, `fig05_correlaciones.png`, `fig06_outliers.png`.

2. **`notebook_02_preprocesamiento.ipynb`** — División estratificada 80/20 en train/test y escalado de `Time`/`Amount`.
   Genera: `data_splits/X_train.csv`, `X_test.csv`, `y_train.csv`, `y_test.csv`, `config.json`.

3. **`notebook_03_modelos_ULB.ipynb`** — Entrena las 15 combinaciones modelo × estrategia (LR, DT, RF, XGBoost, LightGBM × sin tratamiento, SMOTE, ADASYN) con GridSearchCV (5-fold estratificado, métrica AUC-PR) y evalúa sobre el test reservado.
   Genera: `resultados/fig07_heatmap_metricas.png`, `fig08_curvas_pr_roc.png`, `fig09_matrices_confusion.png`, `fig10_coste_computacional.png`, `tabla_resultados_ulb.csv`, y los 20 modelos entrenados sobre ULB (`model_{ALGORITMO}_{ESTRATEGIA}.pkl`).

4. **`notebook_04_SHAP.ipynb`** — Interpretabilidad de los dos modelos finalistas (XGBoost sin tratamiento y Random Forest + SMOTE) mediante SHAP.
   Genera: `resultados/fig9_shap_xgb_3x3.png`, `fig9_shap_rf_3x3.png`, `fig9_shap_combinado.png` (versión final, array 3×3 de las 9 variables PCA más discriminativas por modelo), además de `fig11_shap_beeswarm.png` y `fig12_shap_barplot.png` (importancia media), `fig13_shap_waterfall_TP.png` / `fig13_1_shap_waterfall_TP.png` (explicación local de una transacción fraudulenta detectada) y `tabla_shap_importancia.csv`.

5. **`notebook_05_generalizacion_IEEE_CIS_v2.ipynb`** — Validación externa del protocolo: reentrena los dos modelos finalistas sobre IEEE-CIS bajo dos escenarios (A: hiperparámetros heredados de ULB; B: GridSearchCV específico para IEEE-CIS) y compara el rendimiento entre dominios.
   Genera: `resultados/tabla_resultados_ieee_cis.csv`, `tabla_ieee_escenario_A.csv`, `fig14_generalizacion_comparativa.png` (comparación ULB vs. IEEE-CIS en dos filas, una por modelo) y los modelos `model_{XGB,RF}_IEEE_{A,CIS}.pkl`.

## Resultados principales

| Modelo | Estrategia | Dataset | AUC-PR | AUC-ROC | Recall | F1 |
|---|---|---|---|---|---|---|
| XGBoost | Sin tratamiento | ULB | 0,883 | 0,960 | 0,837 | 0,859 |
| Random Forest | SMOTE | ULB | 0,876 | 0,967 | 0,837 | 0,845 |
| XGBoost | Heredado (Esc. A/B) | IEEE-CIS | 0,614 | 0,927 | 0,831 | 0,306 |
| Random Forest | Heredado (Esc. A/B) | IEEE-CIS | 0,624 | 0,911 | 0,445 | 0,584 |

XGBoost sin tratamiento es el modelo con mejor relación rendimiento/coste sobre ULB (18,0 s de entrenamiento frente a 527,1–1.557,6 s de Random Forest). Al validar el protocolo sobre IEEE-CIS, el AUC-PR cae de forma notable en ambos modelos (Δ≈−0,25/−0,27), y el ranking se invierte: Random Forest supera a XGBoost en este dominio. El detalle completo de las 15 combinaciones, el análisis SHAP y la discusión de estos resultados están en la memoria del TFM.

## Entorno técnico

| Componente | Versión |
|---|---|
| Python | 3.12 |
| scikit-learn | 1.4.x |
| XGBoost | 2.x |
| LightGBM | 4.x |
| imbalanced-learn | 0.12.x |
| shap | 0.45.x |
| pandas | 2.x |
| numpy | 1.26.x |
| matplotlib / seaborn | 3.8.x / 0.13.x |

**Hardware utilizado:** CPU Intel Core i7 (13.ª generación), 64 GB RAM DDR5, GPU NVIDIA RTX 3060 Ti, almacenamiento SSD 2 TB.

## Reproducción

```bash
pip install pandas numpy scikit-learn xgboost lightgbm imbalanced-learn shap matplotlib seaborn joblib
```

Ejecuta los notebooks en el orden indicado en la sección "Flujo de trabajo". Cada uno guarda sus salidas en `data_splits/` o `resultados/`, que son las entradas de los notebooks siguientes.

## Notas

- Los archivos `.pkl` de los modelos entrenados y los datasets (`.csv`) no se versionan en git por su tamaño; ver `.gitignore` e instrucciones de descarga arriba.
- Durante la fase experimental se recurrió puntualmente a un asistente de IA como apoyo técnico para la depuración de código y la resolución de errores en la ejecución de los pipelines, tal como se documenta en la memoria del TFM.
