# Análisis exploratorio de datos 
Un elemento fundamental para que nuestro modelo tenga éxito, es el análisis exploratorio de datos (EDA, por sus siglas en inglés). Imagina que los datos son el mapa de un territorio desconocido, y el EDA es la brújula que te guía a través de él.  

El análisis exploratorio de datos es como desempacar un regalo; revela información valiosa que puede no ser evidente a simple vista. A menudo, los datos contienen patrones, relaciones y tendencias que pueden inspirar decisiones informadas y la creación de modelos más precisos. En este capítulo, exploraremos cómo el EDA es una fase crucial en el flujo de trabajo de aprendizaje automático, ya que puede influir en las decisiones que tomamos durante todo el proceso. 

En este apartado, descubriremos cómo examinar y visualizar datos, identificar valores atípicos, comprender la distribución de los atributos y descubrir posibles correlaciones. Veremos cómo las herramientas y técnicas del análisis exploratorio de datos se convierten en tu compañero de confianza en el camino hacia la creación de modelos exitosos. 

El análisis exploratorio de datos es el primer paso para desentrañar los secretos que los datos almacenan, y este capítulo te guiará a través de todo el proceso. ¡Comencemos a explorar y a desenterrar los tesoros ocultos en tus datos! 

## Importancia del EDA en el aprendizaje automático
El proceso de aprendizaje automático se basa en extraer patrones y relaciones de los datos, para luego aplicar estos patrones en nuevos datos para hacer predicciones. Sin embargo, este proceso no puede ser exitoso si no entendemos adecuadamente los datos que alimentamos a nuestros modelos. Aquí es donde entra en juego el EDA.

El EDA nos permite familiarizarnos con los datos a un nivel profundo. Esto implica explorar las características y atributos presentes en los datos, comprender su significado y entender su rango y distribución. Esta familiaridad nos proporciona información esencial para tomar decisiones informadas sobre cómo diseñar y ajustar nuestros modelos.

A menudo, los datos contienen patrones, tendencias y correlaciones que no son evidentes a simple vista. El EDA nos permite descubrir estos patrones ocultos, lo que puede influir en las decisiones sobre qué características son relevantes para el modelo y cómo se deben transformar o normalizar los datos.

Otros elementos a tener en cuenta son los valores atípicos y el ruido. Estos elementos pueden tener un impacto significativo en la calidad y la precisión de nuestros modelos. El EDA nos ayuda a identificar estos valores atípicos y el ruido, lo que permite tomar medidas para manejarlos adecuadamente, ya sea eliminándolos, transformándolos o realizando imputaciones.

Además de todo esto, el EDA también es útil para seleccionar y extraer características relevantes para la construcción del modelo. Al comprender la correlación y la importancia de diferentes atributos, podemos tomar decisiones informadas sobre cuáles incluir en el modelo y cuáles excluir.
Finalmente, al explorar y comprender los datos, podemos identificar posibles fuentes de sesgo y errores. Esto es crucial para garantizar que nuestro modelo no esté basado en datos sesgados y que pueda generalizar de manera efectiva a nuevos datos.

En resumen, el Análisis Exploratorio de Datos es el cimiento sobre el cual se construye todo el proceso de aprendizaje automático. Al comprender los datos, identificar patrones y tomar decisiones informadas sobre cómo preprocesarlos, el EDA garantiza que los modelos resultantes sean más precisos, generalizables y confiables. Es la puerta de entrada al mundo complejo pero emocionante del aprendizaje automático y un paso que no debe subestimarse. En los siguientes apartados, exploraremos cómo llevar a cabo un EDA efectivo y cómo sus resultados influirán en el éxito de nuestros modelos.

## Un primer vistazo a los datos
La calidad de los resultados del EDA depende en gran medida de la calidad de los datos con los que trabajamos. Para poder desarrollar los conceptos de este capítulo, vamos a contar con el conjunto de datos proporcionado por el DataSet Medical Cost Personal DataSets1. Este DataSet cuenta con 1338 filas y 8 columnas, las cuales se describen en la siguiente tabla:

| Columna | Definición | Tipo de datos | Ejemplos | Números nulos |
| ------------ | ------------- | ------------ | ------------- | ------------ |
| No         | Número de la columna | Number | 22, 35, 48 | 0 |
| Age | Edad del beneficiario. | Número | 22.0, 33.0, 32.0 | 29 |
| Sex | Género del beneficiario. | Texto | Male, Female | 86 | 
| Bmi | Índice de masa corporal | Número | 11, 20, 31 | 98 | 
| Children | Número de hijos cubiertos por el seguro | Número | 0.0, 1.0, 3.0 | 82 | 
| Smoker | Indica si el asegurado fuma | Texto | Yes, no | 48 | 
| Region | Zona de E.E.U.U. donde habita el beneficiario. | Texto | Southwest, southeast | 121 | 
| **Charges** | **Prima del seguro** | **Número** | **16884.92400, 1725.55230** | **55**

La columna o variable en negrita es nuestra variable objetivo, es decir, el valor que queremos predecir mediante nuestro modelo. Muchos de los análisis y cálculos que se van a desarrollar estarán centralizados en esta variable.

```{admonition} Nota
:class: note
En el capítulo anterior listamos un gran número de herramientas y plataformas para resolver problemas de aprendizaje automático. Todas estas herramientas y plataformas pueden utilizarse para resolver problemas de aprendizaje supervisado, pero nosotros nos vamos a centrar en Scikit-learn, Matplotlib, Seaborn, Pandas y Numpy.
```