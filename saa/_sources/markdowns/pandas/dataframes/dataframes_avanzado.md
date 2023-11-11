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


# DataFrames Avanzado
En el apartado anterior hemos visto como interactuar un poco con los DataFrames, cargar, exportar, obtener elementos, particionar un DataFrame y sus atributos y métodos. En este apartado vamos a ver como trabajar un poco a nivel avanzado.


## Obtener las características de un DataFrame
Un DataFrame es una herramienta muy importante dentro del análisis de datos. Permite de forma fácil obtener distintas características e información útil en el proceso de análisis de datos. 

Vamos a cargar un fichero csv en un DataFrame para poder analizar sus datos:

```{code-cell}
import pandas as pd 

df = pd.read_csv('./csv/countries.csv') 
df
```

Una vez cargado el DataFrame, podemos pegalre un primer vistazo con `head` o `tail`:

```{code-cell}
df.head()
```

Head nos muestra los `n` primeros elementos de un DataFrame, y por defecto 5. A su vez, tail muestra los `n` últimos elementos de un DataFrame, por defecto 5.


```{code-cell}
df.tail()
```

Otras funciones interesantes para obtener información de un DataFrame son:

-  `info()`
-  `describe()`

La primera nos muestra un resumen de los datos que contiene el DataFrame, cuantas filas tiene, columnas, valores nulos, etc.

```{code-cell}
df.info()
```

La segunda, información estadística del DataFrame:

```{code-cell}
df.describe()
```

A su vez, podemos utilizar el parámetro all para obtener información más detallada del DataFrame:

```{code-cell}
df.describe(include="all")
```

## Remodelar un DataFrame
La manipulación de DataFrames es una parte fundamental del análisis de datos en Python. A menudo, necesitamos remodelar nuestros datos para adaptarlos a nuestras necesidades de análisis. En este apartado, exploraremos cuatro funciones clave de remodelación de DataFrames en la biblioteca pandas: `pivot`, `stack`, `unstack` y `melt`. Estas funciones son esenciales para transformar datos, cambiar su estructura y realizar tareas de agregación. A lo largo de esta documentación, aprenderás cómo usar estas funciones con ejemplos prácticos y casos de uso comunes. Para ello, vamos a partir del siguiente DataFrame:



```{code-cell}
data = {
    'Fecha': ['2023-01-01', '2023-01-01', '2023-01-02', '2023-01-02'],
    'Categoria': ['A', 'B', 'A', 'B'],
    'Tipo': ['X', 'Y', 'X', 'Y'],
    'Valor_Cantidad': [10, 15, 8, 12],
    'Valor_Precio': [5, 6, 7, 9]
}

df = pd.DataFrame(data)
df

```


### Pivot
La función pivot permite reorganizar un DataFrame para cambiar su estructura de datos de largo a ancho. Puede ser especialmente útil cuando se desea comparar categorías o variables a través de columnas.

![](../../../images/pandas/04.png)

**`DataFrame.pivot(*, columns, index=_NoDefault.no_default, values=_NoDefault.no_default)`**


```{code-cell}
pivot_df = df.pivot(index='Fecha', columns='Categoria', values='Valor_Cantidad')

pivot_df
```

La función pivot puede producir el error **"ValueError: Index contains duplicate entries, cannot reshape"** cuando intentas aplicar la función en un DataFrame y el índice especificado (generalmente en la sección index del método pivot) contiene entradas duplicadas. Pandas no permite usar pivot si hay duplicados en las combinaciones de índice y columnas. Para resolver este error, puedes considerar las siguientes opciones:

1. **Eliminar los duplicados**: La forma más sencilla de resolver el problema es eliminar las filas duplicadas antes de aplicar pivot. Puedes utilizar el método **drop_duplicates()** para hacerlo.
2. **Agregar los valores duplicados**: Si tienes valores duplicados que deseas conservar, debes realizar una operación de agregación antes de aplicar pivot. Puedes usar el método **groupby** para agrupar y luego aplicar una función de agregación, como **sum** o **mean**, para combinar los valores duplicados.


### Stack y Unstack
Las funciones **stack** y **unstack** permiten cambiar entre estructuras de datos anchas y largas. 

**Stack** convierte columnas en un índice múltiple:

![](../../../images/pandas/05.png)

`DataFrame.stack(level=-1, dropna=_NoDefault.no_default, sort=_NoDefault.no_default, future_stack=False` 

```{code-cell}
stacked_df = df.set_index(['Fecha', 'Categoria', 'Tipo']).stack()

stacked_df
```


Por su parte **unstack** convierte un índice múltiple en columnas.


![](../../../images/pandas/06.png)

`DataFrame.unstack(level=-1, fill_value=None, sort=True)`


```{code-cell}
unstacked_df = stacked_df.unstack(level=1)

unstacked_df
```


### Melt
La función melt se utiliza para cambiar un DataFrame de ancho a largo. Convierte múltiples columnas en dos columnas: una que contiene las variables y otra que contiene los valores correspondientes.

![](../../../images/pandas/07.png)

`pandas.melt(frame, id_vars=None, value_vars=None, var_name=None, value_name='value', col_level=None, ignore_index=True)`


```{code-cell}
melted_df = df.melt(id_vars=['Fecha', 'Categoria', 'Tipo'], value_vars=['Valor_Cantidad', 'Valor_Precio'], var_name='Variable', value_name='Valor')


melted_df
```

© 2008–2022, AQR Capital Management, LLC, Lambda Foundry, Inc. and PyData Development Team
Licensed under the 3-clause BSD License.
https://pandas.pydata.org/pandas-docs/version/1.5.0/user_guide/reshaping.html