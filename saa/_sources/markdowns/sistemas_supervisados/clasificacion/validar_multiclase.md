# Validar clasificador multiclase
Anteriormente hemos visto como validar un clasificador binario con la matriz de confusión y la curva ROC. En este punto vamos a ver como validar un clasificador multiclase.

En primer lugar vamos a obtener la matriz de confusión:

```{code}
from sklearn.metrics import ConfusionMatrixDisplay

y_test_pred = svm_clf.predict(X_test)

ConfusionMatrixDisplay.from_predictions(y_test, y_test_pred)
plt.show()
```

```{image} ../../../images/sistemas_supervisados/clasificacion/15.png
:class: bg-primary
:align: center
:width: 65%
```
</br>

Parece que el clasificador funciona bastante bien ya que la diagonal principal es la que más casos está clasificando. No obstante, podemos observar un detalle curioso, y es que los casos de clasificación del número 3 son menores que otros casos, como el 1. Pero, ¿Cuantos casos han fallado? Vamos a ver esto en porcentaje:

```{code}

ConfusionMatrixDisplay.from_predictions(y_test, y_test_pred, normalize="true", values_format=".0%")
plt.show()
```

```{image} ../../../images/sistemas_supervisados/clasificacion/16.png
:class: bg-primary
:align: center
:width: 65%
```
</br>

Como podemos observar, se han clasificado bien un 89% de los casos, la segunda peor marca. Muchas de las imagenes mal clasificadas han sido clasificadas como 5, como podemos ver en la matriz de confusión.

Si queremos ver cuales son los errores que ha cometido el clasificador, podemos generar una matriz de confusión donde esto se resalte para cada una de las clases:

```{code}

sample_weight = (y_test_pred != y_test)
ConfusionMatrixDisplay.from_predictions(y_test, y_test_pred, sample_weight=sample_weight,
normalize="true", values_format=".0%")
```

```{image} ../../../images/sistemas_supervisados/clasificacion/17.png
:class: bg-primary
:align: center
:width: 65%
```
</br>

Ahora podemos ver como el 50% de los errores de la claisificación del número tres es porque se han clasificado como cinco.

