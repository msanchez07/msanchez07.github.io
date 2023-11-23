# Error Porcentual Absoluto Medio (MAPE)
El Error Porcentual Absoluto Medio (MAPE) es una métrica que te permite medir la precisión relativa de las predicciones de un modelo en términos porcentuales. En el contexto de la predicción de precios de casas, exploraremos cómo funciona el MAPE.

$$MAPE =  \frac{100}{n} \sum_{i=1}^{n}|\frac{y_{i}  - ŷ_{i}}{y_{i}}|$$



#### Ejemplo
Supongamos que has desarrollado un modelo para predecir los precios de casas. El MAPE se enfoca en cuán cerca están las predicciones de tu modelo de los valores reales en términos porcentuales.

Para calcular el MAPE, primero calculas el error absoluto porcentual para cada predicción, que es la diferencia absoluta entre la predicción y el valor real dividida por el valor real, y luego calculas el promedio de estos errores porcentuales.



#### Interpretación
Un MAPE de 10% significa que, en promedio, las predicciones de tu modelo se desvían en un 10% de los valores reales. Esto indica que las predicciones tienden a estar en promedio dentro del 10% de diferencia de los valores reales.

Un MAPE más bajo indica una mayor precisión relativa de las predicciones, mientras que un MAPE más alto sugiere que las predicciones tienden a tener mayores desviaciones porcentuales de los valores reales.

En resumen, el MAPE te proporciona una medida porcentual de qué tan precisas son las predicciones de tu modelo en comparación con los valores reales. Es útil para comprender la magnitud relativa de los errores y puede ser especialmente importante en situaciones donde la precisión en términos porcentuales es crucial.


#### ¿Cuándo usarlo?
El MAPE es útil cuando deseas calcular el error porcentual promedio entre las predicciones y los valores reales. Es especialmente útil cuando los errores porcentuales son más informativos que los errores absolutos.

Por ejemplo, en la predicción de la demanda de productos en una tienda, el MAPE puede medir cuánto difieren las estimaciones de ventas en términos porcentuales.