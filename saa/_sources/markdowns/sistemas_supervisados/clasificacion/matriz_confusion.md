
# Matriz de confusión
La matriz de confusión es una herramienta esencial en el campo de la evaluación de modelos de clasificación en aprendizaje automático. Se trata de una tabla que permite visualizar y analizar el rendimiento de un modelo al comparar sus predicciones con las clases reales de un conjunto de datos. Esta matriz organiza la información en cuatro cuadrantes: verdaderos positivos (VP), verdaderos negativos (VN), falsos positivos (FP) y falsos negativos (FN). Cada uno de estos elementos proporciona información valiosa sobre la capacidad del modelo para clasificar correctamente las instancias de cada clase.


```{image} ../../../images/sistemas_supervisados/clasificacion/03.png
:class: bg-primary
:align: center
:width: 55%
```

</br>

En el cuadrante de verdaderos positivos, se encuentran las instancias correctamente clasificadas como positivas por el modelo. Los verdaderos negativos representan las instancias correctamente clasificadas como negativas. Por otro lado, los falsos positivos son instancias que el modelo clasifica incorrectamente como positivas, mientras que los falsos negativos son instancias que deberían ser positivas pero son clasificadas incorrectamente como negativas. Estos elementos permiten evaluar aspectos como la precisión, sensibilidad y especificidad del modelo, proporcionando una visión más completa de su rendimiento.

La interpretación de la matriz de confusión es crucial para comprender las fortalezas y debilidades del modelo, así como para ajustar y mejorar su rendimiento. Además, a partir de la matriz de confusión, se derivan métricas importantes como la precisión, la sensibilidad (recall) y la especificidad, que son fundamentales para evaluar la eficacia de un modelo en la tarea de clasificación. 

## Como obtener la matriz de confusión
Para obtener la matriz de confusión, primero, debes entrenar tu modelo de aprendizaje automático utilizando el conjunto de datos, en este caso MNIST. Como ya hemos indicado antes, vamos a utilizar un árbol de decisión para este proposito. Después de entrenar tu modelo, utiliza conjuntos de datos separados (por ejemplo, conjunto de validación o prueba) para hacer predicciones. Estas predicciones serán comparadas con las etiquetas reales para evaluar el rendimiento del modelo.

```{code}
from sklearn.metrics import confusion_matrix
import numpy as np

cm = confusion_matrix(y_test_3, y_pred)
cm
```

```raw
  array([[8784,  206]
         [ 152,  858]])
```


También puedes visualizar esta matriz para obtener una comprensión más clara del rendimiento del modelo. Esto te ayudará a identificar qué dígitos se clasifican correctamente y cuáles pueden ser fuente de confusión para el modelo.

```{code}
import seaborn as sns
import matplotlib.pyplot as plt

sns.heatmap(cm, annot=True, fmt='d', cmap='Blues', xticklabels=np.unique(y_test_3), yticklabels=np.unique(y_test_3))
plt.xlabel('Predicciones')
plt.ylabel('Etiquetas Reales')
plt.show()
```

```{image} ../../../images/sistemas_supervisados/clasificacion/04.png
:class: bg-primary
:align: center
:width: 65%
```

</br>

Cada fila de una matriz de confusión representa una clase real , mientras que cada columna representa una clase prevista .La primera fila de esta matriz considera imágenes no 3 (la clase negativa ): 8784 de ellas fueron clasificadas correctamente como no 3 (se llaman verdaderos negativos ), mientras que las 206 restantes fueron clasificadas erróneamente como 3 ( falsos positivos , también llamados errores tipo I ).La segunda fila considera las imágenes de 3 (la clase positiva ): 152 fueron clasificadas erróneamente como no 3 ( falsos negativos , también llamados errores de tipo II ), mientras que las 858 restantes fueron clasificadas correctamente como 3 ( verdaderos positivos ). Un clasificador perfecto solo tendría verdaderos positivos y verdaderos negativos, por lo que tu matriz de confusión tendría valores distintos de cero solo en su diagonal principal (de arriba a la izquierda a abajo a la derecha).

La matriz de confusión brinda mucha información, pero a veces es posible que prefieras una métrica más concisa. Para esto podemos usar la precisión, que  es una métrica comúnmente derivada de la matriz de confusión y se define como la proporción de predicciones correctas (verdaderos positivos y verdaderos negativos) respecto al total de predicciones. Puedes calcular la precisión utilizando la fórmula:


$$precision=\frac{VP+VN}{TI}$$

donde:

- **VP**: Verdaderos positivos.
- **VN**: Verdaderos negativos.
- **TI**: Total de instancias.

El siguiente código calcula la precisión de nuestro modelo:

```{code}
from sklearn.metrics import precision_score

precision_score(y_test_3, y_pred)

```

```raw
0.806390977443609
```

Vaya, parece que tenemos una precisión bastante buena pero recuerda que la precisión por sí sola puede no ser suficiente para evaluar completamente el rendimiento del modelo, especialmente en conjuntos de datos desbalanceados. Puedes considerar otras métricas como la sensibilidad (recall), la especificidad y la F1-score para obtener una evaluación más completa.

## Sensibilidad
La sensibilidad, también conocida como recall o tasa de verdaderos positivos, es una métrica que mide la proporción de instancias positivas reales que fueron correctamente identificadas por el modelo. Se calcula utilizando la fórmula:

$$recall=\frac{VP}{VP + FN}$$

donde:

- **VP**: Verdaderos positivos.
- **FN**: Falsos negativos.

El siguiente código utiliza la función recall_score de scikit-learn para calcular la sensibilidad directamente:

```{code}
from sklearn.metrics import recall_score

recall_score(y_test_3, y_pred)

```

```raw
0.8495049504950495
```


La sensibilidad es especialmente útil en situaciones donde identificar positivos verdaderos es crítico y los falsos negativos son costosos o tienen un impacto significativo en el problema en cuestión.

## F1
La puntuación F1, también conocida como medida F1 o F1-score, es una métrica que combina tanto la precisión como la sensibilidad (recall) en una sola métrica. Se calcula utilizando la fórmula:

$$especificidad=2*\frac{Precision * Sensibilidad}{Precision + Sensibilidad}$$

Para calcular esto podemos usar sickit-learn:

```{code}
from sklearn.metrics import f1_score

f1_score(y_test_3, y_pred)
```

```raw
0.8273866923818707
```

La puntuación F1 es especialmente útil cuando hay un desequilibrio en las clases y se desea tener en cuenta tanto la precisión como la sensibilidad en la evaluación del modelo.

## Cuando usar cada métrica
La elección entre precision, recall y la puntuación F1 depende del contexto específico del problema y de las implicaciones prácticas de los errores de clasificación en tu aplicación. Aquí hay algunas consideraciones generales:

<table class="table table-bordered my-table-border">
  <thead>
    <tr class="my-table-header">
      <th class="text-center my-table-header" colspan="4">MÉTRICAS DE EVALUACIÓN DE LA MATRIZ DE CONFUSIÓN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th class="left-header" scope="row">Precision</th>
      <td  colspan="3">La precision es útil cuando los falsos positivos son costosos o tienen consecuencias significativas. Por ejemplo, en un sistema de detección de spam, podrías priorizar la precision para asegurarte de que los correos electrónicos clasificados como "no spam" realmente no lo sean.</td>
    </tr>
     <tr>
      <th class="left-header" scope="row">Recall (Sensibilidad)</th>
      <td  colspan="3"> El recall es importante cuando los falsos negativos son costosos o críticos. Por ejemplo, en un sistema de diagnóstico médico, querrías maximizar el recall para garantizar que no se pierda ninguna instancia positiva, aunque esto pueda resultar en algunos falsos positivos.</td>
    </tr>
    <tr>
      <th class="left-header" scope="row">Puntuación F1</th>
      <td  colspan="3">La puntuación F1 es útil cuando buscas un equilibrio entre precision y recall. Si tanto los falsos positivos como los falsos negativos son importantes en tu aplicación, y deseas encontrar un punto medio, la puntuación F1 es una métrica balanceada. También lo puedes usar para comparar modelos de clasificación.</td>
    </tr>
  </tbody>
</table>



