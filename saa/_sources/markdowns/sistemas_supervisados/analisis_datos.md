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


<table class="table table-bordered my-table-border">
  <thead>
    <tr class="my-table-header">
      <th class="text-center my-table-header" colspan="1">Columna</th>
      <th class="text-center my-table-header" colspan="1">Definición</th>
      <th class="text-center my-table-header" colspan="1">Tipo de datos</th>
      <th class="text-center my-table-header" colspan="1">Ejemplos</th>
      <th class="text-center my-table-header" colspan="1">Número de nulos</th>
    </tr>
  </thead>
  <tbody>
    <tr >
      <td colspan="1">No</th>
      <td colspan="1">Número de la columna</td>
      <td colspan="1">Número</th>
      <td colspan="1">22, 35, 48</td>
      <td colspan="1">0</td>
    </tr>
    <tr >
      <td colspan="1">Age</th>
      <td colspan="1">Edad del beneficiario</td>
      <td colspan="1">Número</th>
      <td colspan="1">22.0, 33.0, 32.0</td>
      <td colspan="1">29</td>
    </tr>
    <tr >
      <td colspan="1">Sex</th>
      <td colspan="1">Género del beneficiario</td>
      <td colspan="1">Texto</th>
      <td colspan="1">Male, female</td>
      <td colspan="1">86</td>
    </tr>
    <tr >
      <td colspan="1">Bmi</th>
      <td colspan="1">Índice de masa corporal</td>
      <td colspan="1">Número</th>
      <td colspan="1">11, 20, 31</td>
      <td colspan="1">98</td>
    </tr>
    <tr >
      <td colspan="1">Children</th>
      <td colspan="1">Hijos en el seguro</td>
      <td colspan="1">Número</th>
      <td colspan="1">0.0, 1.0, 3.0</td>
      <td colspan="1">82</td>
    </tr>
    <tr >
      <td colspan="1">Smoker</th>
      <td colspan="1">Fumador</td>
      <td colspan="1">Texto</th>
      <td colspan="1">Yes, no</td>
      <td colspan="1">48</td>
    </tr>
    <tr >
      <td colspan="1">Region</th>
      <td colspan="1">Zona del beneficiario</td>
      <td colspan="1">Texto</th>
      <td colspan="1">Southwest, southeast</td>
      <td colspan="1">121</td>
    </tr>
    <tr class="table-warning">
      <td colspan="1"><strong>Charges</strong></th>
      <td colspan="1"><strong>Prima del seguro</strong></td>
      <td colspan="1"><strong>Número</strong></th>
      <td colspan="1"><strong>16884.92, 1725.55</strong></td>
      <td colspan="1"><strong>55</strong></td>
    </tr>
  </tbody>
</table>


La columna o variable resaltada es nuestra variable objetivo, es decir, el valor que queremos predecir mediante nuestro modelo. Muchos de los análisis y cálculos que se van a desarrollar estarán centralizados en esta variable.

```{admonition} Nota
:class: note
En el capítulo anterior listamos un gran número de herramientas y plataformas para resolver problemas de aprendizaje automático. Todas estas herramientas y plataformas pueden utilizarse para resolver problemas de aprendizaje supervisado, pero nosotros nos vamos a centrar en Scikit-learn, Matplotlib, Seaborn, Pandas y Numpy.
```