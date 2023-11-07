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


# Trabajar con varios dataframes
En el apartado anterior hemos visto como interactuar un poco con los DataFrames, cargar, exportar, obtener elementos, particionar un DataFrame y sus atributos y métodos. En este apartado vamos a ver como trabajar un poco a nivel avanzado.



```{code-cell}
import pandas as pd 

df = pd.read_csv('./csv/countries.csv') 
df
```



![](../../../images/pandas/07.png)

`pandas.melt(frame, id_vars=None, value_vars=None, var_name=None, value_name='value', col_level=None, ignore_index=True)`


```{code-cell}
melted_df = df.melt(id_vars=['Fecha', 'Categoria', 'Tipo'], value_vars=['Valor_Cantidad', 'Valor_Precio'], var_name='Variable', value_name='Valor')


melted_df
```

© 2008–2022, AQR Capital Management, LLC, Lambda Foundry, Inc. and PyData Development Team
Licensed under the 3-clause BSD License.
https://pandas.pydata.org/pandas-docs/version/1.5.0/user_guide/reshaping.html