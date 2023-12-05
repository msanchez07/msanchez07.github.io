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

# Ejercicios Dataframes 3

::::{admonition} Ejercicio 1

Dado la siguiente serie:

:::{code}
ser = pd.Series(['01 Jan 2010', '02-02-2011', '20120303', '2013/04/04', '2014-05-05', '2015-06-06T12:20'])
:::

Transforma la serie para que se muestren los elementos de la serie en formato datetime.
::::


::::{admonition} Ejercicio 2
Dada la serie del ejercicio anterior, obten los siguientes elementos:
- Un array con los días del mes.
- Un array con el número de la semana.
- Un array con el año.
- Un array con el día de la semana en texto.
::::

::::{admonition} Ejercicio 3
Dada la siguiente serie:

:::{code}
ser = pd.Series(['Jan 2010', 'Feb 2011', 'Mar 2012'])
:::

Transforma la serie para que se muestra la fecha en formato Y-m-d y el días sea el último del mes.
::::

::::{admonition} Ejercicio 4
Dados los siguientes datos:

[Datos](./log_report.xlsx)

Muestra:

- Los registros que hay desde el año 2020 hasta el año actual.
- Los registros que hay de marzo de 2020.
- Cual fue la última inspección del equipo 'Pump'.
- Cuántos registros hay entre abril de 2020 y junio de 2020.
- HCuantos días han pasado desde la última inspección del equipo 'Pump'.
- Muestra los últimos 30 registros desde el día actual.
- Muestra todos los registros que se han generado en miércoles.
- Muestra el año y el número de registros de ese año.
- Muestra el mes y el número de registros en ese mes.
- Mostrar año y mes con la cantidad de registros en ese mes del año

::::

::::{admonition} Ejercicio 5
Dada la saiguiente serie:

:::{code}
ser = pd.Series(['Apple', 'Orange', 'Plan', 'Python', 'Money'])
:::

Obten aquellas alabras que tienen dos vocales.

::::

::::{admonition} Ejercicio 6
Dada la siguiente serie:

:::{code}
emails = pd.Series(['buying books at amazom.com', 'rameses@egypt.com', 'matt@t.co', 'narendra@modi.com'])
:::
Utiliza una expresión regular para obtener los emails válidos.
::::

::::{admonition} Ejercicio 7
Dado el siguiente dataframe:
:::{code}
data = {'texto': ['Python es genial', 'Programación en Python', 'Análisis de datos', 'Ciencia de datos', 'Machine Learning']}
df = pd.DataFrame(data)
:::
1. Concatena las palabras del texto en una sola cadena, separadas por guiones bajos.
2. Encuentra la palabra más larga en cada texto y almacenala en una nueva columna.
3. Cuenta la cantidad de palabras que comienzan con la letra 'a' en cada texto.
4. Reemplaza cada vocal en cada texto por la vocal siguiente en el alfabeto (a por e, e por i, etc.).
5. Crea una nueva columna que contenga solo las palabras únicas en cada texto, ordenadas alfabéticamente.
::::

