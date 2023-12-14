# Curva ROC
La Curva ROC (Receiver Operating Characteristic) es una herramienta fundamental en la evaluación de modelos de clasificación en el ámbito del aprendizaje automático y la estadística. Esta curva proporciona una representación gráfica de la capacidad de un modelo para discriminar entre dos clases, generalmente la positiva y la negativa. Su origen se remonta al ámbito militar y la detección de señales, pero ha encontrado una aplicación significativa en la evaluación de algoritmos de clasificación en diversos campos.

En su esencia, la Curva ROC ilustra **la relación entre la tasa de verdaderos positivos (sensibilidad) y la tasa de falsos positivos**, proporcionando un marco visual para comprender cómo varía el rendimiento del modelo a medida que se ajusta su umbral de decisión. Cuanto más se acerque la curva ROC al área bajo la curva (AUC) de 1.0, mejor será la capacidad del modelo para discriminar entre las clases, mientras que una curva diagonal (AUC de 0.5) indica un rendimiento similar al azar.

```{image} ../../../images/sistemas_supervisados/clasificacion/05.png
:class: bg-primary
:align: center
:width: 65%
```
</br>

Una de las ventajas clave de la Curva ROC es su independencia de umbrales específicos, lo que la hace particularmente valiosa en situaciones donde la distribución de clases o los costos asociados con los errores de clasificación pueden variar. Además, la Curva ROC proporciona una forma intuitiva de comparar el rendimiento de diferentes modelos, ya que un modelo con una curva ROC más alejada de la diagonal generalmente se considera más efectivo.

En la práctica, la interpretación de la Curva ROC y su área bajo la curva no solo ofrece información sobre la capacidad de clasificación del modelo, sino que también permite a los practicantes ajustar sus modelos según las necesidades específicas de la aplicación. 

## Calcular curva ROC
Para calcular la curva ROC En scikit-learn, puedes utilizar la función roc_curve y visualizarla utilizando la biblioteca matplotlib. Vamos a ver esto en nuestro ejemplo:

```{code}
from sklearn.metrics import roc_curve, auc

fpr, tpr, thresholds = roc_curve(y_test_3, y_pred)
roc_auc = auc(fpr, tpr)

# Visualizar la Curva ROC
plt.figure(figsize=(8, 6))
plt.plot(fpr, tpr, color='darkorange', lw=2, label=f'AUC = {roc_auc:.2f}')
plt.plot([0, 1], [0, 1], color='navy', lw=2, linestyle='--')
plt.xlabel('Tasa de Falsos Positivos (FPR)')
plt.ylabel('Tasa de Verdaderos Positivos (TPR)')
plt.title('Curva ROC')
plt.legend(loc='lower right')
plt.show()
```

```{image} ../../../images/sistemas_supervisados/clasificacion/06.png
:class: bg-primary
:align: center
:width: 65%
```

</br>

La Curva ROC representa la relación entre la **Tasa de Verdaderos Positivos** (TPR o Sensibilidad) en el eje **y** y la **Tasa de Falsos Positivos** (FPR) en el eje **x**. Cada punto en la curva corresponde a un umbral de decisión diferente. Es decir, la línea muestra cómo cambia la capacidad del modelo para acertar cuando ajustamos el umbral para decidir qué es "sí" y qué es "no". Se compara cuántas cosas "sí" acierta con cuántas veces se equivoca al decir "sí" cuando debería ser "no" .

El **caso ideal en la curva ROC es el (0,1)**, donde la TPR es 1 (todos los positivos se clasifican correctamente) y el FPR es 0 (no hay falsos positivos). Si la curva fuera perfecta, estaría en la esquina superior izquierda, donde acierta todo lo que debería y no se equivoca en nada.

Por otro lado, **la línea diagonal desde (0,0) a (1,1)** representa el rendimiento de un clasificador aleatorio. Un clasificador que simplemente adivina al azar tendría una curva ROC que sigue esta línea. Si nuestro modelo está por encima de esta línea, está haciendo algo útil.

Otro factor a tener en cuenta es el AUC, que **mide el área bajo la Curva ROC** y proporciona una única métrica resumen del rendimiento del modelo. Un AUC de 1.0 indica un rendimiento perfecto, mientras que un AUC de 0.5 sugiere un rendimiento similar al azar. Puedes utilizar el AUC para comparar el rendimiento relativo de diferentes modelos de clasificación. Un modelo con un AUC más alto generalmente se considera mejor en términos de discriminación entre las clases.

Si queremos medir el rendimiento del modelo, hay que tener en cuenta que **cuanto más arriba y a la izquierda esté la curva, mejor**. Eso significa que el modelo es bueno para distinguir entre las cosas que estamos buscando y las que no.

Eso si, debes tener en cuenta que la curva no nos dice exactamente dónde poner el límite para decir "sí" o "no". Eso depende de lo que sea más importante para nosotros: ¿Queremos estar seguros de acertar todo, incluso si a veces decimos "sí" cuando deberíamos decir "no", o estamos bien con algunos errores si generalmente acertamos?

