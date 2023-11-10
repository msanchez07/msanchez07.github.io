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

# Ejercicios Dataframes 1

::::{admonition} Ejercicio 1

Crea un nuevo DataFrame el cual tenga los índices por defecto, es decir, sin especificar por el usuario. Realiza las siguientes modificaciones:

- Modifica los índices del DataFrame, indicando tu los nuevos índices.
- Selecciona los datos de un índice en concreto del DataFrame.
- Obten el nombre de las filas y las columnas del DataFrame.
- Obten el tipo de datos de las columnas del DataFrame.
- Obten un primer vistazo de la información que contiene el DataFrame.
::::


::::{admonition} Ejercicio 2

Dado el siguiente diccionario:

:::{code}
datos = {'real': [3.1415], 'entero': [0], 'fecha': [pd.Timestamp('20170121')], 'cadena': ['Python']}
:::

Crea un nuevo DataFrame y obten todas las columnas de tipo entero.
::::

::::{admonition} Ejercicio 3
Dado el siguiente DataFrame:

:::{code}
nombre = ['Oliva', 'Daniela', 'Juan', 'Germán', 'Edward', 'Alex', 'Julio', 
          'Edgar', 'Angie', 'Irlesa']
puntaje = [11.5, 8, 15.5, np.nan, 8, 19, 13.5, np.nan, 8, 18]
intentos = [1, 3, 2, 3, 2, 3, 1, 1, 2, 1]
califico = ['Sí', 'No', 'Sí', 'No', 'No', 'Sí', 'Sí', 'No', 'No', 'Sí']

indices = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']

jugadores = {'nombre': nombre, 'puntaje': puntaje, 'intentos': intentos, 'califico': califico}

df = pd.DataFrame(data=jugadores, index=indices)
:::

Realiza las siguientes operaciones:

- Obtenen las primeras **n** filas.
- Obtenen las últimas **n** filas.
- Utiliza el método loc para seleccionar un subconjunto de filas y columnas de un DataFrame.
- Utiliza el método iloc para seleccionar un subconjunto de filas y columnas de un DataFrame.
- Ordena un DataFrame en función de los valores de una columna en orden ascendente y descendente.
- Utiliza operaciones de agregación como sum, mean o count en un DataFrame para resumir los datos de una columna específica.
::::

::::{admonition} Ejercicio 4
Dado el DataFrame del ejercicio anterior, realiza las siguientes operaciones:

- Obtenen las primeras **n** filas.
- Obtenen las últimas **n** filas.
- Utiliza el método loc para seleccionar un subconjunto de filas y columnas de un DataFrame.
- Utiliza el método iloc para seleccionar un subconjunto de filas y columnas de un DataFrame.
- Ordena un DataFrame en función de los valores de una columna en orden ascendente y descendente.
- Utiliza operaciones de agregación como sum, mean o count en un DataFrame para resumir los datos de una columna específica.
::::

::::{admonition} Ejercicio 5
Dado el siguiente archivo csv con los datos de los empleados de una empresa:

[Empleados](./csv/employees.csv)

Realiza las siguientes operaciones:

- Obten el nombre de aquellos empleados que tienen un salario inferior a 3000 euros.
- Obten el nombre de los empleados cuyo nombre empiece por J.
- Obten el nombre y el apellido de los empleados cuyo apeliido no contenga una h.
- Ordena los empleados en base a su departamento.
- Obten el empleado que es el gerente de la empresa.
- Obten todos los empleados que están a cargo de un jefe.
::::