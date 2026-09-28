# Guía de preparación para la defensa del TFM

**TFM:** *Comparativa de modelos de aprendizaje automático supervisado para detección de fraude en tarjetas de crédito: resampling, interpretabilidad SHAP y validación externa sobre IEEE-CIS*
**Autor:** Dany Xavier Lucas Garcia · **Director:** David Jiménez Cabello · Máster Universitario en Inteligencia Artificial (UNIR)

Archivos de apoyo:

- `docs/Presentacion_Defensa_TFM.pptx`: la presentación, hecha sobre la plantilla UNIR (`Presentacion.pptx`). Tiene **21 diapositivas** y cada una lleva **notas del orador** con el guion que puedes leer o memorizar (en PowerPoint: *Presentación con diapositivas → Usar vista del moderador*).
- Esta guía: qué estudiar del documento, qué decir en cada diapositiva, cifras clave, respuestas a preguntas probables del tribunal y puntos débiles que conviene tener preparados.

---

## 1. Plan de trabajo recomendado (antes de la defensa)

| Día | Tarea |
|---|---|
| 1 | Lee la sección 2 de esta guía y estudia los apartados **imprescindibles** del docx (tabla de la sección 3). |
| 2 | Repasa la presentación con las notas del orador. Ensaya en voz alta con cronómetro: **objetivo de 13 a 15 minutos**. |
| 3 | Memoriza las **cifras clave** (sección 4) y los **conceptos** (sección 5). Explícalos como si hablaras con alguien del banco que no es técnico. |
| 4 | Practica las **preguntas del tribunal** (sección 6). Contesta sin leer y compara con la respuesta propuesta. |
| 5 | Revisa los **puntos débiles** (sección 7) y corrige en el repositorio lo que se pueda corregir (sección 8). Haz un ensayo final completo. |

**Consejo general:** el tribunal valora mucho que reconozcas las limitaciones con serenidad. Tu memoria ya es prudente (dice que la contribución es *un protocolo replicable*, no *un modelo para producción*). Mantén ese mismo tono en las respuestas.

---

## 2. Mapa de la presentación: qué decir en cada diapositiva y qué estudiar del docx

| # | Diapositiva | Mensaje clave (una frase) | Sección del docx que debes dominar | Tiempo |
|---|---|---|---|---|
| 1 | Portada | Presentación personal y del tema | Resumen | 20 s |
| 2 | Índice | Cuatro bloques | 1.3 Estructura del trabajo | 15 s |
| 3 | Cifras del problema | 33.830 M$ de pérdidas, 0,173 % de fraude, por eso no sirve la *accuracy* | 1.1 Motivación · 2.1.1 Magnitud económica · 2.1.3 Desbalance | 45 s |
| 4 | Pregunta y objetivo | Buscamos el equilibrio entre detección, interpretabilidad y coste, y comprobamos si el protocolo se sostiene en otro dominio | 1.2 Planteamiento · 3.1 Objetivo general · 3.2 Objetivos específicos | 40 s |
| 5 | Contribuciones | Cuatro aportes; el más diferenciador es la validación externa | 1.2 (contribuciones) · 2.2.7 Brecha metodológica | 40 s |
| 6 | Datasets | ULB (benchmark) frente a IEEE-CIS (validación externa) | 2.2.2 Datasets · 4.1.1 · 4.1.2 · 4.1.3 | 40 s |
| 7 | Protocolo | 5 pasos; resampling **solo dentro de cada fold** (sin *data leakage*) | 4.5 Protocolo experimental · 3.3 Metodología | 50 s |
| 8 | Diseño 5×3 | Modelos, estrategias, validación y métricas | 4.2 Modelos · 4.3 Resampling · 4.4 Métricas | 45 s |
| 9 | EDA | Desbalance, importes bajos (pruebas de tarjeta), horario | 5.1 completo (5.1.2 a 5.1.7) | 40 s |
| 10 | Tabla de resultados | XGB sin tratamiento 0,883; RF+SMOTE 0,876; la RL detecta mucho pero con 4.886 falsas alarmas | 5.2.1 Tablas 3 y 4 · 5.2.4 Finalistas | 45 s |
| 11 | Heatmap | El resampling ayuda a RF y perjudica a XGB; la anomalía de LightGBM está explicada | 5.2.3 · 6.1.2 Impacto del resampling | 45 s |
| 12 | Finalistas | Casi empate en AUC-PR; XGB genera solo 11 falsas alarmas | 5.2.4 · 6.1.1 | 30 s |
| 13 | Coste | XGB 18 s frente a RF 527–1.558 s; inferencia viable en tiempo real | 5.3 · 6.3 | 40 s |
| 14 | SHAP global | V14, V4, V12 y V10 en ambos modelos | 2.2.5 · 5.4.1 · 6.2 | 45 s |
| 15 | SHAP local | Explicación de una transacción concreta, útil para auditoría | 5.4.2 · 2.1.4 Marco regulatorio | 45 s |
| 16 | Validación externa | AUC-PR baja a 0,61–0,62, el *ranking* se invierte y AUC-ROC lo habría ocultado | 4.6 Diseño · 5.5 · 6.4 | 60 s |
| 17 | Conclusiones | Mejor modelo, resampling, interpretabilidad y generalización | 7.1 Conclusiones | 45 s |
| 18 | Aporte | Sociedad, banca y Ecuador | 1.1 Motivación (párrafos 3 y 4) · 2.1.4 · 7.2 (quinta línea) | 45 s |
| 19 | Limitaciones | Dataset antiguo, preprocesamiento genérico, muestra SHAP y una sola semilla | 6.6 Limitaciones · último párrafo de 7.1 | 35 s |
| 20 | Trabajo futuro | Cinco líneas | 7.2 | 30 s |
| 21 | Gracias | — | — | — |

**Total aproximado: 13–14 minutos.** Si tu turno es de 10 minutos, puedes saltar las diapositivas 9 y 12 y acortar la 8.

---

## 3. Qué estudiar del docx, por prioridad

### Imprescindible (te preguntarán sí o sí)
1. **1.2 Planteamiento del trabajo**: la pregunta de investigación, los 4 ejes y las 4 contribuciones.
2. **2.1.3 El desafío del desbalance extremo**: por qué la *accuracy* engaña y por qué se usa AUC-PR.
3. **4.3 Estrategias de resampling** y **4.5 Protocolo experimental**: SMOTE y ADASYN dentro de cada fold, `ImbPipeline`, GridSearchCV y test reservado.
4. **4.4 Criterios de éxito y métricas**: AUC-PR como métrica principal y el criterio para elegir finalistas.
5. **5.2 Resultados sobre ULB** (Tablas 3 y 4) y **5.2.4 Selección de finalistas**.
6. **5.5 y 6.4 Validación externa**: escenarios A y B, inversión del *ranking* y cautela por las tasas base distintas.
7. **6.6 Limitaciones** y el **último párrafo de 7.1** (lo que se puede y lo que no se puede afirmar).

### Importante
8. **2.1.4 Marco regulatorio ecuatoriano** (Superintendencia de Bancos y LOPDP 2021): clave para las preguntas sobre el país.
9. **2.2.3 Modelos en la literatura** y **2.2.7 Brecha metodológica**.
10. **4.2 Selección de modelos**: hiperparámetros y grids.
11. **5.3 y 6.3 Coste computacional**.
12. **5.4 y 6.2 SHAP**: global, local y beeswarm.
13. **6.1.1 a 6.1.3**: por qué gana XGBoost, el impacto del resampling y dónde fallan los modelos.

### Repaso (lectura rápida)
14. **2.1.2 Tipología del fraude**: CNP, *account takeover*, skimming, identidad sintética.
15. **2.2.1 Evolución histórica** y **2.2.6 Estudios hispanohablantes** (Galarza y Trejo, 2025, ESPOCH).
16. **5.1 EDA**, sobre todo las cifras de *Amount* y *outliers*.
17. **6.5 Comparación con el estado del arte** (Tabla 8).
18. **Anexos A–C**: repositorio, datos y entorno (hardware).

---

## 4. Cifras clave para memorizar

| Dato | Valor |
|---|---|
| Pérdidas mundiales por fraude con tarjetas (2023) | **33.830 M USD** (Nilson Report, 2025) |
| Proyección de fraude CNP para 2030 | **49.000 M USD** (FICO, 2025) |
| ULB | 284.807 tx · 492 fraudes · **0,173 %** · ratio **578:1** · 30 variables · 0 faltantes |
| IEEE-CIS | 590.540 tx · 20.663 fraudes · **3,50 %** · ratio **27:1** · 434 variables · 115,5 M faltantes |
| Test ULB | 56.962 tx · **98 fraudes** |
| Test IEEE-CIS | 118.108 tx · **4.133 fraudes** |
| XGBoost sin tratamiento (ULB) | AUC-PR **0,883** · Recall 0,837 · Precisión 0,882 · F1 0,859 · **82 TP / 16 FN / 11 FP** · **18,0 s** |
| RF + SMOTE (ULB) | AUC-PR **0,876** · Recall 0,837 · Precisión 0,854 · F1 0,845 · 82 TP / 16 FN / 14 FP · **1.557,6 s** |
| Regresión Logística | Recall 0,918 (90/98) pero **1.389–4.886 FP** · AUC-PR máx. 0,732 |
| LightGBM sin tratamiento | AUC-PR 0,121 con `is_unbalance=True` → **0,651** con `False` |
| Velocidad | XGB **29×** más rápido que RF sin tratamiento y **43×** más que RF+SMOTE |
| Inferencia | < **0,002 ms** por transacción (todos los modelos) |
| SHAP top | **V14, V4, V12, V10** (XGB: V14 = 3,196; RF: V12 = 0,078) |
| SHAP local | P = 1,00; E[f(X)] = −0,287 → f(x) = 14,219; V14 +6,44 |
| IEEE-CIS XGB | AUC-PR **0,614** (Δ −0,269) · Recall 0,831 · Precisión 0,187 · **14.915 FP** |
| IEEE-CIS RF | AUC-PR **0,624** (Δ −0,252) · Recall 0,445 · Precisión 0,852 · **2.296 FN** |
| AUC-PR de un clasificador aleatorio en IEEE-CIS | ≈ 0,035 (la tasa de fraude) |
| Hardware | i7 de 13.ª gen · 64 GB DDR5 · RTX 3060 Ti · SSD 2 TB |

---

## 5. Conceptos que debes saber explicar en 30 segundos

- **Desbalance de clases:** una clase (fraude) es muchísimo menos frecuente. Un modelo que dice siempre "legítima" acierta el 99,83 % y no sirve para nada.
- **Precisión:** de las alertas que da el modelo, cuántas son fraude de verdad. Mide las **falsas alarmas**.
- **Recall (sensibilidad):** de los fraudes reales, cuántos detecta. Mide los **fraudes que se escapan**.
- **F1:** media armónica de precisión y recall.
- **AUC-ROC:** área bajo la curva de tasa de verdaderos positivos frente a tasa de falsos positivos. Con desbalance extremo se infla, porque la tasa de falsos positivos se divide entre muchísimos negativos.
- **AUC-PR (Average Precision):** área bajo la curva Precisión–Recall. **No usa los verdaderos negativos**, así que refleja el problema real: detectar fraude sin inundar de alertas. Su valor de referencia (azar) es la tasa de fraude.
- **SMOTE:** crea fraudes sintéticos interpolando entre un fraude y sus *k* vecinos fraudulentos más cercanos.
- **ADASYN:** como SMOTE, pero genera más ejemplos sintéticos donde el problema es más difícil (cerca de la frontera). Sube el recall, pero también las falsas alarmas.
- **Data leakage (fuga de datos):** que información del test "se cuele" en el entrenamiento. Si aplicas SMOTE antes de dividir, los sintéticos se crean a partir de fraudes que luego estarán en el test y el resultado queda inflado. Por eso se usa `ImbPipeline`, que aplica el resampling solo sobre la parte de entrenamiento de cada fold.
- **Validación cruzada estratificada de 5 folds:** divide el train en 5 partes con la misma proporción de fraude; entrena con 4 y valida con 1, cinco veces.
- **GridSearchCV:** prueba todas las combinaciones de hiperparámetros de una rejilla y se queda con la de mejor AUC-PR media en validación cruzada.
- **Bagging (Random Forest):** muchos árboles independientes sobre muestras aleatorias; se promedian. Reduce la varianza.
- **Boosting (XGBoost, LightGBM):** árboles secuenciales; cada uno corrige los errores del anterior. Reduce el sesgo y concentra el aprendizaje en los casos difíciles.
- **`scale_pos_weight` / `class_weight='balanced'` / `is_unbalance`:** hacen que un error en un fraude "pese" más en el entrenamiento, sin crear datos nuevos.
- **PCA:** transforma las variables originales en componentes independientes. En ULB se usó para anonimizar; por eso V1–V28 no tienen significado de negocio.
- **SHAP:** basado en los valores de Shapley (teoría de juegos cooperativos). Reparte la predicción entre las variables de forma que la suma de contribuciones más el valor base da la predicción. Ofrece explicación **global** (importancia media) y **local** (por transacción). TreeSHAP lo hace eficiente en modelos de árboles.

---

## 6. Preguntas probables del tribunal y respuestas propuestas

> Las respuestas están escritas para que las adaptes a tu forma de hablar. No las leas literalmente: quédate con la idea y con los datos.

### A. Aporte, sociedad, país y trabajo

**1. ¿Qué aporta este trabajo a la sociedad?**
El fraude con tarjetas no es un problema abstracto: le quita dinero a personas y comercios, y hace que la gente desconfíe de los pagos digitales. El trabajo aporta dos cosas a la sociedad. Primero, una forma rigurosa de elegir modelos que **detecten más fraude**, lo que protege el patrimonio de los usuarios. Segundo, una forma que también **mide las falsas alarmas**, es decir, cuántos clientes honestos verían bloqueada su tarjeta sin motivo. En mi experimento, la regresión logística detectaba más fraudes pero habría bloqueado casi 5.000 transacciones legítimas; XGBoost detecta casi lo mismo con solo 11. Además, con SHAP cada bloqueo se puede **explicar al cliente**, algo que es un derecho de transparencia.

**2. ¿Qué aporta a Ecuador?**
Tres cosas. (1) **Contexto:** la digitalización bancaria en Ecuador ha crecido rápido y con ella el fraude sin tarjeta presente y el skimming, que en la región sigue siendo frecuente. (2) **Regulación:** la Superintendencia de Bancos exige gestión del riesgo operativo y de fraude, con control, monitoreo y auditoría; y la Ley Orgánica de Protección de Datos Personales (2021) exige transparencia y responsabilidad en el tratamiento de datos. Un modelo que no se puede explicar es difícil de auditar y de aprobar internamente; por eso integré SHAP en el protocolo. (3) **Conocimiento local:** hay poca literatura en español sobre esto; el trabajo más cercano es el de Galarza y Trejo (2025, revista Perfiles de la ESPOCH), y este TFM lo complementa con coste computacional y validación externa. La quinta línea de trabajo futuro es justamente validarlo con datos de una entidad ecuatoriana.

**3. Usted trabaja en un banco: ¿cómo aplicaría esto en su trabajo?**

**Versión corta (para decir en unos 30 segundos):**
> "Trabajo en el área de tecnología del banco, en proyectos de tarjeta de crédito. Desde ahí no soy quien define la política de fraude, pero sí quien construye e integra las soluciones en el flujo de la tarjeta. Este trabajo me da tres cosas concretas: un **protocolo para evaluar modelos** con nuestros propios datos sin fuga de información; **criterios técnicos para desplegarlos**, porque medí que la inferencia es viable en tiempo real y que XGBoost se reentrena en segundos; y **SHAP para que cada alerta sea explicable** ante el área de fraude, auditoría y la Superintendencia. Lo implementaría primero como un piloto en paralelo al sistema actual, sin afectar a las autorizaciones."

**Versión desarrollada (si el tribunal pide más detalle):**
El valor no está en copiar el modelo, porque ULB es de 2013 y sus variables están anonimizadas, sino en **aplicar el protocolo con los datos de tarjeta del banco**. Desde tecnología lo haría así:

1. **Datos y etiquetas.** Construir un pipeline que junte las transacciones de autorización de tarjeta de crédito con las marcas de fraude confirmado (reclamos y contracargos). Ese es el dataset etiquetado equivalente a ULB, pero con variables reales: canal (presencial, comercio electrónico o sin contacto), MCC del comercio, país, importe frente al promedio del cliente, hora, etc.
2. **Evaluación con el protocolo del TFM.** Partición estratificada (idealmente temporal), validación cruzada con resampling dentro de cada fold, AUC-PR como métrica principal y registro de falsas alarmas y tiempos. Todo versionado y reproducible, igual que en los notebooks.
3. **Integración en el flujo de la tarjeta.** El modelo se expone como un **servicio de scoring** (una API) que el flujo de autorización consulta, o que en una primera fase recibe una copia de las transacciones. La inferencia medida (menos de 0,002 ms por transacción) muestra que el modelo no es el cuello de botella; el reto técnico real es obtener las variables del cliente en milisegundos, que es trabajo de arquitectura y de datos.
4. **Piloto en modo sombra (*shadow mode*).** El modelo puntúa en paralelo al motor de reglas actual **sin bloquear nada**. Se comparan sus alertas con las del sistema actual y con el fraude confirmado. Solo con evidencia se pasa a producción, y con posibilidad de *rollback*.
5. **Umbral y operación.** El umbral no lo decide tecnología sola: se acuerda con el área de fraude y riesgos según su capacidad de revisión y su apetito de riesgo. Es la lección de la regresión logística: detectar mucho con miles de falsas alarmas no es viable.
6. **Explicabilidad y cumplimiento.** Cada alerta se guarda con su explicación SHAP, para que el analista vea el motivo y para tener trazabilidad ante auditoría interna, la Superintendencia de Bancos y la LOPDP (2021).
7. **MLOps.** Monitorizar la deriva y el rendimiento, y programar el reentrenamiento. Aquí el resultado de coste es decisivo: XGBoost entrena en 18 s frente a 527–1.558 s de Random Forest, lo que permite reentrenar con frecuencia sin grandes costes de infraestructura.

Además, en los **proyectos nuevos de tarjeta** (tarjeta virtual, pagos sin contacto, billeteras digitales, comercio electrónico) propondría capturar desde el diseño los datos de canal y dispositivo que luego necesita un modelo antifraude. El experimento con IEEE-CIS mostró que ese tipo de variables cambia mucho el problema.

*(Cuida no dar detalles internos ni nombres de proveedores o sistemas del banco; habla siempre en términos de "una arquitectura típica" o "el flujo de autorización".)*

**3.1. ¿Cómo lo integraría con el motor de reglas o la herramienta antifraude que ya tiene el banco?**
No lo plantearía como un reemplazo, sino como un **complemento**. El score del modelo sería una variable más que el motor de reglas puede usar (por ejemplo, "si el score supera X y la operación es de comercio electrónico, pedir autenticación reforzada o enviar a revisión"). Así se mantiene la gobernanza actual, las reglas siguen cubriendo los casos conocidos y el modelo aporta la detección de patrones combinados. SHAP ayuda además a proponer reglas nuevas a partir de lo que aprende el modelo.

**3.2. ¿El modelo aguantaría el tiempo real de una autorización?**
La inferencia sí: medí menos de 0,002 ms por transacción en todos los modelos, muy por debajo de los tiempos de respuesta que maneja una autorización. Esa medición es de mi equipo y por lotes; en producción se suma la latencia de red y, sobre todo, la de calcular las variables del cliente (por ejemplo, su gasto de la última hora). Por eso el trabajo de tecnología está en la arquitectura de datos (almacenes de variables precalculadas y caché), no en el modelo. Mientras tanto, una alternativa es arrancar en *near real time*: puntuar justo después de la autorización y generar alertas o bloqueos preventivos.

**3.3. ¿Qué necesitaría el banco para llevarlo a producción?**
Datos históricos etiquetados con fraude confirmado; infraestructura para servir el modelo y monitorizarlo; un piloto en modo sombra; el umbral acordado con fraude y riesgos; validación del área de riesgos y cumplimiento (la explicabilidad con SHAP facilita esa aprobación); y un procedimiento de reentrenamiento y de vuelta atrás. Mi TFM cubre la parte metodológica de evaluación y selección; el resto es un proyecto de implantación en el que el área de tecnología tiene un papel central.

**4. ¿Por qué no simplemente seguir usando reglas, como hacen muchos bancos?**
Las reglas son transparentes, pero los defraudadores las aprenden y las esquivan, y además no captan combinaciones de señales débiles. El modelo aprende patrones de los datos. El análisis SHAP local lo muestra: ninguna variable decide sola; el modelo suma varias señales. Lo ideal es un **sistema híbrido**: reglas para casos conocidos y un modelo explicable para lo demás. SHAP también ayuda a proponer reglas nuevas a partir de lo que el modelo aprende.

**5. ¿Cuál es el impacto económico concreto?**
No lo cuantifiqué en dinero porque ULB no permite asociar un coste a cada transacción de forma realista. Pero la literatura (Dal Pozzolo et al., 2015) estima que un falso negativo cuesta entre 5 y 10 veces más que un falso positivo. Con esa asimetría, reducir falsas alarmas de miles a decenas manteniendo el recall tiene un impacto operativo claro. Un análisis de coste con importes reales es una extensión natural del trabajo.

### B. Planteamiento y metodología

**6. ¿Por qué eligió el dataset ULB si es de 2013?**
Porque es el **benchmark de referencia**: más de 500 publicaciones lo usan, así que mis resultados se pueden comparar directamente con la literatura. Son datos reales, no sintéticos. Reconozco su antigüedad como limitación y precisamente por eso añadí la validación externa con IEEE-CIS (2019), más reciente y de comercio electrónico.

**7. ¿Por qué AUC-PR y no AUC-ROC o accuracy?**
Con 578 legítimas por cada fraude, la accuracy es inútil (99,83 % sin detectar nada) y AUC-ROC se infla porque incluye los verdaderos negativos, que son abrumadores. AUC-PR solo mira precisión y recall, que es el dilema real del banco: detectar fraude sin saturar a los analistas. Mis propios resultados lo demuestran: al pasar a IEEE-CIS, AUC-ROC apenas cae unos 0,03, mientras que AUC-PR cae unos 0,26. Si hubiera mirado solo AUC-ROC, no habría visto el problema.

**8. ¿Qué es el data leakage y cómo lo evitó?**
Es que información del conjunto de validación o test se filtre al entrenamiento. El error típico es aplicar SMOTE a todo el dataset antes de dividir: los fraudes sintéticos se parecen a fraudes que luego están en el test y el resultado se infla. Yo usé `ImbPipeline` de imbalanced-learn dentro de `GridSearchCV`, de modo que SMOTE y ADASYN solo se aplican sobre la parte de entrenamiento de cada fold. El test (20 %) se reservó desde el principio y se evaluó una sola vez. El escalado de Time y Amount se ajustó solo con el train.

**9. ¿Por qué no usó undersampling?**
Con un ratio de 578:1 habría que descartar más del 99 % de las transacciones legítimas, perdiendo casi toda la información. Además, la literatura (Hashemi et al., 2025) muestra que SMOTE y ADASYN lo superan en AUC-PR sobre ULB.

**10. ¿Por qué esos cinco modelos y no redes neuronales o CatBoost?**
Porque cubren el espectro de los datos tabulares: un modelo lineal interpretable, un árbol individual, bagging y dos variantes de boosting. La literatura reciente (Hashemi et al., 2025) indica que en datos tabulares de tamaño moderado el gradient boosting es competitivo o superior al deep learning. CatBoost o las redes neuronales son extensiones válidas; las dejé fuera para mantener el experimento controlado y dentro de lo que permitían el tiempo y el hardware.

**11. ¿Cómo eligió los hiperparámetros?**
Con GridSearchCV y validación cruzada estratificada de 5 folds, optimizando `average_precision` (AUC-PR). Por ejemplo, para XGBoost: `n_estimators` {100, 200}, `max_depth` {3, 6} y `learning_rate` {0,05; 0,1; 0,3}. La mejor configuración de XGBoost sin tratamiento fue 200 árboles, profundidad 6 y learning rate 0,3.

**12. ¿Por qué usó una semilla fija (42)?**
Para que el experimento sea reproducible: cualquiera que ejecute los notebooks obtiene los mismos resultados. Reconozco que una sola semilla no permite estimar la variabilidad; repetir con varias semillas está dentro de las mejoras propuestas.

### C. Resultados

**13. ¿Por qué gana XGBoost?**
Por tres razones propias de ULB: (1) el boosting secuencial se especializa en los casos difíciles, y en ULB la señal se concentra en pocas variables (V14, V4); (2) `scale_pos_weight` compensa el desbalance sin alterar los datos; y (3) su regularización L1/L2 evita el sobreajuste a los 394 fraudes del train. Pero la diferencia con Random Forest + SMOTE es pequeña (0,883 frente a 0,876) y en IEEE-CIS el orden se invierte, así que no es un ganador universal.

**14. ¿La diferencia 0,883 frente a 0,876 es significativa?**
No lo afirmaría. Con 98 fraudes en el test, un solo fraude cambia el recall en cerca de 1 punto, y ambos modelos detectan exactamente los mismos 82. Por eso el criterio que realmente separa a los finalistas es el **coste computacional** (18 s frente a 1.558 s) y las falsas alarmas (11 frente a 14). Para afirmar significancia estadística haría falta repetir con varias semillas o usar *bootstrap* sobre el test; es una mejora que reconozco.

**15. ¿Por qué el resampling empeora XGBoost?**
Porque XGBoost ya compensa el desbalance con `scale_pos_weight`. En mi implementación ese parámetro se mantiene también cuando se aplica SMOTE, así que el modelo recibe una **doble compensación**: datos balanceados y además un peso extra para el fraude. El resultado es que se vuelve demasiado "alarmista": 243 falsas alarmas con SMOTE frente a 11 sin él. Además, los sintéticos interpolados pueden alterar la estructura de las componentes PCA. *(Ver sección 7, punto 1.)*

**16. ¿Por qué Random Forest sí mejora con SMOTE?**
Random Forest usa `class_weight='balanced'`, pero no tiene un mecanismo tan directo como `scale_pos_weight` de XGBoost (así lo argumenta la memoria en 6.1.2). Mi interpretación es que, como cada árbol se entrena sobre una muestra *bootstrap* con muy pocos fraudes, SMOTE aumenta su presencia y cada árbol aprende mejor la frontera. Su recall pasa de 0,755 a 0,837 con solo 11 falsas alarmas más (de 3 a 14).

**17. ¿Qué pasó con LightGBM sin resampling (0,121)?**
Fue el resultado anómalo del experimento. Formulé la hipótesis de que se debía al parámetro `is_unbalance=True` y la comprobé: repetí esa combinación con `is_unbalance=False`, con la misma partición, rejilla y semilla, y el AUC-PR subió a 0,651. No aislé el mecanismo exacto, pero confirmé que no era un error de código ni de datos. Lo documenté en lugar de ocultarlo.

**18. La regresión logística tiene el mejor recall (0,918). ¿Por qué no la eligió?**
Porque para detectar 90 fraudes generaba entre 1.389 y 4.886 falsas alarmas. En un banco con 100.000 transacciones diarias, eso equivaldría a más de 2.000 bloqueos injustos al día: operativamente inviable. Por eso optimizar solo el recall es un error, y AUC-PR, que penaliza ambas cosas, es la métrica adecuada.

**19. ¿Qué umbral de decisión usó?**
El umbral por defecto de 0,5 para las métricas de precisión, recall y F1 (el método `predict`). AUC-PR y AUC-ROC son independientes del umbral. En producción el umbral se ajustaría según la capacidad del equipo de revisión y el coste de cada tipo de error; la literatura (Dal Pozzolo et al., 2015) incluso propone que ajustar el umbral puede ser más efectivo que el resampling. Es una mejora natural.

**20. ¿Cómo midió el tiempo de entrenamiento?**
Es el tiempo total de `GridSearchCV.fit`, es decir, la búsqueda de hiperparámetros con 5 folds más el reentrenamiento final, medido en el mismo equipo para todos los modelos. Random Forest y XGBoost exploran el mismo número de combinaciones (12), así que la comparación entre ambos es justa. LightGBM explora 24 combinaciones, lo que explica parte de su mayor tiempo.

**21. ¿Cómo se comparan sus resultados con la literatura?**
Son coherentes: Ikermane et al. (2025) obtienen F1 de 0,86 con RF y de 0,83 con XGB; yo obtengo 0,845 y 0,859. Algunos estudios reportan valores de 0,99 (Babaei & Giudici, 2025), pero hay que leerlos con cuidado, porque varios trabajos aplican SMOTE antes de dividir y sobreestiman el rendimiento (Fahim et al., 2024). Mis valores son más conservadores porque el protocolo evita la fuga de datos.

### D. Interpretabilidad (SHAP)

**22. ¿Qué es SHAP y por qué lo eligió frente a LIME?**
SHAP reparte la predicción entre las variables usando los valores de Shapley de la teoría de juegos. Tiene propiedades matemáticas que LIME no garantiza: aditividad (las contribuciones suman exactamente la predicción) y consistencia. Además, TreeSHAP es exacto y eficiente para modelos de árboles como los míos. LIME aproxima localmente con un modelo lineal y puede ser inestable.

**23. Si las variables son PCA, ¿para qué sirve SHAP?**
Buena pregunta: en ULB no puedo decir qué comportamiento real es V14. Aun así, SHAP sirve para tres cosas: (1) **validar** que el modelo usa las mismas variables que el EDA señaló como discriminativas (V14, V12, V10) y que la literatura también identifica; (2) **comparar** cómo razonan los dos modelos (XGBoost concentra la señal y RF la reparte); y (3) **demostrar el procedimiento**: con datos reales de un banco, el mismo análisis diría, por ejemplo, "se bloqueó porque el importe es 10 veces el habitual y el comercio es de otro país". El valor está en el protocolo, que se traslada tal cual a datos con significado.

**24. ¿Por qué las escalas SHAP de XGBoost y RF son tan diferentes (3,2 frente a 0,078)?**
Porque XGBoost se explica en el espacio de *log-odds* (margen del modelo) y Random Forest en el de probabilidad. Por eso comparo el **orden** de las variables, no los valores absolutos.

**25. ¿Por qué calculó SHAP solo sobre 2.000 transacciones?**
Por coste computacional, sobre todo con Random Forest de 200 árboles. Con una muestra aleatoria de 2.000 la importancia global es estable, pero reconozco que una muestra mayor, o un análisis dirigido a los falsos negativos, podría revelar más patrones locales. Está en las líneas futuras.

### E. Validación externa (IEEE-CIS)

**26. ¿Por qué no aplicó directamente el modelo de ULB a IEEE-CIS?**
Porque es imposible: ULB tiene 30 variables PCA e IEEE-CIS tiene 434 variables distintas. Lo que se transfiere es el **protocolo** (modelos, resampling, validación y métricas), no el modelo entrenado. Por eso hablo de *validación externa del protocolo* y no de transferencia de modelo.

**27. ¿Por qué cae tanto el AUC-PR (≈ −0,26)?**
Por varias razones: un dominio distinto (comercio electrónico), variables más heterogéneas, muchos valores faltantes imputados con la mediana y un preprocesamiento genérico. Pero hay que leerlo con cautela: con tasas base distintas (0,17 % frente a 3,5 %), el AUC-PR no se compara de forma directa entre datasets. Aun así, 0,61–0,62 es unas 17 veces mejor que el azar (0,035).

**28. ¿Por qué los escenarios A y B dan exactamente el mismo resultado?**
Porque el GridSearchCV del escenario B, con la rejilla explorada, eligió como mejor configuración justamente la que ya usaba el escenario A. Tengo que ser honesto: la rejilla del escenario B se redujo para evitar problemas de memoria (por ejemplo, `learning_rate` fijo en 0,1 y `max_features` solo `sqrt`) e incluía la configuración de A, así que la coincidencia era un resultado posible por construcción. La conclusión correcta es que *dentro de ese espacio* no hubo mejora, no que no exista una configuración mejor. Una búsqueda más amplia es trabajo futuro. *(Ver sección 7, punto 3.)*

**29. ¿Qué significa que el ranking se invierta?**
Que no existe un "mejor modelo universal" para fraude: depende del dominio y de los datos. En la práctica bancaria, la selección siempre debe validarse con los datos propios de la entidad. Además, en IEEE-CIS los modelos tienen perfiles opuestos: XGBoost detecta más (recall 0,83) con muchas falsas alarmas y RF es muy preciso (0,85) pero deja escapar más de la mitad de los fraudes. La elección dependería del apetito de riesgo del banco y de la capacidad de revisión.

**30. ¿Por qué usó LabelEncoder en IEEE-CIS y no one-hot?**
Porque hay variables categóricas con cientos de categorías (por ejemplo, `DeviceInfo`) y el one-hot habría disparado la dimensionalidad y el coste. Los modelos de árboles no dependen de la distancia entre códigos, así que la codificación ordinal es una práctica aceptada con ellos.

### F. Limitaciones y críticas

**31. ¿Cuál es la mayor debilidad del trabajo?**
Que el benchmark principal es de 2013 y está anonimizado con PCA, lo que impide interpretar el negocio y puede no reflejar el fraude actual. Le sigue que los resultados vienen de una sola partición y semilla. Por eso formulé conclusiones acotadas: la aportación es un protocolo replicable, no un modelo listo para producción.

**32. ¿Es este modelo apto para producción?**
No directamente, y la memoria lo dice explícitamente. Para producción haría falta: datos actuales propios, variables de comportamiento del cliente (frecuencia, desvío del importe habitual), ajuste del umbral según costes, monitorización de la deriva, reentrenamiento periódico, un piloto en paralelo y aprobación de riesgos y cumplimiento. Lo que sí es transferible es el protocolo de evaluación.

**33. ¿Cómo trataría la deriva del fraude (*concept drift*) en producción?**
Monitorizando las métricas en el tiempo (AUC-PR sobre casos confirmados, tasa de alertas) y la distribución de las variables, y reentrenando periódicamente. Aquí el coste computacional es decisivo: XGBoost reentrena en segundos frente a minutos de Random Forest. También haría la validación con particiones temporales (entrenar con el pasado y evaluar con el futuro).

**34. ¿Por qué hizo una partición aleatoria y no temporal?**
Para seguir el protocolo habitual con ULB y poder comparar con la literatura; además, ULB solo abarca 48 horas. Reconozco que en producción una partición temporal es más realista, porque simula predecir fraudes futuros. Sería una mejora para la validación con datos reales.

**35. ¿Usó inteligencia artificial generativa para hacer el trabajo?**
Sí, de forma puntual y declarada en el Anexo C: usé un asistente de IA como apoyo técnico para depurar código y resolver errores de ejecución. No intervino en el diseño experimental, la interpretación de los resultados ni la redacción de las conclusiones. Ejecuté y revisé todo el código personalmente.

**36. ¿Qué haría diferente si empezara de nuevo?**
(1) Repetir con varias semillas y reportar intervalos de confianza; (2) desactivar los pesos de clase cuando se aplica resampling, para aislar el efecto de cada técnica; (3) ajustar el preprocesamiento de IEEE-CIS dentro del pipeline; (4) usar una rejilla más amplia en el escenario B; y (5) añadir un análisis de umbral y de coste económico.

---

## 7. Puntos débiles detectados al revisar los notebooks (prepáralos)

Al revisar el código frente a la memoria encontré detalles que un tribunal técnico podría detectar. Ninguno invalida el trabajo, pero conviene que los conozcas **antes** de que te los pregunten:

1. **Doble compensación del desbalance con SMOTE/ADASYN.** En `notebook_03`, los modelos mantienen `class_weight='balanced'`, `scale_pos_weight` o `is_unbalance=True` también cuando se aplica SMOTE o ADASYN. Es decir, en las columnas SMOTE y ADASYN se evalúa *resampling + pesos*, no resampling solo. Esto explica muy bien las 243 falsas alarmas de XGB+SMOTE y los miles de la regresión logística. **Cómo defenderlo:** "Es una decisión del diseño: el escenario base ya incluye la compensación interna de cada algoritmo y el resampling se añade encima; eso muestra que, cuando el modelo ya compensa, añadir resampling lo vuelve demasiado alarmista. Aislar el efecto puro del resampling, sin pesos, es una mejora que propongo." (Pregunta 15.)

2. **Tiempo de entrenamiento = tiempo total del GridSearchCV.** No es un único ajuste del modelo, sino la búsqueda completa (5 folds × combinaciones + reentrenamiento). La comparación entre RF y XGB es justa (12 combinaciones cada uno), pero LightGBM tiene 24 y la regresión logística 4. (Pregunta 20.)

3. **Escenario A "heredado" no replica exactamente la configuración ganadora en ULB.** En ULB, XGBoost ganó *sin resampling* y con `learning_rate=0,3`; en el escenario A se usa **SMOTE** y `learning_rate=0,1`. Para RF, en ULB la mejor configuración fue `max_depth=None, max_features=log2`, y en A se usa `max_depth=20, max_features=sqrt`. Además, la rejilla del escenario B es reducida y contiene la configuración de A. La memoria dice que el GridSearch "coincide exactamente con la configuración heredada de ULB": es correcto respecto al escenario A, pero A es una configuración *base*, no la óptima de ULB. **Cómo defenderlo:** "El escenario A usa una configuración base común (SMOTE para ambos, hiperparámetros intermedios) para aislar el efecto del cambio de dominio; por limitaciones de memoria, la rejilla del escenario B se redujo. Reconozco que una búsqueda más amplia podría mejorar el resultado." (Pregunta 28.)

4. **Preprocesamiento de IEEE-CIS ajustado antes de la partición.** En `notebook_05_v2`, LabelEncoder, la imputación por mediana y el StandardScaler de `TransactionAmt` se ajustan sobre el dataset completo *antes* del split 80/20. Es una fuga menor (solo estadísticos no supervisados, sin usar la etiqueta) y su efecto práctico es muy pequeño, pero técnicamente contradice "libre de data leakage" en IEEE-CIS. **Cómo defenderlo:** "Son transformaciones no supervisadas que no usan la etiqueta, así que su impacto es mínimo; lo correcto sería meterlas dentro del pipeline, y lo incluyo en la línea de preprocesamiento específico para IEEE-CIS."

5. **Una sola partición y semilla, sin intervalos de confianza**, con solo 98 fraudes en el test ULB. (Pregunta 14.)

6. **Umbral fijo de 0,5** para precisión, recall y F1. (Pregunta 19.)

7. **Afirmación en 6.1.3** ("los falsos negativos tienen valores de V14, V4 y V12 más cercanos a la distribución legítima"): no está respaldada por una figura o tabla específica en los notebooks. Si te preguntan, di que es una observación de la exploración de las matrices de confusión y que el análisis sistemático de los falsos negativos con SHAP es la tercera línea de trabajo futuro.

---

## 8. Inconsistencias del repositorio y la memoria (corrígelas si puedes antes de la defensa)

El Anexo A enlaza el repositorio público, así que un miembro del tribunal podría abrirlo:

| # | Problema | Dónde | Recomendación |
|---|---|---|---|
| 1 | ~~Los CSV de IEEE-CIS no coincidían con la memoria~~ **Corregido:** `tabla_ieee_escenario_A.csv`, `tabla_ieee_escenario_B.csv` (nuevo) y `tabla_resultados_ieee_cis.csv` se regeneraron a partir de las salidas del notebook v2 y ahora coinciden con la Tabla 7. Las filas idénticas venían del notebook v1, donde la fila "RF" se entrenaba en realidad con XGBoost. | `resultados/` | Hecho. Si te preguntan, explica ese origen: demuestra que revisaste los resultados. |
| 2 | La Figura 12 de la memoria se generó como `fig12_comparativa_2filas.png`, pero en el repo está `fig14_generalizacion_comparativa.png`; `fig14a` y `fig14b` no están. | `resultados/` | Subir las figuras de v2 o alinear los nombres del README. |
| 3 | El Anexo A cita `notebook_04_shap.ipynb` y `notebook_05_validacion_externa.ipynb`, pero los archivos reales son `notebook_04_SHAP.ipynb` y `notebook_05_generalizacion_IEEE_CIS_v2.ipynb`. El Anexo B menciona un `download_data.sh` que no existe en el repositorio. | docx, Anexos A y B | Corregir los nombres y quitar la mención al script (o crearlo). |
| 4 | Versiones de librerías distintas en tres sitios: README (scikit-learn 1.4.x, shap 0.45), Anexo C (scikit-learn 1.8.0, shap 0.51.0) y la salida del notebook 05 (scikit-learn 1.9.0, shap 0.52.0). | README / docx | Unificar con las versiones reales de la última ejecución. |
| 5 | Tamaño del test ULB: 56.961 (sección 4.5) frente a 56.962 (Tabla 5). Ratio: 578:1 y 577:1. Tasa: 0,172 % y 0,173 %. | docx | Unificar (el test real tiene 56.962 = 98 + 56.864). |
| 6 | La figura SHAP local usada en la memoria es `fig13_shap_waterfall_TP.png` (título interno "Figura 13.2"); `fig13_1` es otra transacción con valores distintos. | `resultados/` | Aclarar en el README cuál es la de la memoria. |
| 7 | La Tabla 7 muestra filas idénticas para los escenarios A y B; es correcto, pero conviene añadir una nota que explique que la rejilla de B incluía la configuración de A. | docx 5.5 | Añadir una frase de contexto (punto 3 de la sección 7). |

---

## 9. Checklist del día de la defensa

- [ ] Abrir `Presentacion_Defensa_TFM.pptx` en el ordenador de la defensa y comprobar que la fuente **Franklin Gothic** está instalada (viene con Office). Si no lo está, PowerPoint la sustituirá y puede mover algún texto: revisa las diapositivas 3, 12 y 18.
- [ ] Tener abierta la **vista del presentador** para ver las notas.
- [ ] Llevar el docx en PDF y el repositorio abierto por si piden ver el código (notebooks 03 y 05).
- [ ] Llevar anotadas las **cifras de la sección 4**.
- [ ] Ensayo final cronometrado: 13–15 minutos.
- [ ] Ante una pregunta difícil: 1) agradecer, 2) responder con un dato, 3) reconocer la limitación si existe, 4) proponer cómo lo mejorarías. Nunca inventar un resultado que no esté en la memoria.

¡Mucho éxito en la defensa!
