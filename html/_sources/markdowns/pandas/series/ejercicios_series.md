---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# Ejercicios Series

::::{admonition} Ejercicio 1

Dada una serie: 

:::{code}
import pandas as pd 

data = pd.Series([1, 2, 3, 4, 5])
:::

Escribe una función que filtre la serie y devuelva solo los valores mayores que 30. 
::::

::::{admonition} Ejercicio 2

Dada una serie fechas que contiene fechas: 

:::{code}
import pandas as pd 

fechas = pd.to_datetime(['2023-01-15', '2023-02-20', '2023-03-25', '2023-04-30', '2023-05-15']) 
:::

Crea una función que calcule la diferencia en días entre cada fecha y la fecha más temprana en la serie. 
::::


::::{admonition} Ejercicio 3

Dada una serie fechas que contiene fechas: 

:::{code}
import pandas as pd 

nombres = pd.Series(['Ana', 'Juan', 'María', 'Carlos', 'Sofía']) 
:::

Escribe una función que devuelva una nueva serie con la primera letra de cada nombre en mayúsculas. 
::::


::::{admonition} Ejercicio 4

Crea una serie aleatoria de longitud 10 que contenga números enteros aleatorios entre 1 y 100. Luego, escribe una función para encontrar el número más grande en la serie. 

::::


::::{admonition} Ejercicio 5

Crea una serie que represente la población de una ciudad en diferentes años. Luego, escribe una función que calcule la tasa de crecimiento anual de la población en base a un valor que tu consideres. 
::::


::::{admonition} Ejercicio 6

Dada una serie que contiene algunos valores nulos: 

:::{code}
import pandas as pd 
import numpy as np 

valores = pd.Series([1, 2, np.nan, 4, np.nan, 6, 7, np.nan, 9, 10]) 
:::

Escribe una función que reemplace los valores nulos con el promedio de los valores no nulos en la serie. 
::::


::::{admonition} Ejercicio 7

Dada una serie de fechas: 

:::{code}
import pandas as pd 
import numpy as np 

horarios = pd.to_datetime(['2023-01-15 08:30', '2023-02-20 12:45', '2023-03-25 19:15', '2023-04-30 22:00']) 
:::

Escribe una función que calcule la diferencia en horas entre cada par de fechas consecutivas. 
::::


::::{admonition} Ejercicio 8

Dada una serie de texto: 

:::{code}
import pandas as pd 

texto = pd.Series(['Python es genial', 'Data Science es emocionante', 'Aprender es divertido']) 
:::

Escribe una función que cuente cuántas palabras en cada elemento de la serie tienen una longitud de 6 letras o más. 
::::
 
 
 ::::{admonition} Ejercicio 9

Dada una serie que contiene nombres y fechas de nacimiento de personas, escribe una función que calcule la edad de cada persona en años completos a partir de su fecha de nacimiento. Luego, debes crear una nueva serie que contenga los nombres y las edades de las personas.: 

:::{code}
import pandas as pd 

datos = {'Nombre': ['Ana', 'Juan', 'María', 'Carlos'], 
'FechaNacimiento': ['1990-03-15', '1985-12-10', '1995-05-20', '1980-07-01']} 

personas = pd.DataFrame(datos) 

personas['FechaNacimiento'] = pd.to_datetime(personas['FechaNacimiento']) 
:::

::::


::::{admonition} Ejercicio 10

Crea dos series serie1 y serie2 con etiquetas que se superpongan. Luego, escribe una función que combine ambas series, sumando los valores correspondientes cuando las etiquetas coinciden. 

Ejemplo de series que se superponen 

:::{code}
import pandas as pd 

serie1 = pd.Series([10, 20, 30], index=['A', 'B', 'C']) 
serie2 = pd.Series([15, 25, 35], index=['B', 'C', 'D']) 
:::

::::



 



 

 