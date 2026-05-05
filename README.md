# default_credit_prediction
Ejercicio de Machine Learning para predicción de pago y probabilidad de default. 

## Data
Se utiliza el [conjunto de datos](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients) (Default of Credit Card Clients) con los campos:
| name | role | type | demographic | description | units | missing_values |
|------|------|------|-------------|-------------|-------|----------------|
| ID | ID | Integer |  |  | None | no |
| X1 | Feature | Integer |  | LIMIT_BAL | None | no |
| X2 | Feature | Integer | Sex | SEX | None | no |
| X3 | Feature | Integer | Education Level | EDUCATION | None | no |
| X4 | Feature | Integer | Marital Status | MARRIAGE | None | no |
| X5 | Feature | Integer | Age | AGE | None | no |
| X6 | Feature | Integer |  | PAY_0 | None | no |
| X7 | Feature | Integer |  | PAY_2 | None | no |
| X8 | Feature | Integer |  | PAY_3 | None | no |
| X9 | Feature | Integer |  | PAY_4 | None | no |
| X10 | Feature | Integer |  | PAY_5 | None | no |
| X11 | Feature | Integer |  | PAY_6 | None | no |
| X12 | Feature | Integer |  | BILL_AMT1 | None | no |
| X13 | Feature | Integer |  | BILL_AMT2 | None | no |
| X14 | Feature | Integer |  | BILL_AMT3 | None | no |
| X15 | Feature | Integer |  | BILL_AMT4 | None | no |
| X16 | Feature | Integer |  | BILL_AMT5 | None | no |
| X17 | Feature | Integer |  | BILL_AMT6 | None | no |
| X18 | Feature | Integer |  | PAY_AMT1 | None | no |
| X19 | Feature | Integer |  | PAY_AMT2 | None | no |
| X20 | Feature | Integer |  | PAY_AMT3 | None | no |
| X21 | Feature | Integer |  | PAY_AMT4 | None | no |
| X22 | Feature | Integer |  | PAY_AMT5 | None | no |
| X23 | Feature | Integer |  | PAY_AMT6 | None | no |
| Y | Target | Binary |  | default payment next month | None | no |

- *ID*: ID of each client
- *LIMIT_BAL*: Amount of given credit in NT dollars (includes individual and family/supplementary credit)
- *SEX*: Gender (1=male, 2=female)
- *EDUCATION*: (1=graduate school, 2=university, 3=high school, 4=others, 5=unknown, 6=unknown)
- *MARRIAGE*: Marital status (1=married, 2=single, 3=others)
- *AGE*: Age in years
- *PAY_0*: Repayment status in September, 2005 (-1=pay duly, 1=payment delay for one month, 2=payment delay for two months, … 8=payment delay for eight months, 9=payment delay for nine months and above)
- *PAY_2*: Repayment status in August, 2005 (scale same as above)
- *PAY_3*: Repayment status in July, 2005 (scale same as above)
- *PAY_4*: Repayment status in June, 2005 (scale same as above)
- *PAY_5*: Repayment status in May, 2005 (scale same as above)
- *PAY_6*: Repayment status in April, 2005 (scale same as above)
- *BILL_AMT1*: Amount of bill statement in September, 2005 (NT dollar)
- *BILL_AMT2*: Amount of bill statement in August, 2005 (NT dollar)
- *BILL_AMT3*: Amount of bill statement in July, 2005 (NT dollar)
- *BILL_AMT4*: Amount of bill statement in June, 2005 (NT dollar)
- *BILL_AMT5*: Amount of bill statement in May, 2005 (NT dollar)
- *BILL_AMT6*: Amount of bill statement in April, 2005 (NT dollar)
- *PAY_AMT1*: Amount of previous payment in September, 2005 (NT dollar)
- *PAY_AMT2*: Amount of previous payment in August, 2005 (NT dollar)
- *PAY_AMT3*: Amount of previous payment in July, 2005 (NT dollar)
- *PAY_AMT4*: Amount of previous payment in June, 2005 (NT dollar)
- *PAY_AMT5*: Amount of previous payment in May, 2005 (NT dollar)
- *PAY_AMT6*: Amount of previous payment in April, 2005 (NT dollar)
- *default.payment.next.month*: Default payment (1=yes, 0=no)

## Objetivo
Se busca predecir la variable **PAY_AMT4** y **default_payment_next_month** con los modelos que se consideren apropiados.

## Estructura del repositorio
- data
    - raw
    - interim
    - processed
        - binary classification
            - train, test, validation
        - continuous regression
            - train, test, validation
- notebooks: con siguiente nomenclatura
    - 0: data extraction
    - 1: data exploration
    - 2: data preparation
    - 3: models
- outputs: imágenes y otras salidas
- reports: slide-deck 
- requirements.txt : archivo con lista de librerías y dependencias necesarias para la réplica de resultados

## Insights detectados
1. De las deficiencias en los datos, ¿cuáles y como las identificaste?
    - **INCONSISTENCIAS EN VARIABLES:**  
        - Al realizar el análisis exploratorio, rápidamente podemos identificar un nombre incorrecto en la variable *PAY_0* debido a la inconsitencia en el orden numérico con las demás variables *PAY_i*, así como la inconsistencia en tiempo comparado con las variables de *PAY_AMT* y *BILL_AMT*. 
        - Al urilizar la función *pd.describe()* también es fácil detectar inconsistencias en los valores de las variables *EDUCATION* (valores 0, 5 y 6) y *MARRIAGE* (valor 0) en las que se observan valores distintos de los especificados en la documentación otorgada, si bien podría investigarse sobre estas codificaciones (valores imputados, agregar en categoria others, etc) conservarlos dificultaría la interpretación de la variable (algo sumamente importante para modelos de probabilidad de default e interacción con clientes). Además, las variables de *PAY* se observaban con una distribución "recorrida" respecto a los valores documentados (con rango -2 a 8 con valores 0, en lugar de -1 a 9). Usando **sidetable** es muy sencillo conseguir los porcentajes y distribución acumulada de los distintos valores de estas funciones categóricas.
    - **Sesgo / outliers:** Las variables numéricas tienen un alto grado de sesgo con distribuciones aparentemente de la clase exponencial (tanto tipo discreto como continuo). 
    - **DESBALANCE DE VARIABLE DEFAULT:**
        - Usando porcentajes y gráficos observando el tamaño de las clases de la variable default detectados un desbalance de 1:3.5.
    - **Problema de temporalidad para regresión**: 
        - Para predecir la variable de Junio, no podemos utilizar las variables de Julio, Agosto y Septiembre (ya que en teoría, no existirían)
2. De realizar creación de variables, explica cuales hiciste y por qué.
    - Creación de dummies (OneHotEncoding): para los modelos líneares es mucho mejor la utilización de variables dummy porque mejoran la interpretabilidad de variables categóricas sin sesgar la interpretación de un valor ordinal. Para modelos basados en árboles de decisión esto no es del todo necesario, ya que se determinará ciertas reglas a partir de la separación de la variable categórica.
    - Ratios / combinación de variables: obtener métricas sobre el comportamiento de cada cliente en distintos margenes financieros como:
        - Utilización creditica
        -  
    - 
3. De los modelos realizados, ¿cómo seleccionaste al mejor?
    - **Optimización de hiperparámetros con Optuna:**  
    Para la elección entre mismos modelos, es importante asegurarse que se esté utilizando un buen modelo enfocado en los objetivos de negocio. Esto ayuda en conseguir un mejor ajuste del modelo y busca mejorar la generalización. 
    - **Parsimonía e interpretabilidad:**
        - En particular para el caso financiero es de suma importancia poder contar con interpretabilidad en los modelos, de lo contrario se puede ser acreedor a multas o inconformidad del cliente en caso de rechazos. Por eso para el objetivo de default no se utilizan redes neuronales. 
        - Si bien es posible utilizar herramientas para interpretabilidad, siempre es más sencillo utilizar un modelo más sencillo si tiene paridad de desempeño. Por ello se utilizan modelos baseline que ayuden a justificar una mejoría.
    - **Metricas:**
        -  *Estabilidad*: una de las primeras métricas es poder observar estabilidad entre los conjuntos de validación y entrenamiento, para poder justificar que no existe un over fitting. 
        - *Desempeño*: 
            - en crédito y riesgos se acostumbra el uso de las métricas de curva ROC, Gini y KS; sin embargo, en ML también deberíamos incluir las métricas de F1 Score y Recall debido a la diferencia en el impacto de negocio según falsos positivos. Para el caso de clasificación un buen benchmark es que aleatoriamente se alcanzaría un accuracy de 78% (dado un 22% de default).
            - para el modelo de regresión lo que cambia son algunas de las métricas utilizadas, entre las que destacarían $R^2$, RMSE y Accuracy. 
4. ¿Qué desafíos encontraste y cómo los superaste?
    - Entendimiento del dataset: llama la atención que existan distintas versiones de la documentación del dataset y no coincida con los datos per se. Sin embargo, asumí que sería parte del ejercicio y actúe conforme a la intuición y supuestos identificables. Asimismo la relación entre las variables de pagos, estado de pago y deuda me hicieron ruido al revisar algunos datos de ejemplo ya que no identifiqué un patrón claro, que mi intuición me dice que debería existir. Podría haberse realizado un modelo de regresión para identificar estas relaciones, pero lo consideré fuera del alcance de la tarea.
    - Organización de pasos y código de acuerdo a qué variable objetivo se desea. En el EDA intenté explorar todo lo posible sobre el dataset, enfocándolo hacia las variables objetivo según consideraba apropiado. Mientras que en el paso de preparación de datos preferí separar por secciones de acuerdo a lo buscado ya que los datasets si bien comparten muchos pasos de preparación similares, no pueden ser iguales debido a la temporalidad de la variable objetivo. 
    - El uso de RobustScaler con ColumnTransformer puede reacomodar las variables si de acuerdo a cuales se van a reescalar y cuales no, esto presentó un obstaculo no previsto para el cual fue necesario debuggear los resultados para darme cuenta de que solo estaban reorganizadas y poder reacomodarlas correctamente. 
    - El cómputo y tiempo es limitado, por lo que una búsqueda exhaustiva de nuevas variables, de hiperparámetros y de modelos también es limitada. Por lo que se optó por una selección sencilla, menor y general para cada una de las opciones anteriores intentando no exceder los recursos. Una de las principales consecuencias de ello, fue utilizar únicamente un conjunto de validación para la búsqueda de hiperparámetros en lugar de un cross validation con KFold o StartifiedKFold. 
    -

## Preguntas adicionales

1. Establece con tus propias palabras, algunas buenas prácticas y funciones recomendadas para optimizar operaciones de lectura, escritura y manipulación en Spark/PySpark.
    - Aprovechar la escritura con _cache_ adecuadamente: cuando se va a utilizar varias veces un resultado, es buena práctica escribir a caché el dataframe utilizado para evitar recalcular el mismo resultado en cada accionable. Sin embargo, tener cuidado con escribir datasets muy grandes o no frecuentes ya que se puede saturar la memoria.
    - Preferir funciones nativas de Spark/PySpark sobre UDFs para aprovechar la arquitectura. 
    - Siempre filtrar datos innecesarios antes de generar resultados. Tranajar con la información mínima indispensable para evitar operaciones innecesariamente caras o tardadas.
    - Definir esquemas (evitar inferSchema) en lecturas de datos.
    - Particiones (partitionBy, repartition, coalesce) depende el caso y lo que se busque hacer, pero hay que tomar en cuenta como particionar para aprovechar adecuadamente el computo paralelo
    - Broadcast join para tablas pequeñas evitando shuffle
    - explain y Spark UI para evaluación de métricas de performance e identificar cuellos de botella
2. Indica las pruebas estadísticas que has utilizado como parte del desarrollo de una solución de ciencia de datos.
    - Kolmogorov-Smirnov (KS): para corroborar normalidad
    - Population Stability Index (PSI): para corroborar data drift 
    - Tests de diferencia de medias: para evaluar diferencias sencillas entre la media de dos poblaciones
    - ANOVA: evaluar diferencia de medias en más de dos grupos
    - Test de correlaciones: identificar variables con relaciones lineales
    - Augmented Dicky-Fuller: identificación de estacionariedad 
    - Test de autocorrelaciones: generalmente con gráficos ACF 
3. En el contexto de Machine Learning y Ciencia de datos, explica:
    - a. **No Free Lunch Theorem:** este teorema establece que no hay una ruta fácil y general para resolver los problemas de ML, ya que cada problema tiene comportamientos diferentes. El teorema establece que en promedio todos los algoritmos se desempeñan de la misma forma, ya que habrá algoritmos que funcionen mejor en alguna aplicaciones, pero peor en otra. 
    - b. **Occam’s Razor:** el principio de la Navaja de Ockham surge del filósofo Ockham como crítica a las prácticas de filosofía anteriores en las que las explicaciones se explayaban de formas complejas y extensas. En contraposición, Ockham opta por la explicación más simple. En la Ciencia de Datos, y otras disciplinas, este principio esta fuertemente relacionado con la elección de los modelos más parsimoniosos, si es posible, por encima de un modelo más complejo. Recientemente las redes neuronales mostraron un cambio de paradigma debido al Teorema de Aproximación Universal, que establece que con suficientes parámetros una red neuronal puede aproximar cualquier función. Sin embargo, son modelos complejos que, en ocasiones, pueden no generar una mejoría significativa en comparación a otros modelos más simples y parsimoniosos como una regresión multiple o una regresión logística; en estos casos lo más recomendable es seguir el principio de la Navaja de Ockham y optar por una explicación simple y parsimoniosa en lugar de una red neuronal. Incluso dentro de una misma familia de modelos, digamos una regresión multiple, el principio sostiene que ante un mismo desempeño de dos modelos, aquel con menos parámetros (por lo tanto, menos variables explicativas) es preferible.  
    - c. **Data Leakage:** este concepto define un problema indeseable común en Machine Learning, que puede presentarse al entrenar un modelo directa o indirectamente con información de lo que se intenta predecir o con información que no estaría disponible antes de la predicción, sesgando el aprendizaje del modelo y con ello las métricas de desempeño. Existen muchos tipos de data leakage, pero hay que cuidarse de todos ya que es la principal razón para fallas de modelos en producción que cuentan con sustento de desempeño en los casos de pruebas. Un ejemplo de data leakage es imputar datos faltantes con la media del conjunto de datos completo (antes de separar en conjuntos de entrenamiento, prueba y validación) con lo que el modelo aprendería, aunque sea poco, de información del conjunto de prueba o validación, generando mejores métricas de desempeño. Otro ejemplo, es incluir una columna dependiente de la variable objetivo: en el contexto de predicción de impago de crédito, usar una variable como _deuda-sin-pagar_ para predecir si un cliente pagará generaría un fuerte poder predictivo ya que los pagadores tendrían siempre un valor de 0, pero es información no disponible en un ambiente real de predicción de impago para un cliente nuevo. 

## Pasos futuros y mejoras
- Uso de WOE y IV para categorizción y feature selection. No se usa debido a que scorecardpy está deprecada.
- Agregar modelos para entender la relación entre features.
- Aumentar el tamaño de las redes de búsqueda de hiperparámetros.
- Probar más modelos.
- Implementar un sklearn Pipeline para pruebas de inferencia. 