---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.15.2
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Pandas
En la era actual, donde la información es abundante y omnipresente, la capacidad de analizar datos se ha convertido en una habilidad fundamental. Desde la toma de decisiones empresariales hasta la comprensión de tendencias sociales, el análisis de datos desempeña un papel crucial en una amplia gama de campos. Dentro de las herramientas de los sistemas de inteligencia artificial, nos adentraremos en el mundo de Pandas, una de las bibliotecas más poderosas y versátiles de Python para el análisis de datos. 

Este capítulo marca el comienzo de un apasionante viaje hacia el entendimiento y la utilización de Pandas para explorar, limpiar y visualizar datos de manera efectiva. A lo largo de estas páginas, aprenderemos cómo aprovechar esta herramienta de código abierto para extraer conocimiento a partir de conjuntos de datos reales, sin importar si se trata de datos financieros, registros climáticos, información de ventas o cualquier otro tipo de información que puedas imaginar. 

Pandas, con su nombre derivado de "Panel Data" y "Python Data Analysis", se ha convertido en una herramienta imprescindible para científicos de datos, analistas y profesionales de diversas disciplinas. Con sus potentes estructuras de datos, herramientas de manipulación y una amplia gama de funciones incorporadas, Pandas facilita la exploración de datos, la limpieza, la agregación y la preparación para el modelado estadístico y el aprendizaje automático. 

En este capítulo, te sumergirás en los conceptos básicos de Pandas y explorarás su funcionalidad esencial. Comenzaremos con la instalación y configuración de Pandas en tu entorno de desarrollo, y luego avanzaremos a través de los componentes clave de esta biblioteca, como Series y DataFrames. Aprenderás a cargar datos desde diversas fuentes, a realizar operaciones de selección y filtrado, a manipular y transformar conjuntos de datos, y a generar visualizaciones para comunicar tus hallazgos de manera efectiva. 

El análisis de datos con Pandas te proporcionará una base sólida en la ciencia de datos, lo que te permitirá abordar problemas reales y tomar decisiones informadas. Prepárate para explorar el mundo de los datos de una manera completamente nueva y emocionante a medida que avanzamos en este viaje hacia el dominio de Pandas y el análisis de datos. ¡Comencemos! 


## Instalacíon y primeros pasos

Antes de comenzar el análisis de datos con Pandas, es esencial asegurarse de que tengas Pandas instalado en tu entorno de desarrollo. Pandas se integra perfectamente en el ecosistema de Python y se puede instalar de manera sencilla utilizando herramientas de gestión de paquetes como pip. Aquí te mostramos cómo hacerlo: 

```
pip3 install pandas
```

Este comando descargará e instalará Pandas y sus dependencias automáticamente. Asegúrate de tener una conexión a Internet activa, ya que pip necesita descargar los paquetes desde el repositorio de Python Package Index (PyPI). 

Una vez que la instalación se haya completado, puedes verificar si Pandas se ha instalado correctamente. Abre una ventana de Python en tu terminal o IDE y ejecuta el siguiente código:

```{code-cell}
import pandas as pd
pd
```

Si no se produce ningún error, significa que Pandas se ha instalado correctamente y está listo para ser utilizado en tu entorno. 

Ahora que has instalado Pandas con éxito, estás preparado para comenzar a explorar el mundo del análisis de datos con esta poderosa biblioteca. En los siguientes apartados de este capítulo, te guiaremos a través de los conceptos básicos y las funciones clave de Pandas para que puedas empezar a trabajar con conjuntos de datos y realizar análisis de datos de manera efectiva.

## Tipos de datos en Pandas 

Pandas ofrece una variedad de tipos de datos que te permiten representar y manipular datos de manera eficiente. A continuación, exploraremos algunos de los tipos de datos más comunes que encontrarás al trabajar con Pandas. 

### [Series](https://pandas.pydata.org/docs/reference/api/pandas.Series.html)

Una Serie es un tipo de datos fundamental en Pandas. Es similar a un array de una dimensión o una columna en una hoja de cálculo. Los elementos de una Serie son homogéneos, es decir, todos los elementos deben ser del mismo tipo de dato. Puedes pensar en una Serie como una estructura de datos que consta de un índice (etiquetas) y una columna de valores asociados. Por ejemplo:

```{code-cell}
import pandas as pd 

data = pd.Series([1, 2, 3, 4, 5])
data 
```

&nbsp;  


![](../images/pandas/01.png)

&nbsp;


Como podemos observar, Pandas establece unos índices por defecto a las columnas de una Serie, pero también podemos indicarlo nosotros en caso de que lo consideremos necesario:

```{code-cell}
import pandas as pd 

data = pd.Series([1, 2, 3, 4, 5], index=["A", "B", "C", "D", "E"]) 
data
```

&nbsp;

![](../images/pandas/02.png)

&nbsp;

Este mismo resultado lo podríamos obtener si creáramos la serie a partir de un diccionario:

```{code-cell}
import pandas as pd 

diccionario = {"A": 1, "B": 2, "C": 3, "D": 4, "E": 5} 
data = pd.Series(diccionario)
data 
```

### Atributos de una serie
Las Series tienen varios atributos que te permiten acceder y manipular los datos contenidos en ellas. A continuación, se muestran algunos de los atributos más comunes de una Series asumiendo que tenemos una Serie llamada s: 

- **s.values**: Este atributo te permite acceder a los valores de la Series. Retorna un array NumPy que contiene los datos de la Serie.
- **s.index**: El atributo index proporciona acceso a los índices de la Serie. Los índices son etiquetas o números enteros que identifican cada elemento en la Serie. 
- **s.dtype**: Devuelve el tipo de datos de los elementos de la Serie. 
- **s.name**: Puedes asignar un nombre a la Serie mediante el atributo name. Esto es útil cuando la Serie forma parte de un DataFrame. 
- **s.shape**: Este atributo retorna una tupla que indica la forma de la Serie. Dado que una Serie es un array unidimensional, la forma será una tupla con un solo valor, que es la longitud de la Serie. 
- **s.size**: El atributo size devuelve el número total de elementos en la Serie. 


### Acceso a los elementos de una serie
Para acceder a los elementos de una serie de pandas en Python, puedes utilizar diferentes métodos y técnicas, dependiendo de lo que necesites hacer. Una serie de pandas es una estructura de datos unidimensional similar a un array o una lista, pero con etiquetas en lugar de índices numéricos. Vamos a ver algunas formas comunes de acceder a los elementos de una serie de pandas. 

<ol>
  <li><strong>Acceso por etiqueta</strong>: Puedes acceder a un elemento específico de la serie utilizando su etiqueta o nombre:
  
  &nbsp;

```{code-cell}
import pandas as pd 
# Crear una serie de ejemplo 

data = {'A': 1, 'B': 2, 'C': 3} 
serie = pd.Series(data) 

# Acceder al elemento con etiqueta 'B' 
elemento = serie['B'] 
print(elemento) 
```

  &nbsp;
  </li>

  <li><strong>Acceso por posición</strong>: También puedes acceder a un elemento por su posición en la serie utilizando índices numéricos:
  
  &nbsp;

```{code-cell}
import pandas as pd 
# Crear una serie de ejemplo 

data = [1, 2, 3] 
serie = pd.Series(data) 

# Acceder al elemento en la posición 1 (segundo elemento) 
elemento = serie[1] 
print(elemento) 
```

  &nbsp;
  </li>

  <li><strong>Acceso a múltiples elementos</strong>: También puedes acceder a varios elementos a la vez especificando una lista de etiquetas o una lista de posiciones:
  
  &nbsp;

```{code-cell}
import pandas as pd 

# Crear una serie de ejemplo 
data = {'A': 1, 'B': 2, 'C': 3} 
serie = pd.Series(data) 


# Acceder a múltiples elementos por etiqueta 
elementos = serie[['A', 'C']] 
print(elementos) 


# Acceder a múltiples elementos por posición 
elementos = serie.iloc[0:2]
print(elementos) 
```

  </li>

</ol>

### Métodos de una serie de Pandas
Una serie de pandas cuenta con varios métodos que facilitan la interacción con sus datos y que nos devuelven una gran cantidad de información útil. A continuación, vamos a listar algunos de estos métodos: 

- **count()**: No acepta parámetros. Devuelve el número de elementos de la serie. 
- **head(n)**: Devuelve las primeras n filas de la serie. El parámetro n es opcional y, de forma predeterminada, es 5. 
- **tail(n)**: Devuelve las últimas n filas de la serie. El parámetro n es opcional y, de forma predeterminada, es 5. 
- **describe(percentiles=None, include=None, exclude=None)**: Calcula estadísticas descriptivas de la serie. Puedes especificar los percentiles, columnas incluidas y columnas excluidas como parámetros opcionales. 
- **mean()**: No acepta parámetros. Calcula la media de los valores en la serie. 
- **sum()**: No acepta parámetros. Calcula la suma de los valores en la serie. 
- **min()**: No acepta parámetros. Encuentra el valor mínimo en la serie. 
- **max()**: No acepta parámetros. Encuentra el valor máximo en la serie. 
- **unique()**: No acepta parámetros. Devuelve una serie de valores únicos en la serie. 
- **nunique(dropna=True)**: Devuelve el número de elementos únicos. Acepta el parámetro dropna, que es un booleano que controla si se deben contar los valores nulos (de forma predeterminada, es True). 
- **value_counts(normalize=False, sort=True, ascending=False, bins=None)**: Cuenta cuantas veces aparece un elemento en una serie. Acepta varios parámetros, como normalize (para obtener frecuencias relativas), sort (para ordenar los resultados), ascending (para controlar el orden ascendente o descendente) y bins (para datos numéricos). 
- **sort_values(ascending=True, inplace=False)**: Ordena los elementos de una serie. Acepta el parámetro ascending (para controlar el orden ascendente o descendente) y inplace (para aplicar la ordenación en el lugar). 
- **idxmax()**: No acepta parámetros. Encuentra la etiqueta (índice) correspondiente al valor máximo en la serie. 
- **idxmin()**: No acepta parámetros. Encuentra la etiqueta (índice) correspondiente al valor mínimo en la serie. 
- **isnull()**: No acepta parámetros. Devuelve una serie booleana que indica qué valores son nulos. 
- **notnull()**: No acepta parámetros. Devuelve una serie booleana que indica qué valores no son nulos. 
- **fillna(value, method=None, axis=None, inplace=False, limit=None, downcast=None)**: Acepta varios parámetros, incluyendo value (el valor para reemplazar los nulos), method (método para propagar valores no nulos), axis (eje a lo largo del cual llenar nulos), inplace (para modificar la serie en su lugar), limit (límite de valores a llenar) y downcast (para reducir el tipo de datos de la serie). 
- **dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)**: Acepta varios parámetros, como axis (eje a lo largo del cual eliminar nulos), how (cómo determinar si se elimina una fila/columna), thresh (número mínimo de valores no nulos requeridos), subset (etiquetas para considerar) e inplace (para modificar la serie en su lugar). 
- **map(arg, na_action=None)**: Acepta una función o un diccionario como arg para aplicar a la serie y un parámetro opcional na_action para controlar cómo se manejan los nulos. 
- **str methods**: Para series que contienen datos de texto, puedes utilizar métodos específicos para manipular cadenas, como str.contains(), str.replace(), y otros. 
- **apply(f)**: Aplica una función a cada elemento de una serie. Devuelve como resultado una nueva serie con los valores producidos por la función. 
- **filter(condición)**: Se utiliza para seleccionar etiquetas de la serie basadas en criterios específicos, como nombres de etiquetas, coincidencias de cadenas o expresiones regulares. Puedes usarla para filtrar y seleccionar subconjuntos de datos de una serie. 

 
Adicionalmente a estos métodos, podemos aplicar operaciones aritméticas a los elementos de una serie, dando como resultado una nueva serie con los elementos producidos tras aplicar estas operaciones.

```{code-cell}
import pandas as pd 

# Crear una serie de ejemplo 
data = [1, 2, 3] 
serie = pd.Series(data) 

serie = serie * 5
print(serie)
```

```{note}
Here is a note
```
