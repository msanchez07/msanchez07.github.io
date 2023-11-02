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

# [Series](https://pandas.pydata.org/docs/reference/api/pandas.Series.html)
Una Serie es un tipo de datos fundamental en Pandas. Es similar a un array de una dimensión o una columna en una hoja de cálculo. Los elementos de una Serie son homogéneos, es decir, todos los elementos deben ser del mismo tipo de dato. Puedes pensar en una Serie como una estructura de datos que consta de un índice (etiquetas) y una columna de valores asociados. Por ejemplo:

```{code-cell}
import pandas as pd 

data = pd.Series([1, 2, 3, 4, 5])
data 
```

&nbsp;  


![](../../../images/pandas/01.png)

&nbsp;


Como podemos observar, Pandas establece unos índices por defecto a las columnas de una Serie, pero también podemos indicarlo nosotros en caso de que lo consideremos necesario:

```{code-cell}
import pandas as pd 

data = pd.Series([1, 2, 3, 4, 5], index=["A", "B", "C", "D", "E"]) 
data
```

&nbsp;

![](../../../images/pandas/02.png)

&nbsp;

Este mismo resultado lo podríamos obtener si creáramos la serie a partir de un diccionario:

```{code-cell}
import pandas as pd 

diccionario = {"A": 1, "B": 2, "C": 3, "D": 4, "E": 5} 
data = pd.Series(diccionario)
data 
```

## Atributos de una serie
Las Series tienen varios atributos que te permiten acceder y manipular los datos contenidos en ellas. A continuación, se muestran algunos de los atributos más comunes de una Series asumiendo que tenemos una Serie llamada s: 

- **s.values**: Este atributo te permite acceder a los valores de la Series. Retorna un array NumPy que contiene los datos de la Serie.
- **s.index**: El atributo index proporciona acceso a los índices de la Serie. Los índices son etiquetas o números enteros que identifican cada elemento en la Serie. 
- **s.dtype**: Devuelve el tipo de datos de los elementos de la Serie. 
- **s.name**: Puedes asignar un nombre a la Serie mediante el atributo name. Esto es útil cuando la Serie forma parte de un DataFrame. 
- **s.shape**: Este atributo retorna una tupla que indica la forma de la Serie. Dado que una Serie es un array unidimensional, la forma será una tupla con un solo valor, que es la longitud de la Serie. 
- **s.size**: El atributo size devuelve el número total de elementos en la Serie. 


## Acceso a los elementos de una serie
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

## Métodos de una serie de Pandas
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

