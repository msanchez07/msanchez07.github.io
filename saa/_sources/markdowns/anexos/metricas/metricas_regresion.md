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

# Anexo: Métricas de regresión
En este punto vamos a explicar cada una de las métricas y para ello vamos a partir de un ejemplo. Imagina que estás construyendo un modelo de regresión para predecir los precios de las casas en función de diferentes características, como el tamaño y la ubicación. Después de entrenar tu modelo, obtendrás predicciones de precios para cada casa en tu conjunto de datos. El MSE se centra en medir cómo de lejos están estas predicciones de los valores reales de los precios. 

Para cada predicción, calculas la diferencia entre la predicción y el valor real. Luego, elevas esta diferencia al cuadrado para eliminar signos negativos y resaltar la magnitud del error. El MSE se calcula tomando el promedio de estos errores al cuadrado. En esencia, el MSE representa el promedio de las distancias al cuadrado entre las predicciones y los valores reales. Cuanto menor sea el MSE, mejor se ajustarán las predicciones del modelo a los valores reales. 

Vamos a suponer que existen cinco casas con sus valores reales y las predicciones de tu modelo: 

<table class="table table-bordered my-table-border text-center">
  <thead>
    <tr class="my-table-header">
      <th class="text-center my-table-header" colspan="1">Casa</th>
      <th class="text-center my-table-header" colspan="1">Valor real</th>
      <th class="text-center my-table-header" colspan="1">Predicción</th>
    </tr>
  </thead>
  <tbody>
    <tr >
      <td colspan="1" >1</th>
      <td colspan="1">200.000</td>
      <td colspan="1">180.000</th>
    </tr>
    <tr >
      <td colspan="1">2</th>
      <td colspan="1">250.000</td>
      <td colspan="1">240.000</th>
    </tr>
    <tr >
      <td colspan="1">3</th>
      <td colspan="1">180.000</td>
      <td colspan="1">200.000</th>
    </tr>
    <tr >
      <td colspan="1">4</th>
      <td colspan="1">300.000</td>
      <td colspan="1">280.000</th>
    </tr>
    <tr >
      <td colspan="1">5</th>
      <td colspan="1">220.000</td>
      <td colspan="1">230.000</th>
    </tr>
  </tbody>
</table>


```{image} ../../../images/anexos/01.png
:class: bg-primary
:align: center
```



