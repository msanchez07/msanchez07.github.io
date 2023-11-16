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

# Otras operaciones con DataFrames
Vamos a ver alguans funcionalidades adicionales que podemos aplicar a los DataFrames. Algunas de ellas ya las hemos comentado anteriormente, pero aquí vamos a mostrar ejemplos prácticos.

## Aplicar funciones personalizadas
Algunas veces queremos aplicar nuestras propias funciones ya que estas no están contempladas por Pandas. Para hacer esto, contamos con varios métodos:

- `df.apply()`: aplica una función a las columnas o las filas de un dataframe (la función debe poder aceptar/devolver un array).
- `df.applymap()`: aplica una función a los elementos (para funciones que acceptan/devuelven un solo valor).
- `series.apply()/ series.map()`:, igual que las anteriores pero para series.

Vamos a ver algunos ejemplos que aplicaremos al siguiente DataFrame:

```{code-cell}
import pandas as pd
import numpy as np

np.random.seed(42)
tiempo_en_segundos = np.random.randint(0, 36000, size=10)
distancia_en_metros = np.random.randint(0, 10000, size=10)

df = pd.DataFrame({'Tiempo': tiempo_en_segundos, 'Distancia': distancia_en_metros})

df
```

Vamos a plicar una función para pasar el tiempo a horas:

```{code-cell}
df[["Tiempo"]].apply(lambda x: x / 3600)
df
```

En el ejemplo estamos aplicando una función a una columna en concreto. Podemos utilizar tanto funciones **lambda**, como **funciones clásicas** u otras funciones proporcionadas ya, por ejemplo, la suma de Numpy.

Adicionalmente a esto, las funciones que definamos también pueden aceptar parámetros adicionales, los cuales deben ser especificados:

```{code-cell}
def convert_seconds(x, to="hours"):
    if to == "hours":
        return x / 3600
    elif to == "minutes":
        return x / 60

df[['Tiempo']].apply(convert_seconds, to="minutes")
```

Algunas funciones solo devuelven un valor, en ese caso, tenemos que usar `applymap()`:

```{code-cell}
df[['Tiempo']].applymap(int)
```

## Grouping
Cuando queramos esplorar los distintos grupos que existen en un DataFrame, podemos debemos utilizar la función `grouping()`. Esta función agrupará los datos en base a las variables indicadas. Vamos a partir del siguiente dataframe para los ejemplos:

```{code-cell}
df = pd.read_csv("./csv/employees.csv")
df
```

Vamos a grupar el dataframe en base al id del departamento:

```{code-cell}
dfg = df.groupby(by='department_id')
dfg
```

Esto nos devuelve un objeto de tipo DataFrameGroupBy, el cual contiene varios subDataFrames, tantos como departamentos tengamos.

Si queremos ver todos los grupos, podemos utilizar la propiedad `groups`:

```{code-cell}
dfg.groups
```

La cual nos devuelve los grupos y los id de las filas incluidas en estos grupos. 

Por su parte, si queremos obtener un grupo en concreto, podemos utilizar la función `get_group()`:

```{code-cell}
dfg.get_group(30.0)
```

Al igual que ocurre en sql, podemos aplicar funciones de agregación a grupos de datos:

```{code-cell}
dfg[["salary"]].mean()
```

si queremos usar varias funciones a la vez, podemos utilizar la función `aggregate()`:

```{code-cell}
dfg[["salary"]].aggregate(['mean', 'sum', 'count'])
```

E incluso podemos aplicar distintas funciones a distintas columnas:


```{code-cell}

def num_range(x):
    return x.max() - x.min()

dfg.aggregate({"salary": ['max', 'min', 'mean'], 
    "employ_id": ['sum', num_range]})           
```

Por último, hay que remarcar que podemos utilizar las funciones de agregación a dataframes no agrupados. Esto es lo que hace la función `describe()`:


```{code-cell}
df[["employ_id", "salary", "manager_id", "department_id"]].agg(['mean', 'min', 'count', num_range])        
```

## Trabajar con valores nulos
Los valores nulos se representan en pandas con el valor `Nan`. Podemos utilizar la función `df.isnull()` para encontrar estos valores nulos:

```{code-cell}
df.isnull()   
```

Pero suele ser de más ayuda utilizar las funciones `info` o `any` para saber cuantos valores nulos tenemos por columna o fila:

```{code-cell}
df.info()   
```

```{code-cell}
df[df.isnull().any(axis=1)]  
```

Si queremos borrar las filas que contienen valores nulos, podemos utilizar la función `dropna()`:

```{code-cell}
df.copy().dropna() 
```

También podemos imputar valores a los nulos con la función `fillna()`. Este método tiene varias opciones, como utilizar un valor fijo, la media de la columna, el valor previo no nulo, etc.


```{code-cell}
df = pd.DataFrame([[np.nan, 5, np.nan, 2],
                   [1, 0, np.nan, 7],
                   [np.nan, np.nan, np.nan, 3],
                   [np.nan, 9, np.nan, 3]],
                  columns=['Primera', 'Segunda', 'Tercera', 'Cuarta'])
df
```

Rellenamos con ceros:

```{code-cell}
df.fillna(0) 
```

Renellamos con la media:

```{code-cell}
df.fillna(df.mean())
```

Rellenamos con el valor posterior:

```{code-cell}
df.bfill()
```

Rellenamos con el valor previo:

```{code-cell}
df.ffill()
```

Por último, podemos hacer una representación de los valores nulos que tenemos mediante una gráfica:

```{code-cell}
import seaborn as sns
sns.set(rc={'figure.figsize':(7, 7)})
np.random.seed(50)
npx = np.zeros((100,20))
mask = np.random.choice([True, False], npx.shape, p=[.1, .9])
npx[mask] = np.nan
sns.heatmap(pd.DataFrame(npx).isnull(), cmap='viridis', cbar=False);
```