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
Se busca predecir la variable *PAY_AMT4* y *default.payment.next.month* con los modelos que se consideren apropiados.

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
    a. No Free Lunch Theorem: 
    b. Occam’s Razor: 
    c. Data Leakage: 