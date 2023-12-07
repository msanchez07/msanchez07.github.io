---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: ipython3
  language: python
  name: python3
---

# Estandarizar y normalizar
La estandarización y normalización son prácticas fundamentales que permiten mejorar la eficacia y la interpretación de los modelos. Estos procesos son esenciales para garantizar que los datos utilizados en los modelos estadísticos, algoritmos de aprendizaje automático o cualquier otra aplicación analítica estén en una escala coherente y comparable.

Por ejemplo, supongamos que tienes un conjunto de datos con dos características, la edad de las personas en años y sus ingresos anuales en miles de dólares. Estos dos atributos tienen magnitudes muy diferentes, y podrían afectar la capacidad de ciertos algoritmos para aprender patrones efectivamente. 

La estandarización implica **ajustar los datos para que tengan una media de cero** y una **desviación estándar de uno**, mientras que la normalización generalmente se refiere a **escalar los datos en un rango específico, como [0, 1]**. Ambos métodos son esenciales para mitigar problemas derivados de las diferencias en la escala y la variabilidad de los datos, lo que puede afectar negativamente el rendimiento de los modelos.

La importancia de estos procesos repercute en la obtención de resultados más consistentes, interpretación más clara de los resultados y, en última instancia, modelos más robustos y efectivos. 

## Estandarización de los datos
La estandarización de datos es un proceso fundamental en el análisis de datos y el desarrollo de modelos estadísticos y de aprendizaje automático. Consiste en ajustar los valores de las variables para que sigan una escala común, generalmente centrándolos en una media de cero y escalándolos de acuerdo con su desviación estándar. Este proceso tiene como objetivo principal eliminar las diferencias en la escala de las variables, lo que puede ser crucial para el correcto funcionamiento de muchos algoritmos.

Al estandarizar los datos, se logra que todas las variables tengan una media de cero y una desviación estándar de uno. Este proceso es especialmente relevante cuando las variables de entrada de un modelo tienen unidades y escalas diferentes, ya que ayuda a que el modelo sea más robusto y menos sensible a las variaciones en las magnitudes de las variables.

La estandarización facilita la comparación y la interpretación de los coeficientes en modelos lineales, mejora la convergencia en algoritmos de optimización y puede tener un impacto positivo en la eficacia de muchos algoritmos de aprendizaje automático. En resumen, es un paso crucial para garantizar la consistencia y la fiabilidad de los resultados analíticos.

### Ventajas de estandarizar los datos
La estandarización de datos es un paso importante en el preprocesamiento de datos que tiene varios propósitos y beneficios en el análisis de datos y en la construcción de modelos, especialmente en el contexto de algoritmos de aprendizaje automático. Aquí hay algunas razones clave para realizar la estandarización de datos:

- **Facilita la Comparación**: Al estandarizar datos, todas las variables **tienen la misma escala, lo que facilita la comparación directa entre ellas**. Esto es esencial cuando trabajas con modelos que utilizan medidas de distancia, como k-means o algoritmos basados en gradiente.

- **Mejora la Convergencia**: Muchos algoritmos de optimización, como el descenso de gradiente, **convergen más rápido en datos estandarizados**. La estandarización ayuda a que el algoritmo alcance el mínimo global de manera más eficiente al garantizar que las variables contribuyan de manera equitativa al proceso de optimización.

- **Evita Problemas Numéricos**: Al estandarizar datos, se reducen los **problemas relacionados con la escala de las variables, como la pérdida de precisión numérica o la inestabilidad numérica** en cálculos que involucran números muy grandes o muy pequeños.

- **Interpretación Mejorada**: La estandarización **facilita la interpretación de coeficientes en modelos lineales**. Los coeficientes estandarizados representan el cambio en la variable de respuesta en unidades de desviación estándar, lo que hace que la interpretación sea más intuitiva y comparable entre diferentes variables.

- **Robustez del Modelo**: La estandarización puede hacer que **los modelos sean más robustos a las variaciones en la escala y la distribución de los datos**. Esto significa que el modelo puede **generalizar mejor a datos nuevos y desconocidos**.

- **Previene el Sesgo por Escala**: Algunos algoritmos pueden verse afectados por diferencias en la escala de las variables, dando más peso a las variables con magnitudes más grandes. La estandarización **ayuda a evitar este sesgo y a garantizar que todas las variables contribuyan de manera equitativa al modelo**.


### Como estandarizar datos
A continuación se muestra un ejemplo de como estandarizar los datos con los que contamos. Posteriormente, estos datos se mostrarán en una gráfica:

```{code-cell}
import matplotlib.pyplot as plt
from sklearn.preprocessing import StandardScaler
import numpy as np

# Crear datos de ejemplo
np.random.seed(42)
datos_originales = np.random.randn(50, 2) * 5 + 10  # Datos con media 10 y desviación estándar 5

# Inicializar el objeto StandardScaler
scaler = StandardScaler()

# Estandarizar los datos
datos_estandarizados = scaler.fit_transform(datos_originales)

# Crear un gráfico de dispersión para los datos originales
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
plt.scatter(datos_originales[:, 0], datos_originales[:, 1], c='blue', label='Original')
plt.title('Datos Originales')
plt.xlabel('Característica 1')
plt.ylabel('Característica 2')
plt.legend()

# Crear un gráfico de dispersión para los datos estandarizados
plt.subplot(1, 2, 2)
plt.scatter(datos_estandarizados[:, 0], datos_estandarizados[:, 1], c='red', label='Estandarizado')
plt.title('Datos Estandarizados')
plt.xlabel('Característica 1 (Estandarizada)')
plt.ylabel('Característica 2 (Estandarizada)')
plt.legend()

plt.tight_layout()
plt.show()

```

## Normalización de datos
La normalización de datos emerge como una práctica fundamental para transformar las variables en escalas específicas, proporcionando una perspectiva uniforme y comparativa. Este proceso es esencial para mitigar desafíos asociados con disparidades en las magnitudes y rangos de las variables, permitiendo una interpretación más coherente y potenciando el rendimiento de diversos algoritmos y técnicas analíticas.

La normalización se refiere al ajuste sistemático de los valores de las variables para que sigan una escala común, típicamente situándolos dentro de un rango específico, como [0, 1]. Este procedimiento, a menudo crítico en el preprocesamiento de datos, busca eliminar sesgos derivados de diferencias en las unidades o magnitudes de las características, asegurando así una comparación justa y equitativa entre ellas.


### Ventajas de normalizar los datos
La normalización de datos proporciona varias ventajas en el análisis de datos y la construcción de modelos, especialmente en el contexto de algoritmos de aprendizaje automático. Aquí algunas de las ventajas clave:

- **Comparación Justa**: La normalización asegura que todas las variables tengan la misma escala, lo que facilita la comparación directa entre ellas. Esto es crucial cuando se utilizan algoritmos que se basan en medidas de distancia, como k-means o algoritmos basados en gradiente.

- **Mejora de la Convergencia**: Al igual que en la estandarización, la normalización puede mejorar la convergencia de algoritmos de optimización, como el descenso de gradiente. Facilita que el algoritmo alcance el mínimo global de manera más eficiente al garantizar que las variables contribuyan de manera equitativa al proceso de optimización.

- **Evita Problemas Numéricos**: Normalizar los datos ayuda a evitar problemas numéricos asociados con diferencias en la escala de las variables, como la pérdida de precisión numérica o la inestabilidad numérica en cálculos que involucran números muy grandes o muy pequeños.

- **Interpretación Mejorada**: Al igual que con la estandarización, la normalización facilita la interpretación de coeficientes en modelos lineales. Los coeficientes normalizados representan el cambio en la variable de respuesta en unidades específicas, lo que hace que la interpretación sea más intuitiva y comparable entre diferentes variables.

- **Mayor Robustez del Modelo** : La normalización puede hacer que los modelos sean más robustos a las variaciones en la escala y la distribución de los datos. Esto mejora la generalización del modelo a datos nuevos y desconocidos.

- **Previene Sesgo por Escala**: Evita que algunas variables tengan un impacto desproporcionado en modelos que son sensibles a las diferencias en la escala, asegurando que todas las variables contribuyan de manera equitativa.

- **Adecuada para Algoritmos Sensibles a la Escala** : Algunos algoritmos, como las Máquinas de Soporte Vectorial (SVM) y los métodos basados en distancia, pueden beneficiarse significativamente de la normalización, ya que su rendimiento puede depender fuertemente de la escala de las variables.

### Como normalizar datos
A continuación se muestra un ejemplo de como normalizar los datos con los que contamos. Posteriormente, estos datos se mostrarán en una gráfica:

```{code-cell}
import numpy as np
import matplotlib.pyplot as plt
from sklearn.preprocessing import MinMaxScaler
from sklearn.datasets import make_regression

# Generar datos de ejemplo
X, y = make_regression(n_samples=100, n_features=1, noise=10, random_state=42)

# Crear un objeto MinMaxScaler
scaler = MinMaxScaler()

# Ajustar y transformar los datos
X_scaled = scaler.fit_transform(X)

# Visualizar los resultados
plt.figure(figsize=(10, 4))

plt.subplot(1, 2, 1)
plt.scatter(X, y, color='blue')
plt.title('Datos Originales')
plt.xlabel('Característica')
plt.ylabel('Objetivo')

plt.subplot(1, 2, 2)
plt.scatter(X_scaled, y, color='green')
plt.title('Datos Escalados (MinMaxScaler)')
plt.xlabel('Característica (Escalada)')
plt.ylabel('Objetivo')

plt.tight_layout()
plt.show()
```

## Cuando usar estandarización y cuando normalización
La elección entre estandarización y normalización depende del contexto específico de tus datos y del algoritmo o método que estés utilizando. Aquí hay algunas pautas generales:

### Estandarización
La estandarización es especialmente útil cuando **tus datos siguen una distribución normal o se aproximan a ella**. Esto se debe a que la estandarización transforma los datos para que tengan una media de cero y una desviación estándar de uno, lo que es beneficioso para muchos algoritmos que asumen una distribución normal de los datos.

A su vez, la estandarización **es crucial para algoritmos que se basan en medidas de distancia**, como el k-means, o en algoritmos de optimización, como el descenso de gradiente en regresión logística o máquinas de soporte vectorial (SVM).

### Normalización
La normalización es más adecuada cuando los datos **no siguen una distribución normal**. Puedes utilizar métodos como Min-Max para escalar los datos al intervalo [0, 1] o métodos robustos si tus datos contienen valores atípicos.

Además, **si necesitas que tus datos estén en un rango específico y deseas preservar la forma de la distribución original**, la normalización puede ser más apropiada.

Por otro lado, algunos algoritmos, como las redes neuronales, pueden beneficiarse de la normalización, especialmente cuando se utilizan funciones de activación que son sensibles a la escala de las entradas.