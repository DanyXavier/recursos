# Correcciones para `Dany_Lucas_Garcia_TFM_PreDeposito.docx`

**Cómo usar este documento:** en Word, pulsa **Ctrl+B** (Buscar) y pega el texto de la línea **Buscar**. Es un fragmento corto y único, para que lo encuentres aunque cambie algún espacio o salto de línea. Luego sustituye el **Texto actual** por el **Texto corregido**.

Al terminar, actualiza los índices: haz clic en cada índice (contenidos, figuras y tablas) y pulsa **F9 → Actualizar toda la tabla**. Así se reflejan los cambios de pies de tabla.

Prioridades:
- **A. Errores de datos**: cifras que no coinciden con el código o con otras partes del documento. Corrígelos sí o sí.
- **B. Anexos**: nombres de archivos y referencias que no coinciden con el repositorio.
- **C. Precisión metodológica**: frases que el tribunal podría señalar al compararlas con los notebooks. Muy recomendables.
- **D. Erratas**: palabras que se perdieron y signos de puntuación.

---

## A. Errores de datos

### A1. Tamaño del conjunto de prueba (sección 4.5)
- **Buscar:** `El conjunto de prueba (56.961`
- **Texto actual:** El conjunto de prueba (56.961 transacciones) se reserva completamente…
- **Texto corregido:** El conjunto de prueba (56.962 transacciones) se reserva completamente…
- **Motivo:** 98 fraudes + 56.864 legítimas = 56.962, como en la Tabla 5.

### A2. Ratio de desbalance de ULB (sección 4.1.3)
- **Buscar:** `menos extremo que el de ULB (577:1)`
- **Texto actual:** …sustancialmente menos extremo que el de ULB (577:1).
- **Texto corregido:** …sustancialmente menos extremo que el de ULB (578:1).
- **Motivo:** en el resto del documento y en el EDA (notebook 01) el ratio es 578:1 (284.315 / 492 = 577,9).

### A3. Valor de `scale_pos_weight` (sección 6.1.1)
- **Buscar:** `(valor 578 en este experimento`
- **Texto actual:** …el parámetro scale_pos_weight (valor 578 en este experimento, igual al ratio de desbalance) pondera…
- **Texto corregido:** …el parámetro scale_pos_weight (valor 577 en este experimento, igual al ratio de desbalance del conjunto de entrenamiento: 227.451 legítimas / 394 fraudes) pondera…
- **Motivo:** en el notebook 02 el valor se calcula como `int(227.451 / 394)` = 577, sobre el train y no sobre el dataset completo.

### A4. Tasa de fraude de ULB: unificar en 0,173 %
En el dataset completo, 492 / 284.807 = 0,1727 %, que redondea a **0,173 %**. Es la cifra de tu EDA (5.1.2 y 4.1.1). Cambia **0,172 %** por **0,173 %** en estos 6 lugares:

| # | Sección | Buscar |
|---|---|---|
| a | 1.2 Planteamiento | `con una tasa de fraude del 0,172 %. Su elección` |
| b | 2.1.3 Desbalance | `representan el 0,172 % del total (492 de 284.807)` |
| c | 2.1.3 Desbalance | `(fraude) representa el 0,172 % del total` |
| d | 2.2.2 Datasets | `La tasa de fraude es del 0,172 %. Citado` |
| e | Tabla 1 | celda `0,172 %` de la fila `ULB (2015)` |
| f | 3.3 Metodología | `con una tasa de fraude del 0,172 %. Constituye` |

- **Deja sin cambiar** el **0,172 %** de la **Tabla 5** (fila *ULB – Test*): ahí es correcto, porque 98 / 56.962 = 0,172 %.
- Si prefieres mantener 0,172 % porque es la cifra que publica Kaggle, cambia entonces los 0,173 % a 0,172 %. Lo importante es que sea **una sola cifra**.

### A5. Pie de la Tabla 7 (sección 5.5)
- **Buscar:** `para XGBoost y Random Forest con SMOTE. Las filas amarillas`
- **Texto actual:** Tabla 7 Resultados del experimento de validación externa del protocolo: ULB vs. IEEE-CIS para XGBoost y Random Forest con SMOTE. Las filas amarillas corresponden a IEEE-CIS.
- **Texto corregido:** Tabla 7 Resultados del experimento de validación externa del protocolo: ULB vs. IEEE-CIS para los dos finalistas (XGBoost y Random Forest). En ULB, XGBoost corresponde a la configuración sin tratamiento y Random Forest a SMOTE; en IEEE-CIS, ambos se entrenan con SMOTE. Las filas amarillas corresponden a IEEE-CIS.
- **Motivo:** en ULB el XGBoost finalista no usa SMOTE.

---

## B. Anexos y referencias internas

### B1. Referencia al anexo de versiones (sección 4.5)
- **Buscar:** `se recoge en el Anexo A.`
- **Texto actual:** La especificación completa de versiones se recoge en el Anexo A.
- **Texto corregido:** La especificación completa de versiones se recoge en el Anexo C.

### B2. Descripción del Anexo A en la estructura del trabajo (sección 1.3)
- **Buscar:** `estructura planificada del repositorio`
- **Texto actual:** El Anexo A describe la estructura planificada del repositorio de código y los notebooks de Python que se desarrollarán en la fase experimental.
- **Texto corregido:** El Anexo A describe la estructura del repositorio de código y los notebooks de Python desarrollados en la fase experimental.
- **Motivo:** el texto estaba en futuro, de la fase de propuesta.

### B3. Lista de notebooks del Anexo A
- **Buscar:** `notebook_04_shap.ipynb`
- **Texto actual (bullets 4 y 5):**
  - notebook_04_shap.ipynb.- Análisis SHAP global y local sobre los dos mejores modelos.
  - notebook_05_validacion_externa.ipynb.- Experimento de validación externa del protocolo sobre el dataset IEEE-CIS, incluyendo Escenario A y Escenario B.
- **Texto corregido:**
  - notebook_04_SHAP.ipynb.- Análisis SHAP global y local sobre los dos mejores modelos.
  - notebook_05_generalizacion_IEEE_CIS_v2.ipynb.- Experimento de validación externa del protocolo sobre el dataset IEEE-CIS, incluyendo Escenario A y Escenario B (versión final utilizada en esta memoria). El repositorio conserva además notebook_05_generalizacion_IEEE_CIS.ipynb, una versión preliminar del experimento, solo como referencia.
- **Opcional (bullet 2):** `notebook_02_preprocesamiento.ipynb` también contiene una primera prueba de entrenamiento; la descripción actual ("escalado… división estratificada") es correcta y puede quedarse así.

### B4. Scripts de descarga en el Anexo A
- **Buscar:** `pero se proporcionan los scripts de descarga automatizada`
- **Texto actual:** …No se incluyen en el repositorio por limitaciones de tamaño, pero se proporcionan los scripts de descarga automatizada.
- **Texto corregido:** …No se incluyen en el repositorio por limitaciones de tamaño; el archivo README del repositorio indica los enlaces de descarga y la ubicación en la que deben colocarse los archivos.

### B5. Script `download_data.sh` en el Anexo B
- **Buscar:** `(download_data.sh)` (en Word puede aparecer como `download\_data.sh`; busca solo `download_data`)
- **Texto actual:** Los datasets utilizados son públicamente accesibles en Kaggle y no se incluyen en el repositorio por limitaciones de tamaño. El repositorio contiene un script de descarga automatizada (download_data.sh) con instrucciones para obtener ambos datasets:
- **Texto corregido:** Los datasets utilizados son públicamente accesibles en Kaggle y no se incluyen en el repositorio por limitaciones de tamaño. El archivo README del repositorio incluye las instrucciones para descargarlos y la carpeta en la que debe colocarse cada uno (creditcard.csv en la raíz y los archivos de IEEE-CIS en ieee_cis/):
- **Motivo:** el script no existe en el repositorio.

### B6. Nota de versiones en el Anexo C (añadir después de la tabla)
Las versiones de la tabla son correctas para los notebooks 01 a 04; así lo muestran sus salidas. El notebook 05 (IEEE-CIS) se ejecutó con versiones más recientes. Añade este párrafo **justo debajo de la tabla del Anexo C**, antes del párrafo sobre el asistente de IA:

> Las versiones indicadas corresponden a la ejecución de los notebooks 01 a 04 (dataset ULB). El experimento de validación externa sobre IEEE-CIS (notebook 05) se ejecutó posteriormente en un entorno con versiones más recientes de las mismas librerías: scikit-learn 1.9.0, XGBoost 3.3.0, imbalanced-learn 0.14.2, shap 0.52.0 y matplotlib 3.11.0, con el resto de componentes iguales.

---

## C. Precisión metodológica (muy recomendable)

Estos cambios hacen que el texto describa exactamente lo que hace el código. Protegen tu defensa: si alguien del tribunal abre los notebooks, lo que lea coincidirá con la memoria.

### C1. Descripción del Escenario A (sección 4.6)
- **Buscar:** `con la misma configuración de hiperparámetros que funcionó en ULB`
- **Texto actual:** En el Escenario A (protocolo heredado), los dos modelos finalistas XGBoost sin tratamiento y Random Forest con SMOTE se reentrenan sobre IEEE-CIS con la misma configuración de hiperparámetros que funcionó en ULB, aplicando SMOTE y división estratificada 80/20. Este escenario mide la caída de rendimiento atribuible exclusivamente al cambio de dominio.
- **Texto corregido:** En el Escenario A (protocolo heredado), los dos modelos finalistas, XGBoost y Random Forest, se reentrenan sobre IEEE-CIS con una configuración base común derivada del protocolo de ULB: SMOTE aplicado solo al conjunto de entrenamiento, división estratificada 80/20, compensación interna del desbalance (scale_pos_weight en XGBoost y class_weight='balanced' en Random Forest) e hiperparámetros intermedios dentro de los rangos explorados en ULB (XGBoost: n_estimators=200, max_depth=6, learning_rate=0,1; Random Forest: n_estimators=200, max_depth=20, max_features='sqrt'). Este escenario mide la caída de rendimiento asociada al cambio de dominio sin reajustar el modelo.
- **Motivo:** en ULB, XGBoost ganó sin SMOTE y con learning_rate=0,3, y Random Forest con max_depth=None y max_features='log2'. El escenario A no usa exactamente esas configuraciones, así que el texto actual no es exacto.

### C2. Resultados idénticos de los escenarios A y B (sección 5.5)
- **Buscar:** `coinciden exactamente, en ambos modelos, con la configuración heredada de ULB`
- **Texto actual:** …los hiperparámetros que el GridSearchCV selecciona como óptimos para IEEE-CIS coinciden exactamente, en ambos modelos, con la configuración heredada de ULB.
- **Texto corregido:** …los hiperparámetros que el GridSearchCV selecciona como óptimos para IEEE-CIS coinciden exactamente, en ambos modelos, con la configuración utilizada en el Escenario A.

- **Buscar:** `no existe una configuración alternativa que mejore el rendimiento heredado`
- **Texto actual:** En ambos casos coinciden con los valores usados en el Escenario A, lo que indica que, dentro del espacio de hiperparámetros explorado, no existe una configuración alternativa que mejore el rendimiento heredado de ULB sobre IEEE-CIS.
- **Texto corregido:** En ambos casos coinciden con los valores usados en el Escenario A, lo que indica que, dentro del espacio de hiperparámetros explorado, no existe una configuración alternativa que mejore el rendimiento del Escenario A sobre IEEE-CIS. Debe señalarse que, para evitar problemas de memoria con 472.432 transacciones de entrenamiento, la rejilla del Escenario B se redujo a cuatro combinaciones por modelo (XGBoost: n_estimators {100, 200} y max_depth {3, 6} con learning_rate=0,1; Random Forest: n_estimators {100, 200} y max_depth {10, 20} con max_features='sqrt') y que incluía la configuración del Escenario A; una búsqueda más amplia podría encontrar configuraciones mejores.

### C3. Definición del tiempo de entrenamiento (sección 5.3)
- **Buscar:** `XGBoost es el modelo más eficiente en entrenamiento sin resampling`
- **Acción:** **añadir antes** de esa frase:
  > El tiempo de entrenamiento reportado corresponde al proceso completo de GridSearchCV (validación cruzada de 5 folds sobre todas las combinaciones de la rejilla más el reentrenamiento final del mejor modelo), medido en el mismo equipo para todas las combinaciones. Random Forest y XGBoost exploran el mismo número de combinaciones (12), por lo que su comparación es directa; LightGBM explora 24 y la Regresión Logística 4.
- **Motivo:** en el notebook 03 el tiempo medido es el de `gs.fit(...)`. El objetivo específico (3.2) habla de "tiempo de entrenamiento sobre el conjunto de entrenamiento completo", y conviene aclarar qué incluye.

### C4. Compensación interna junto con resampling (sección 4.3)
- **Buscar:** `Este escenario sirve como baseline de resampling.`
- **Acción:** **añadir después** de esa frase:
  > Estos mecanismos internos se mantienen también en las estrategias SMOTE y ADASYN, de modo que estas combinaciones evalúan el efecto de añadir resampling externo sobre la configuración base de cada algoritmo, y no el resampling de forma aislada.
- **Motivo:** en el notebook 03, `class_weight`, `scale_pos_weight` e `is_unbalance` siguen activos con SMOTE y ADASYN. Esta frase explica además por qué XGBoost con SMOTE genera 243 falsos positivos (hay una doble compensación), y encaja con tu discusión en 6.1.1.

### C5. Preprocesamiento de IEEE-CIS (sección 4.1.3), opcional pero honesto
- **Buscar:** `replicando el tratamiento aplicado a Amount en ULB.`
- **Acción:** **añadir después** de esa frase:
  > Estas tres transformaciones (codificación, imputación y escalado) se ajustaron sobre el dataset combinado antes de la partición train/test. Al tratarse de transformaciones no supervisadas, que no utilizan la variable objetivo, su efecto sobre los resultados es previsiblemente muy reducido; no obstante, integrarlas dentro del pipeline de entrenamiento se incluye como mejora en las líneas de trabajo futuro.
- **Motivo:** en el notebook 05 v2 el `LabelEncoder`, la mediana y el `StandardScaler` se calculan antes del split. Si no lo aclaras, contradice la frase "libre de data leakage".

### C6. Falsos negativos (sección 6.1.3), opcional
- **Buscar:** `El análisis de las matrices de confusión muestra que estos corresponden`
- **Texto actual:** El análisis de las matrices de confusión muestra que estos corresponden a transacciones con valores de V14, V4 y V12 más cercanos a la distribución de transacciones legítimas…
- **Texto corregido:** Una exploración de estos casos sugiere que corresponden a transacciones con valores de V14, V4 y V12 más cercanos a la distribución de transacciones legítimas…
- **Motivo:** una matriz de confusión no muestra valores de variables y no hay una figura o tabla que lo respalde. Suavizarlo evita una pregunta incómoda; el análisis sistemático ya figura como trabajo futuro (7.2, tercera línea).

---

## D. Erratas (palabras perdidas y puntuación)

Todas las frases de la parte superior parecen venir de un reemplazo de "generalización" que dejó el hueco vacío.

| # | Sección | Buscar | Corregir a |
|---|---|---|---|
| D1 | 1.1 Motivación (penúltimo párrafo) | `y análisis de entre dominios` | `y análisis de robustez entre dominios` |
| D2 | 1.2 Planteamiento | `para el experimento de es el IEEE-CIS` | `para el experimento de validación externa es el IEEE-CIS` |
| D3 | 2.3 Conclusiones (1.er punto) | `la necesidad del experimento de sobre un dataset` | `la necesidad del experimento de validación externa sobre un dataset` |
| D4 | 3.1 Objetivo general | `y robustez de, evaluado sobre` | `y robustez del protocolo entre dominios, evaluado sobre` |
| D5 | 3.2 Objetivo específico 1 | `como benchmark de.` | `como benchmark de validación externa.` |
| D6 | 1.2 Pregunta de investigación | `Fraud Detection, ¿de mayor complejidad y diferente dominio?` | `Fraud Detection, de mayor complejidad y diferente dominio?` (el `¿` inicial ya está al principio de la pregunta) |
| D7 | 1.2 Ejes | `Eje 4,-` | `Eje 4.-` |

---

## Checklist final

- [ ] A1–A5 aplicados
- [ ] B1–B6 aplicados
- [ ] C1–C4 aplicados (C5 y C6 opcionales)
- [ ] D1–D7 aplicados
- [ ] Índices actualizados (F9)
- [ ] Buscar `0,172` y comprobar que solo queda en la Tabla 5
- [ ] Buscar `Anexo A` y comprobar que cada referencia apunta al anexo correcto
- [ ] Exportar a PDF y revisar las páginas modificadas
