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
Concat une dos Dataframes sobreponiendolos, es decir, uniendo las filas.



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


![](../../../images/pandas/08.png)

`pandas.melt(frame, id_vars=None, value_vars=None, var_name=None, value_name='value', col_level=None, ignore_index=True)`


![](../../../images/pandas/09.png)

```{code-cell}
melted_df = df.melt(id_vars=['Fecha', 'Categoria', 'Tipo'], value_vars=['Valor_Cantidad', 'Valor_Precio'], var_name='Variable', value_name='Valor')


melted_df
```

© 2008–2022, AQR Capital Management, LLC, Lambda Foundry, Inc. and PyData Development Team
Licensed under the 3-clause BSD License.
https://pandas.pydata.org/pandas-docs/version/1.5.0/user_guide/reshaping.html