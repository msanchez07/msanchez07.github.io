# Clasificador multiclase
Un clasificador multiclase se distingue por ser un modelo de aprendizaje automático diseñado para abordar problemas de clasificación que involucran tres o más clases distintas. En contraste con los clasificadores binarios, que se centran en distinguir entre dos categorías, los clasificadores multiclase son esenciales para aplicaciones que requieren la asignación de instancias a múltiples categorías exclusivas. Este tipo de modelos desempeñan un papel crucial en una amplia gama de tareas, desde el reconocimiento de dígitos escritos a mano hasta la clasificación de imágenes, el etiquetado de documentos y otros escenarios donde las clases no se limitan a dos opciones.

La tarea principal de un clasificador multiclase implica aprender patrones y características complejas que le permitan diferenciar entre varias clases en función de ejemplos previamente etiquetados. Durante el proceso de entrenamiento, el clasificador ajusta sus parámetros internos para optimizar su capacidad de generalización a nuevos datos no vistos. 

La elección del algoritmo de clasificación en un contexto multiclase puede variar y dependerá de las características del conjunto de datos y de la naturaleza específica del problema. 

A continuación veremos las distintas técnicas para entrenar modelos multiclase, los cuales se basan en los clasificadores binarios.


## OvR
Una de las estrategias que podemos seguir es la **OvR, también conocida como "One-vs-All" o "One-against-All"**. Esta estrategia entrena un clasificador binario para cada clase en el conjunto de datos. Cada clasificador permite distinguir una clase específica de las demás, considerando esa clase como la positiva y agrupando todas las demás clases como la clase negativa. 

Por ejemplo, dado un problema de clasificación de clases múltiples con ejemplos para cada clase 'morado ', 'azul', 'naranja' y 'verde'. Esto podría dividirse en cuatro conjuntos de datos de clasificación binaria de la siguiente manera:

- Problema de clasificación binaria 1 : morado versus [naranja, verde, azul]
- Problema de clasificación binaria 2 : verde vs [azul, naranja, morado]
- Problema de clasificación binaria 3 : azul vs [verde, morado, naranja]
- Problema de clasificación binaria 4 : naranja vs [morado, azul, verde]

</br>

```{image} ../../../images/sistemas_supervisados/clasificacion/07.png
:class: bg-primary
:align: center
:width: 35%
```

</br>

Durante la predicción, se selecciona la clase con la mayor puntuación entre todos los clasificadores. 

Una posible desventaja de este enfoque es que requiere la creación de un modelo para cada clase. Por ejemplo, tres clases requieren tres modelos. Esto podría ser un problema para conjuntos de datos grandes (por ejemplo, millones de filas), modelos lentos (por ejemplo, redes neuronales) o números muy grandes de clases (por ejemplo, cientos de clases).


## OvO
Otra estrategia que podemos seguir es la **OvO, tambié conocida como "One vs One"**, donde se entrena un clasificador binario para cada par único de clases. Es decir, si hay *N*  clases se entrenan $\frac{N*(N-1)}{2}$  clasificadores. 

Cada clasificador OvO se entrena solo con datos pertenecientes a las dos clases que está tratando de distinguir. 

Por ejemplo, considera un problema de clasificación de clases múltiples con cuatro clases: 'morado ', 'azul', 'naranja' y 'verde'. Esto podría dividirse en seis conjuntos de datos de clasificación binaria de la siguiente manera:

- Problema de clasificación binaria 1 : morado versus naranja
- Problema de clasificación binaria 2 : morado versus verde
- Problema de clasificación binaria 3 : morado versus azul
- Problema de clasificación binaria 4 : azul versus verde
- Problema de clasificación binaria 5 : azul versus naranja
- Problema de clasificación binaria 6 : verde versus naranja

</br>

```{image} ../../../images/sistemas_supervisados/clasificacion/08.png
:class: bg-primary
:align: center
:width: 30%
```

</br>

Durante la predicción, cada clasificador vota por la clase que cree que es correcta, y la clase que recibe más votos se elige como la predicción final. 

Aunque puede ser más costoso computacionalmente, OvO es útil cuando los clasificadores binarios son eficientes y el conjunto de datos es grande. 


## Entrenar modelo
La elección entre OvR y OvO depende de varios factores, como el tamaño del conjunto de datos, la eficiencia computacional y el rendimiento deseado. En la práctica, algunos algoritmos, como Support Vector Machines (SVM), son inherentemente OvO, mientras que otros, como Regresión Logística Multinomial, pueden implementarse de manera eficiente como OvR.

Scikit-Learn detecta cuando intenta utilizar un algoritmo de clasificación binaria para una tarea de clasificación multiclase y ejecuta automáticamente OvR u OvO, según el algoritmo. Vamos a ver un ejemplo con una SVC:

```{code}
from sklearn.svm import SVC

svm_clf = SVC(random_state=42)
svm_clf.fit(X_train[:2000], y_train[:2000]) 
svm_clf.predict([some_digit])
```

```raw
array(['3'], dtype=object)
```

¡Vaya, parece que predice de manera correcta! El código entrena un SVC utilizando las clases originales del 0 al 9 (y_train), en lugar de las clases relacionadas con el 3 frente al resto (y_train_3). Debido a que hay 10 clases en total (es decir, más de 2), Scikit-Learn aplicó la estrategia One-vs-One (OvO), lo que implicó el entrenamiento de 45 clasificadores binarios distintos. 

De hecho, vamos a ver los puntuajes de las clasificaciones por cada una de las clases (0, 9):

```{code}
some_digit_scores = svm_clf.decision_function([some_digit])
some_digit_scores.round(2)
```
```raw
array([[ 3.8 , -0.29,  7.24,  9.31,  2.73,  6.25,  0.71,  1.72,  8.29, 5.1 ]])
```

Como podemos observar, la clase que mas puntuaje tiene es la correspondiente al número 3, lo cual podemos comprobar de la siguiente manera:

```{code}
class_id = some_digit_scores.argmax()
class_id
```
```raw
3
```

Al entrenar un clasificador se almacena una lista de las clases objetivo en `classes_`, y en el caso de MNIST estas son 10:

```{code}
svm_clf.classes_
```

```raw
array(['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'], dtype=object)
```

y si accedemos a la clase objetivo nos devuelve la que estamos intentando predecir:

```{code}
svm_clf.classes_[class_id]

```

```raw
'3'
```

Hay que tener en cuenta que podemos forzar a scikit-learn a utilizar la estrategia que nosotros queramos, OvO o OvR. Para ello, contamos con las clases `OneVsOneClassifiero` o `OneVsRestClassifier`. Vamos a ver un ejemplo de esto:

```{code}
from sklearn.multiclass import OneVsRestClassifier

ovr_clf = OneVsRestClassifier(SVC(random_state=42))
ovr_clf.fit(X_train[:2000], y_train[:2000])
```

vamos a realizar una predicción con nuestro clasificador entrenado:

```
ovr_clf.predict([some_digit])
```

```raw
array(['3'], dtype='<U1')
```

ahora podemos obtener cuantos clasificadores se han entrenado:

```{code}
len(ovr_clf.estimators_)
```

```raw
10
```

```{admonition} Nota
Hay algunos modelos que funcionan mejor con la clasificación binaria y otros que funcionan mejor con la clasificación multiclase. 
```