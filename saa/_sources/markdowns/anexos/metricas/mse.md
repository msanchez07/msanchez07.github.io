# Error Cuadrático Medio (MSE)
El Error Cuadrático Medio (MSE) es una métrica utilizada para evaluar el rendimiento de modelos de regresión. Es especialmente útil para medir cuán cerca están las predicciones del modelo de los valores reales en un conjunto de datos. Este viene dado por la siguiente fórmula: 

$$MSE = \sum_{i=1}^{n}\frac{(y_{1}-ŷ_{i})²}{n}$$

Donde: 
-  **n** es el número total de observaciones en el conjunto de datos. 
- **$y_{i}$** representa el valor real de la observación i. 
- **$ŷ_{i}$** representa el valor predicho por el modelo para la observación i. 
- **Σ** denota la suma, es decir, debes calcular la suma de los cuadrados de las diferencias entre los valores reales y los valores predichos para todas las observaciones y luego dividirla por n.

El MSE mide la magnitud promedio de los errores (diferencias) entre las predicciones hechas por el modelo y los valores reales en el conjunto de datos de prueba. Cuanto menor sea el valor del MSE, mejor será el ajuste del modelo a los datos. Aquí hay algunas interpretaciones clave:

- **Mayor MSE significa mayor error**: Un MSE alto indica que el modelo tiene un error promedio significativamente grande en sus predicciones. En otras palabras, el modelo no se ajusta bien a los datos reales.

- **MSE igual a cero**: Si el MSE es cero, significa que el modelo hace predicciones perfectas que coinciden exactamente con los valores reales. Esto es raro en la práctica y a menudo indica un posible sobreajuste (overfitting) al conjunto de datos de entrenamiento.

- **Comparación de modelos**: El MSE se utiliza comúnmente para comparar varios modelos de regresión. Entre dos modelos, el que tenga un MSE más bajo se considera generalmente mejor en términos de su capacidad para hacer predicciones precisas.

- **Magnitud en unidades originales**: La magnitud del MSE está en las unidades originales del problema. Por ejemplo, si se está trabajando en la predicción de precios de viviendas en dólares, el MSE se medirá en dólares al cuadrado.

- **Sensible a valores atípicos**: El MSE es sensible a valores atípicos en los datos, ya que los errores se elevan al cuadrado. Esto significa que un solo valor atípico puede aumentar significativamente el MSE.


#### Ejemplo
Vamos a partir de la base del ejemplo explicado anteriormente para ver como calcular este error. Primero se debe calcular las diferencias entre las predicciones y los valores reales para cada casa:

Diferencias al cuadrado: (200.000 – 180.000)², (250.000 – 240.000)², (180.000 – 200.000)², (300.000 – 280.000)², (220.000 – 230.000)²

Posteriormente se debe calcular el promedio de estas diferencias al cuadrado:

Promedio = (400.000.000 + 100.000.000 + 400.000.000 + 400.000.000 + 100.000.000) / 5 = 280.000.000

El MSE es el promedio calculado:

MSE = 280.000.000

En este ejemplo, el MSE sería 280.000.000, lo que significa que, en promedio, las predicciones de tu modelo están a una distancia de 280.000.000 unidades al cuadrado de los valores reales de los precios de las casas.


#### ¿Cuándo usarlo?
Emplea el MSE cuando necesites calcular el promedio de las diferencias al cuadrado entre las predicciones y los valores reales. Es útil cuando deseas penalizar más los errores grandes.

Por ejemplo, en la predicción de la temperatura diaria, el MSE mide cuánto se desvían tus predicciones en términos de grados cuadrados.