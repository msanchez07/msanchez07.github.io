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


# Trabajar con varios DataFrames
Cuando trabajamos con más de un DataFrame, lo que solemos querer es unirlos. Pandas cuenta con las funcion es `concat()` y `merge()` para poder unir cualquier DataFrame de distintas maneras. La [documentación de pandas](https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html) ofrece una guía muy detallada de todo lo que podemos hacer, pero aquí veremos una pequeña introducción.

## Concat
Concat permite fusionar dos DataFrames tanto a nivel de fila como a nivel de columna:

`pandas.melt(frame, id_vars=None, value_vars=None, var_name=None, value_name='value', col_level=None, ignore_index=True)`

En el caso de querer unirla a niovel de filas, el resultado será un nuevo DataFrame con todas las filas de los DataFrames unidos:

![](../../../images/pandas/08.png)

Por otro lado, so lo unimos a nivel de columna, el resultado será un nuevo DataFrame con todas las columnas de los anteriores concatenadas:

![](../../../images/pandas/09.png)

Vamos a ver un par de ejemplos partiendo de los siguientes DataFrames:


```{code-cell}
import pandas as pd 

df1 = pd.DataFrame({'A': ["A0", "A1", "A2", "A3"],
                    'B': ["B0", "B1", "B2", "B3"],
                    'C': ["C0", "C1", "C2", "C3"]})

df1
```

```{code-cell}
df2 = pd.DataFrame({'A': ["A4", "A5", "A6", "A7"],
                    'B': ["B4", "B5", "B6", "B7"],
                    'C': ["C4", "C5", "C6", "C7"]})
df2
```

```{code-cell}
df3 = pd.DataFrame({'D': ["D0", "D1", "D2", "D3"],
                    'E': ["E0", "E1", "E2", "E3"],
                    'F': ["F0", "F1", "F2", "F3"]})
df3
```

Lo primero que vamos a hacer es unir los dos primeros DataFrames a nivel de fila, generando un nuevo DataFrame con todas las filas que lo componen:

```{code-cell}
concat_df = pd.concat((df1, df2), axis=0)
concat_df
```

A continuación, vamos a unir el primer DataFrame y el segundo a nivel de columna:


```{code-cell}
concat_df = pd.concat((df1, df3), axis=1)
concat_df
```

Cabe destacar que ne los ejemplos solo se han unido dos DataFrames, pero que en la práctica puedes unir tantos como quieras.


## Merge 
El método merge nos permite unir dos dataframes como si utilizaramos un join con tablas SQL. 

`DataFrame.merge(right, how='inner', on=None, left_on=None, right_on=None, left_index=False, right_index=False, sort=False, suffixes=('_x', '_y'), copy=None, indicator=False, validate=None)`

Las operaciones permitidas son:

- `inner join`
- `outer join`
- `left join`
- `right join`


Para este apartado vamos a contar con los siguientes dataframes:

![](../../../images/pandas/10.png)


```{code-cell}
df1 = pd.DataFrame({"nombre": ['Arturo', 'Ramón', 'Enrique', 'Ana', 'María', 'Marta', 'Helena'],
                    'coche': ['si', 'no', 'si', 'no', 'si', 'si', 'no'],
                    'sexo': ['hombre', 'hombre', 'hombre', 'mujer', 'mujer', 'mujer', 'mujer'],
                    'cargo': ['Comercial', 'Comercial', 'Comercial', 'Programador', 'Programador', 'Programador', 'Gerente']})

df1
```


```{code-cell}
df2 = pd.DataFrame({'cargo': ['Comercial', 'Programador', 'Analista'],
                    'salario': [30000, 28000, 40000]})
df2
```

### Inner Join
Esta cláusula busca coincidencias entre 2 dataframes, en función a una columna que tienen en común y que debe ser indicada:

```{code-cell}
pd.merge(df1, df2, how="inner", on="cargo")
```

### Outer join
El outer join obtendrá todas las filas de df1y df2, y colocará  NaN en aquellos elementos que no estén disponibles:

```{code-cell}
pd.merge(df1, df2, how="outer", on="cargo")
```

### Left join
El left join devuelve todas las filas del df1 y todas las columnas del df1 y df2, añadiendo NaN donde no haya datos en las columnas del df2:

```{code-cell}
pd.merge(df1, df2, how="left", on="cargo")
```

### Right join
Es la operación inversa a left join. Devuelve todas las filas del df1 y todas las columnas del df1 y df2, añadiendo NaN donde no haya datos en las columnas del df1:


```{code-cell}
pd.merge(df1, df2, how="right", on="cargo")
```

### Indicator
Existe un parámetro adicional llamado indicator. Este parámetro, por defecto está a `False`, pero si lo cambiamos a `True` se creará una nueva columna indicando en que dataframe se han encontrado las coincidencias de la clave indicada:

```{code-cell}
pd.merge(df1, df2, how="outer", on="cargo", indicator=True)
```