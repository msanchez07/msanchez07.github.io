# Error Absoluto Medio (MAE)	
El Error Absoluto Medio (MAE) es una medida que te ayuda a entender cuán lejos están, en promedio, las predicciones de un modelo con respecto a los valores reales. Para comprenderlo mejor en el contexto de la predicción de precios de casas, como mencionamos anteriormente, consideremos cómo funciona el MAE en este caso.

$$MAE = \sqrt{\sum_{i=1}^{n}\frac{|y_{1}-ŷ_{i})|}{n}}$$


#### Ejemplo
Vamos a ver el cálculo del MAE con el ejemplo de las casas. Después de hacer predicciones para varios casos, calculas la diferencia absoluta entre cada predicción y su valor real:

Casa 1: Predicción = 180.000, Valor Real = 200.000, Diferencia Absoluta = 20.000
Casa 2: Predicción = 240.000, Valor Real = 250.000, Diferencia Absoluta = 10.000
Casa 3: Predicción = 200.000, Valor Real = 180.000, Diferencia Absoluta = 20.000
Casa 4: Predicción = 280.000, Valor Real = 300.000, Diferencia Absoluta = 20.000
Casa 5: Predicción = 230.000, Valor Real = 220.000, Diferencia Absoluta = 10.000

Para calcular el MAE, sumas todas las diferencias absolutas y las divides por el número total de predicciones:

MAE = (20.000 + 10.000 + 20.000 + 20.000 + 10.000) / 5 = 16.000


#### Interpretación
El MAE nos proporciona una perspectiva de cuán cerca o lejos están, en promedio, las predicciones de nuestro modelo de los valores reales. En este caso, un MAE de 16.000 dólares significa que, en promedio, nuestras predicciones se desvían por alrededor de 16.000 dólares del precio real de las casas.

El MAE es una medida directa y fácil de entender. Cuanto menor sea el valor del MAE, más cerca estarán las predicciones del modelo de los valores reales, lo que indica un mejor ajuste y un rendimiento más preciso en la predicción de precios de las casas.


#### ¿Cuándo usarlo?
Utiliza el MAE cuando necesites calcular el promedio de las diferencias absolutas entre las predicciones y los valores reales. Es apropiado cuando todos los errores, ya sean positivos o negativos, tienen la misma importancia.

Por ejemplo, en un problema de regresión para predecir el tiempo de entrega de paquetes, el MAE puede medir cuánto se desvían tus estimaciones de tiempo de entrega en minutos.