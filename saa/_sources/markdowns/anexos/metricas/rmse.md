# Raíz del Error Cuadrático Medio (RMSE)
La Raíz del Error Cuadrático Medio (RMSE) es una métrica que te permite comprender de manera más intuitiva cuán alejadas están las predicciones de un modelo de los valores reales. La fórmula es igual a la del MSE pero añadiendo una raíz cuadrada:

$$RMSE = \sqrt{\sum_{i=1}^{n}\frac{(y_{1}-ŷ_{i})²}{n}}$$



#### Ejemplo
Siguiendo el ejemplo de la predicción de precios de casas, veamos cómo se aplica el RMSE. Luego de hacer las predicciones, calculas el cuadrado de la diferencia entre cada predicción y el valor real:

Casa 1: Predicción = 180.000, Valor Real = 200.000, Diferencia Cuadrada = 20.000² = 400.000.000
Casa 2: Predicción = 240.000, Valor Real = 250.000, Diferencia Cuadrada = 10.000² = 100.000.000
Casa 3: Predicción = 200.000, Valor Real = 180.000, Diferencia Cuadrada = 20.000² = 400.000.000
Casa 4: Predicción = 280.000, Valor Real = 300.000, Diferencia Cuadrada = 20.000² = 400.000.000
Casa 5: Predicción = 230.000, Valor Real = 220.000, Diferencia Cuadrada = 10.000² = 100.000.000

Luego, calculas el promedio de estas diferencias al cuadrado y tomas su raíz cuadrada:

RMSE = √[(400.000.000 + 100.000.000 + 400.000.000 + 400.000.000 + 100.000.000) / 5] = √(280.000.000) ≈ 16.733,20



#### Interpretación
El RMSE te proporciona una medida intuitiva de cuán lejos, en promedio, están las predicciones de tu modelo de los valores reales. En este caso, un RMSE de aproximadamente 16.733,20 dólares significa que, en promedio, las predicciones difieren por alrededor de 16.733,20 dólares del precio real de las casas.

Al utilizar el RMSE, estás evaluando la magnitud promedio de los errores al considerar las diferencias al cuadrado y su raíz cuadrada. Cuanto menor sea el RMSE, más cercanas serán las predicciones del modelo a los valores reales, lo que indica un mejor ajuste y un rendimiento más preciso en la predicción de precios de las casas.


#### ¿Cuándo usarlo?
El RMSE es similar al MSE pero proporciona una medida de error más interpretable en la misma unidad que la variable objetivo. Se utiliza cuando deseas tener una idea más intuitiva de la magnitud de los errores.

Por ejemplo, en la predicción de puntajes en exámenes, el RMSE muestra cuánto se desvían tus predicciones en términos de los puntajes reales.