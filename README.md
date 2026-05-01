# default_credit_prediction
Ejercicio de Machine Learning para predicción de pago y probabilidad de default. 

## Data
Se utiliza el [conjunto de datos](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients) (Default of Credit Card Clients) con los campos:
● ID: ID of each client
● LIMIT_BAL: Amount of given credit in NT dollars (includes individual and family/supplementary credit
● SEX: Gender (1=male, 2=female)
● EDUCATION: (1=graduate school, 2=university, 3=high school, 4=others, 5=unknown, 6=unknown)
● MARRIAGE: Marital status (1=married, 2=single, 3=others)
● AGE: Age in years
● PAY_0: Repayment status in September, 2005 (-1=pay duly, 1=payment delay for one month, 2=payment delay for two months, … 8=payment delay for eight months, 9=payment delay for nine months and above)
● PAY_2: Repayment status in August, 2005 (scale same as above)
● PAY_3: Repayment status in July, 2005 (scale same as above)
● PAY_4: Repayment status in June, 2005 (scale same as above)
● PAY_5: Repayment status in May, 2005 (scale same as above)
● PAY_6: Repayment status in April, 2005 (scale same as above)
● BILL_AMT1: Amount of bill statement in September, 2005 (NT dollar)
● BILL_AMT2: Amount of bill statement in August, 2005 (NT dollar)
● BILL_AMT3: Amount of bill statement in July, 2005 (NT dollar)
● BILL_AMT4: Amount of bill statement in June, 2005 (NT dollar)
● BILL_AMT5: Amount of bill statement in May, 2005 (NT dollar)
● BILL_AMT6: Amount of bill statement in April, 2005 (NT dollar)
● PAY_AMT1: Amount of previous payment in September, 2005 (NT dollar)
● PAY_AMT2: Amount of previous payment in August, 2005 (NT dollar)
● PAY_AMT3: Amount of previous payment in July, 2005 (NT dollar)
● PAY_AMT4: Amount of previous payment in June, 2005 (NT dollar)
● PAY_AMT5: Amount of previous payment in May, 2005 (NT dollar)
● PAY_AMT6: Amount of previous payment in April, 2005 (NT dollar)
● default.payment.next.month: Default payment (1=yes, 0=no)

## Objetivo
Se busca predecir la variable **PAY_AMT4** y **default.payment.next.month** con los modelos que se consideren apropiados.

## Estructura del repositorio

## Insights detectados
1. De las deficiencias en los datos, ¿cuáles y como las identificaste?
2. De realizar creación de variables, explica cuales hiciste y por qué.
3. De los modelos realizados, ¿cómo seleccionaste al mejor?
4. ¿Qué desafíos encontraste y cómo los superaste?

## Preguntas adicionales

1. Establece con tus propias palabras, algunas buenas prácticas y funciones recomendadas para optimizar operaciones de lectura, escritura y manipulación en Spark/PySpark.
2. Indica las pruebas estadísticas que has utilizado como parte del desarrollo de una solución de ciencia de datos.
3. En el contexto de Machine Learning y Ciencia de datos, explica:
    - a. No Free Lunch Theorem: 
    - b. Occam’s Razor: el principio de la Navaja de Ockham surge del filósofo Ockham como crítica a las prácticas de filosofía anteriores en las que las explicaciones se explayaban de formas complejas y extensas. En contraposición, Ockham opta por la explicación más simple. En la Ciencia de Datos, y otras disciplinas, este principio esta fuertemente relacionado con la elección de los modelos más parsimoniosos, si es posible, por encima de un modelo más complejo. Recientemente las redes neuronales mostraron un cambio de paradigma debido al Teorema de Aproximación Universal, que establece que con suficientes parámetros una red neuronal puede aproximar cualquier función. Sin embargo, son modelos complejos que, en ocasiones, pueden no generar una mejoría significativa en comparación a otros modelos más simples y parsimoniosos como una regresión multiple o una regresión logística; en estos casos lo más recomendable es seguir el principio de la Navaja de Ockham y optar por una explicación simple y parsimoniosa en lugar de una red neuronal. Incluso dentro de una misma familia de modelos, digamos una regresión multiple, el principio sostiene que ante un mismo desempeño de dos modelos, aquel con menos parámetros (por lo tanto, menos variables explicativas) es preferible.  
    - c. Data Leakage: este concepto define un problema indeseable común en Machine Learning, que puede presentarse al entrenar un modelo directa o indirectamente con información de lo que se intenta predecir o con información que no estaría disponible antes de la predicción, sesgando el aprendizaje del modelo y con ello las métricas de desempeño. Existen muchos tipos de data leakage, pero hay que cuidarse de todos ya que es la principal razón para fallas de modelos en producción que cuentan con sustento de desempeño en los casos de pruebas. Un ejemplo de data leakage es imputar datos faltantes con la media del conjunto de datos completo (antes de separar en conjuntos de entrenamiento, prueba y validación) con lo que el modelo aprendería, aunque sea poco, de información del conjunto de prueba o validación, generando mejores métricas de desempeño. Otro ejemplo, es incluir una columna dependiente de la variable objetivo: en el contexto de predicción de impago de crédito, usar una variable como _deuda-sin-pagar_ para predecir si un cliente pagará generaría un fuerte poder predictivo ya que los pagadores tendrían siempre un valor de 0, pero es información no disponible en un ambiente real de predicción de impago para un cliente nuevo. 