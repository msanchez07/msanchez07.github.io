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

# Gestión avanzada de datos con Pandas
En este punto vamos a trabajar con métodos propios de los tipos de datos. En concreto nos vamos a centrar en los Strings y los DateTime.  

## Strings
El tipo de datos String, es representado en pandas como un `objeto`, pero este tipo de dato es usado por pandas cuando la variable no es numérica y no sabe de que tipo es. Adicionalmente a esto, Pandas ha creado un tipo nuevo llamado StringDtype para las cadeas de texto. Puedes leer más documentación de esto en la [**documentación de pandas**](https://pandas.pydata.org/pandas-docs/stable/user_guide/text.html#text-data-types).

### Métodos del tipo String
Como ya hemos visto en alguna ocasión, pandas puede aplicar operaciones a todos los elementosde un array:

```{code-cell}
import numpy as np
x = np.array([1, 2, 3, 4, 5])
x * 2
```

Esto no se puede utilizar en elementos de tipo String y el siguiente código fallaría:

```{code}
names = np.array(['Ana', 'Maria', 'Luís', 'Javi', 'Verónica'])
names.upper()
```

Por lo tanto, la única manera de aplicar esta operación es recorriendo los elementos del array y uno a uno, aplicar la operación:

```{code-cell}
names = np.array(['Ana', 'Maria', 'Luís', 'Javi', 'Verónica'])
[name.upper() for name in names]
```

Hay que tener en cuenta que el código anterior fallará si cualquier elemento de tu array es nulo. Por lo tanto, todos los elementos deben tener valor.

Pandas aborda ambos problemas anteriroes con sus métodos de String. Se puede acceder a los métodos de String mediante el atributo `.str` de los elementos o de los índices. Cabe destacar que prácticamente todas las operaciones de String están disponibles, los cuales podemos consultar en la [documentación de pandas](https://pandas.pydata.org/docs/user_guide/text.html#method-summary).

Vamos a ver algún ejemplo de aplicar las operaciones de Strings sobre los elementos de una serie:

```{code-cell}
import pandas as pd
names = np.array(['Ana', 'Maria', None, 'Javi', 'Verónica'])
s = pd.Series(names)
s
```

primero vamos a pasar todos los elementos a mayúsculas:

```{code-cell}
s.str.upper()
```

posteriormente haremos un split:

```{code-cell}
s.str.split("ri", expand=True)
```

Ahora comprobaremos la longitud de las cadenas:

```{code-cell}
s.str.len()
```

También podemos aplicar estas operaciones a los índices de las filas o a los nombres de las columnas:

```{code-cell}
df = pd.DataFrame(np.random.rand(5, 3),
                  columns = ['Columna 1', 'Columna 2', 'Columna 3'],
                  index = [f"FILA_{_}" for _ in range(5)])
df
```

Vamos a cambiar el valor de las columnas cambiando Columna por col:

```{code-cell}
df.columns = df.columns.str.replace("Columna", "Col").str.strip()
```

y las filas por row:

```{code-cell}
df.index = df.index.str.replace("FILA", "ROW")
df
```

## Trabajando con fechas
Pandas cuenta con operaciones propias para trabajar con elementos de tipo `DateTime`. A continuación vamos a ver algunas de estas operaciones. 

### Crear elementos de tipo DateTime
En este punto vamos a ver como crear elementos de tipo DateTime. Normalmente, los elementos que vas a querer crear serán:

1. Un elemento en un momento dado con la función `pd.Timestamp()`, por ejemplo `2020-07-10 00:00:00`.
2. Crear un lapso de tiempo con la función `pd.Period()`, por ejemplo, `Enero de 2020`.
3. Crear una serie de fechas y horas con `pd.date_range()` o `pd.period_range()`.


```{code-cell}
from datetime import datetime
print(pd.Timestamp('2023-10-01')) #A partir de un String.  
print(pd.Timestamp(year=2023, month=12, day=1))  # Indicando directamente la fecha.
print(pd.Timestamp(datetime(year=2024, month=1, day=1)))  # Indicando un objeto de tipo datetime.
```

Lo anterior es un momento específico. A continuación, vamos a  usar pd.Period() para especificar un lapso de tiempo (como un día):

```{code-cell}
periodo = pd.Period('2020-07-09')
print(periodo)
print(periodo.start_time)
print(periodo.end_time)
```

```{code-cell}
momento = pd.Timestamp('1900-07-07 12:00')
periodo = pd.Period('1900-07-07')
print(f"Momento: {momento}")
print(f"Periodo: {periodo}")
print(f"¿El momento está incluido en el periodo? {periodo.start_time < momento < periodo.end_time}")
```

En la mayoría de las ocasiones querrar crear matrices de fechas y horas. Para eso, se puede utilizar las clases `PeriodIndex` o `TimedeltaIndex` o `DatetimeIndex`:

```{code-cell}
pd.date_range('2020-01-01 12:00',
              '2020-12-31 12:00',
              freq='M')
```

En el ejemplo anterior hemos creado un array de fechas con una frecuencia mensual. Cabe destacar que nos ha devuelto el último día de cada més.

Por otro lado, vamos a crear un array de los días de un mes indicando un periodo de tiempo:

```{code-cell}
pd.period_range('2021-01-01',
                '2021-01-31',
                freq='D')
```

Por último, la función `Timedelata` se utiliza para generar objetos temperoales en base a operaciones de añadir o quitar tiempo:

```{code-cell}
pd.date_range('2020-01-01 12:00', '2020-01-11 12:00', freq='D') + pd.Timedelta('1.5 hour')

```

Por último, vamos a remarcar que pandas representa los valores de fecha nulos como `Nat`.

### Transformar elementos en DateTime
Es bastante común tener una serie de fechas como Strings, las cuales podemos transformar con el método `pd.to_datetime()`:

```{code-cell}
fechas = ['July 9, 2020', 'August 1, 2020', 'August 28, 2020']
fechas
```

```{code-cell}
pd.to_datetime(fechas)
```

Si quieres transformar un formato de fecha y hora más complejo, puedes utilizar el argumento `format`:


```{code-cell}
fechas = ['01/01/2023', '01/10/2024', '01/05/2025']
pd.to_datetime(fechas, format="%d/%m/%Y")
```

Tambien puedes utilizar un diccionario para indicar los elementos que quieres transformar:

```{code-cell}
dict_fechas = pd.to_datetime({"year": [2023, 2024, 2025],
                             "month": [1, 2, 3],
                             "day": [23, 24, 25]})  
dict_fechas
```

### Indexar y filtrar por fechas y horas

Vamos a cargar el DataFrame de empleados indicando que queremos que nuestr índice sea la columna correspondiente a la fecha de contratación y que parsee los campos de tipo fecha:

```{code-cell}
df = pd.read_csv("csv/employees.csv", index_col=5, parse_dates=True)
df
```


Ahora, ya podemos filtrar en base a esta columna de forma fácil:

```{code-cell}
df.loc['1987-06']
```

O indicando la fecha de contratación exacta:

```{code-cell}
df.loc['1987-06-21']
```

También podemos indicar un rango de fechas:


```{code-cell}
df.loc['1987-06-20':'1987-06-30']
```

O utilizar `query`:

```{code-cell}
df.query("'1987-06-21'")
```

### Descomposición de fechas y horas:
Podemos descomponer fácilmente nuestra serie temporal en los componentes que la constituyen. Hay muchos atributos que definen a estos elementos:

```{code-cell}
df.index.year
```

```{code-cell}
df.index.second
```


```{code-cell}
df.index.weekday
```

Las fechas también cuentan con una serie de métodos que podemos utilizar:

```{code-cell}
df.index.day_name()
```

```{code-cell}
df.index.month_name()
```

### Desplazar fechas y zona horaria
Antes vimos cómo podemos usar `Timedelta` para sumar/restar tiempo a nuestras fechas y horas. `Timedelta` respeta el tiempo absoluto, lo que puede resultar problemático en algunos casos, donde el tiempo no es regular. Por ejemplo, el 8 de marzo comenzó el horario de verano en Canadá y los relojes avanzaron 1 hora:

```{code-cell}
t1 = pd.Timestamp('2020-03-07 12:00:00', tz='Canada/Pacific')
t2 = t1 + pd.Timedelta("1 day")
print(f"Original time: {t1}")
print(f" Plus one day: {t2}")  # note that time has moved from 12:00 -> 13:00
```

Para solucionar este problema, debemos usar la función `Dateoffset`:


```{code-cell}
t3 = t1 + pd.DateOffset(days=1)
print(f"Original time: {t1}")
print(f" Plus one day: {t3}")  # note that time has stayed at 12:00
```

De forma predeterminada, los objetos de fecha y hora no reconocen la zona horaria. Para asociar horas con una zona horaria, podemos usar el argumento `tz` en la construcción, o podemos usar el método `tz_localize()`:

```{code-cell}
print(f"        No timezone: {pd.Timestamp('2020-03-07 12:00:00').tz}")
print(f"             tz arg: {pd.Timestamp('2020-03-07 12:00:00', tz='Canada/Pacific').tz}")
print(f".tz_localize method: {pd.Timestamp('2020-03-07 12:00:00').tz_localize('Canada/Pacific').tz}")
```

Por último, podemos utilizar el método `tz_convert()` para convertir zonas horarias o el método `DateOffset` para añadir o quitar tiempo.

### Redimensionar y utilizar funciones de agregación
Una de las operaciones más comunes que solemos realizar cuando trabajamos con series temporales es modificar la serie temporal a una agregación más gruesa/fina/regular. Por ejemplo, es posible que desees modificar los datos diarios en datos semanales. Podemos hacerlo con el método `resample()` . Por ejemplo, vamos a volver al dataframe de empleados:

```{code-cell}
df = df[["salary", "department_id"]]
df.index
```

Vamos a redimensionar el dataframe, lo cual es muy parecido a utilizar un `groupby`:


```{code-cell}
dfr = df.resample("1M").count()
dfr
```

Con esto lo que hemos hecho ha sido contar cuanta gente se contrato en cada mes.
