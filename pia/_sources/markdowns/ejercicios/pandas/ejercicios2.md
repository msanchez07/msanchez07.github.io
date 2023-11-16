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

# Ejercicios Dataframes 2

::::{admonition} Ejercicio 1

Dado los siguientes datos:

[Datos](./tienda.csv.zip)

Carga los datos en pandas sin descomprimirlos ¿Sabías que pandas peude leer archivos zip directamente?
::::


::::{admonition} Ejercicio 2
Obtén un DataFrame que muestre la suma de 'Unidades_Vendidas' y el valor promedio de 'Precio_Unitario' para cada categoría.
::::

::::{admonition} Ejercicio 3
Transforma el DataFrame para que tenga una columna por cada producto y el valor máximo de 'Inventario_Disponible' como filas.
::::

::::{admonition} Ejercicio 4
Aplica una operación de pivot para obtener un DataFrame que muestre el valor mínimo de 'Precio_Unitario' para cada categoría y producto.
::::

::::{admonition} Ejercicio 5
Utiliza stack para convertir el DataFrame en uno con un índice multi-nivel, donde 'Oferta' y 'Resolución' sean niveles adicionales en el índice.
::::

::::{admonition} Ejercicio 6
Aplica unstack al DataFrame resultante en el ejercicio 4 para deshacer la operación y volver al DataFrame original.
::::

::::{admonition} Ejercicio 7
Utiliza melt para transformar el DataFrame de manera que 'Producto' sea la columna clave, 'Categoria' y 'Marca' sean columnas adicionales y 'Conexión' sea la variable medida.
::::

::::{admonition} Ejercicio 8
Realiza una operación de pivot en el DataFrame de manera que 'Producto' sea el índice, 'Categoria' sea una de las columnas y el valor en la tabla sea la suma de 'Unidades_Vendidas'.
::::

::::{admonition} Ejercicio 9
Utiliza stack para convertir el DataFrame del ejercicio 7 en uno con un índice multi-nivel, donde 'Marca' sea un nivel adicional en el índice.
::::

::::{admonition} Ejercicio 10
Aplica unstack al DataFrame resultante en el ejercicio 8 para deshacer la operación y volver al DataFrame del ejercicio 7.
::::

::::{admonition} Ejercicio 11
Utiliza melt para transformar el DataFrame del ejercicio 9 de manera que 'Producto' sea la columna clave, 'Categoria' sea una de las columnas y 'Precio_Unitario' sea la variable medida.
::::