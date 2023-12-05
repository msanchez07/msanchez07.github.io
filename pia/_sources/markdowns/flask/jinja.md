# [Jinja2](https://jinja.palletsprojects.com/en/2.10.x/)
Flask utiliza plantillas basadas en el motor de plantillas Jinja2. Jinja2 es un potente motor de plantillas para Python que se integra de manera nativa con Flask y es ampliamente utilizado en el desarrollo web con este framework.

Algunas características destacadas de Jinja2 y cómo se utilizan en Flask incluyen:

- **Sintaxis clara y expresiva**: Jinja2 utiliza una sintaxis sencilla y legible que facilita la creación de plantillas. Por ejemplo, las variables se encierran entre dobles corchetes ({{ variable }}) y las estructuras de control como bucles y condicionales se manejan de manera intuitiva.

- **Herencia de plantillas**: Jinja2 permite la herencia de plantillas, lo que significa que puedes definir una plantilla base con la estructura común de tu sitio y luego extenderla en plantillas secundarias para agregar contenido específico.

- **Filtros y macros**: Jinja2 ofrece filtros que permiten manipular el contenido de las variables y macros que permiten definir bloques de contenido reutilizables.

- **Control de flujo**: Puedes utilizar estructuras de control de flujo como bucles ({% for ... %}) y condicionales ({% if ... %}) en tus plantillas para manejar de manera dinámica la presentación de datos.

- **Inclusión de plantillas**: Puedes incluir una plantilla dentro de otra mediante la directiva {% include 'nombre_de_la_plantilla.html' %}, lo que facilita la modularidad y la reutilización de código.

Aquí hay un ejemplo mínimo de una plantilla en Jinja2 que podrías usar en Flask:

```html
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>{{ titulo }}</title>
    </head>
    <body>
        <h1>{{ titulo }}</h1>
        <ul>
            {% for item in lista %}
                <li>{{ item }}</li>
            {% endfor %}
        </ul>
    </body>
</html>
```

En Flask, las plantillas Jinja2 se almacenan generalmente en el directorio **templates en el directorio principal de tu aplicación**, y Flask automáticamente busca plantillas en este directorio. La integración fluida entre Flask y Jinja2 permite la creación de interfaces web dinámicas y flexibles.

## Configuración predeterminada
En Flask, la configuración predeterminada de Jinja2 se ajusta para adaptarse a las prácticas comunes y para proporcionar un entorno de desarrollo cómodo. A continuación, se muestran algunas de las configuraciones predeterminas de Jinja2 en Flask:

- **trim_blocks y lstrip_blocks**: Ambos están establecidos en False por defecto, lo que significa que no se eliminarán automáticamente los espacios en blanco al comienzo y al final de los bloques de plantillas.

- **autoescape**: Está establecido en True por defecto, lo que significa que las variables se escaparán automáticamente para evitar ataques de inyección de código. Sin embargo, si se detecta que una variable ya está marcada como segura (usando el filtro safe), no se aplicará el escape.

- **undefined**: Por defecto, se utiliza el objeto StrictUndefined como el objeto undefined. Esto significa que acceder a variables no definidas en las plantillas generará una excepción UndefinedError.

- **loader**: Flask configura automáticamente el cargador de plantillas para buscar en el directorio templates dentro de la aplicación.

Estas configuraciones proporcionan un entorno seguro y razonable por defecto. Sin embargo, puedes personalizar estas opciones según tus necesidades específicas utilizando la propiedad **jinja_options** en tu aplicación Flask. Por ejemplo:

```{code}
from flask import Flask

app = Flask(__name__)

# Configuración personalizada de Jinja2
app.jinja_options = {'trim_blocks': True, 'lstrip_blocks': True, 'autoescape': True, 'undefined': app.jinja_options['undefined']}
```

Esta configuración personalizada está configurando **trim_blocks**, **lstrip_blocks**, y **autoescape** a True. Además, utiliza el objeto undefined predeterminado de la aplicación Flask. Puedes ajustar estas opciones según tus preferencias y requisitos específicos del proyecto.

## Contexto estandar
En Flask, varias variables y objetos están disponibles por defecto en el contexto de Jinja2. Estas variables proporcionan información útil sobre la solicitud actual, la aplicación y otras configuraciones. Algunas de las variables y objetos más comunes incluyen:

- **request**: Proporciona acceso a la solicitud HTTP actual. Puedes utilizarlo para acceder a parámetros de consulta, datos de formulario y otros detalles de la solicitud.

- **session**: Si estás utilizando sesiones en Flask, puedes acceder a este objeto para almacenar y recuperar datos de la sesión.

- **g**: Un objeto "global" que se puede utilizar para almacenar datos temporales durante el ciclo de vida de una solicitud. Especificado como "global" solo en el contexto de una solicitud específica.

- **url_for**: Una función que te permite generar URLs para funciones de vista específicas en tu aplicación.

- **config**: Acceso a la configuración de la aplicación, que se puede definir en el objeto de la aplicación Flask.

- **get_flashed_messages**: Una función para recuperar mensajes intermitentes almacenados en la sesión.

- **app**: Una referencia a la instancia de la aplicación Flask. Puedes acceder a esto para obtener información sobre la aplicación, como su nombre.

- **url_for**: Una función que se utiliza para generar URLs. Puedes usarla para generar URLs dinámicamente basadas en el nombre de la función de vista.

Estas variables están disponibles por defecto en el contexto de Jinja2 y pueden ser utilizadas en tus plantillas sin necesidad de configuración adicional. Aquí hay un ejemplo simple de cómo podrías utilizar algunas de estas variables en una plantilla:

```html
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>{{ config['TITLE'] }}</title>
    </head>
    <body>
        <h1>Bienvenido a {{ config['TITLE'] }}</h1>
        <p>Esta es la ruta actual: {{ request.path }}</p>
        <p>Mensajes intermitentes: {{ get_flashed_messages() }}</p>
    </body>
</html>
```

Estas variables facilitan el acceso a información clave en tus plantillas y son parte integral del flujo de trabajo típico de Flask.

## Controlando el autoescape
En Jinja2, el autoescape es una característica que protege automáticamente contra ataques de inyección de código HTML y garantiza que las variables renderizadas en las plantillas sean escapadas para prevenir scripts maliciosos. Flask, por defecto, habilita el autoescape en Jinja2 para garantizar la seguridad. Sin embargo, hay situaciones en las que puede ser necesario desactivar o controlar manualmente el autoescape.

A continuación, se presentan algunas formas de controlar el autoescape en Jinja2 dentro de Flask.

### Desactivar el autoescape para una variable específica
Si deseas desactivar el autoescape para una variable específica en una plantilla, puedes utilizar el modificador **|safe**. Esto indica a Jinja2 que confíe en el contenido y no aplique el escape:

```html
<p>{{ mi_variable | safe }}</p>
```

```{admonition}
:class: note
Utiliza esto con precaución, ya que desactivar el autoescape para una variable implica que debes asegurarte de que el contenido sea seguro y no provenga de fuentes no confiables.
```

### Desactivar el autoescape para una sección de la plantilla
Si deseas desactivar el autoescape para una sección completa de la plantilla, puedes hacerlo utilizando los bloques **{% autoescape %}** y **{% endautoescape %}**:

```html
{% autoescape false %}
    <p>{{ mi_variable }}</p>
{% endautoescape %}
```

### Controlar el autoescape a nivel de la aplicación
En tu aplicación Flask, puedes configurar el autoescape globalmente para todas las plantillas. Puedes hacer esto modificando la propiedad autoescape del entorno de Jinja2:

```{code}
from flask import Flask, render_template, Markup

app = Flask(__name__)

# Desactivar el autoescape globalmente
app.jinja_options = {'autoescape': False}

@app.route('/')
def home():
    return render_template('index.html', mi_variable=Markup('<script>alert("¡Ataque!");</script>'))

```
Aquí, hemos configurado autoescape en False globalmente para todas las plantillas. Además, hemos utilizado Markup para marcar explícitamente la variable como segura.

Recuerda que la seguridad es una consideración crucial al trabajar con plantillas y datos dinámicos. Siempre es preferible mantener el autoescape activado para prevenir ataques de inyección de código. Desactiva el autoescape solo cuando estés completamente seguro de que el contenido es seguro y de confianza.

## Registrar filtros
En Flask, puedes registrar filtros personalizados en Jinja2 para extender las capacidades del sistema de plantillas. Puedes hacer esto utilizando el decorador **app.template_filter** o el método **app.add_template_filter**. Aquí te muestro cómo registrar filtros personalizados en tu aplicación Flask:

### Usando el Decorador @app.template_filter

```{code}
from flask import Flask

app = Flask(__name__)

# Definir un filtro personalizado con el decorador
@app.template_filter('nombre_del_filtro')
def mi_filtro(valor):
    # Lógica del filtro
    return valor.upper()

```

Luego, en tu plantilla Jinja2, puedes usar este filtro de la siguiente manera:

```html
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Filtro Personalizado</title>
    </head>
    <body>
        <p>{{ "Hola, Mundo" | nombre_del_filtro }}</p>
    </body>
</html>
```

### Usando app.add_template_filter
```{code}
from flask import Flask

app = Flask(__name__)

# Definir la función del filtro
def mi_filtro(valor):
    return valor.upper()

# Registrar el filtro en la aplicación
app.add_template_filter(mi_filtro, 'nombre_del_filtro')

```

El resultado en la plantilla será el mismo:

```html
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Filtro Personalizado</title>
    </head>
    <body>
        <p>{{ "Hola, Mundo" | nombre_del_filtro }}</p>
    </body>
</html>

```

En estos ejemplos, hemos registrado un filtro personalizado llamado nombre_del_filtro que convierte el texto a mayúsculas. Puedes adaptar la lógica del filtro según tus necesidades.

Recuerda que los filtros personalizados te permiten extender las funcionalidades de Jinja2 y realizar manipulaciones en los datos antes de renderizarlos en la plantilla.

## Context processors
Los **"context processors"** en Flask son funciones que se ejecutan antes de que se renderice cualquier plantilla y añaden variables al contexto global de Jinja2. Estas variables estarán disponibles en todas las plantillas de la aplicación. Los context processors son útiles para proporcionar datos comunes o configuración a todas las vistas.

Para definir un context processor en Flask, puedes utilizar el decorador **app.context_processor**. Aquí hay un ejemplo de cómo puedes usar context processors en tu aplicación Flask:

```{code}
from flask import Flask, render_template

app = Flask(__name__)

# Context processor para proporcionar datos comunes a todas las plantillas
@app.context_processor
def inject_common_data():
    # Puedes proporcionar cualquier dato que desees que esté disponible en todas las plantillas
    common_data = {
        'sitio_web_nombre': 'Mi Sitio Web',
        'autor': 'John Doe'
    }
    return common_data

# Ruta de ejemplo
@app.route('/')
def home():
    # Renderiza la plantilla sin necesidad de pasar 'sitio_web_nombre' y 'autor' explicitamente
    return render_template('index.html')

if __name__ == '__main__':
    app.run(debug=True)

```

En este ejemplo, el context processor **inject_common_data** añade las variables sitio_web_nombre y autor al contexto global de Jinja2. Estas variables estarán disponibles en todas las plantillas sin necesidad de pasarlas explícitamente en cada llamada a render_template.

Y en tu plantilla (index.html), puedes acceder a estas variables directamente:

```html
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>{{ sitio_web_nombre }}</title>
    </head>
    <body>
        <h1>Bienvenido a {{ sitio_web_nombre }}</h1>
        <p>Autor: {{ autor }}</p>
    </body>
</html>
```

Esto permite tener datos comunes accesibles en todas las plantillas, lo que puede ser útil para la información del sitio, datos del usuario actualmente autenticado, o cualquier otro dato global que necesites compartir entre tus vistas.


## Streaming
El "streaming" en el contexto de Jinja2 y Flask se refiere a la capacidad de enviar la salida de una plantilla de manera incremental al cliente, en lugar de esperar a que se complete todo el procesamiento antes de enviarla por completo. Esto puede ser útil cuando se generan grandes cantidades de datos o se realizan operaciones costosas, permitiendo una respuesta más rápida al usuario.

En Flask, puedes habilitar el streaming en una plantilla utilizando el objeto **stream_with_context** proporcionado por Flask. Aquí tienes un ejemplo básico:

```{code}
from flask import Flask, render_template, stream_with_context
import time

app = Flask(__name__)

# Ruta de ejemplo con streaming
@app.route('/streaming_example')
def streaming_example():
    # Función generadora que simula la generación de datos
    def generate():
        for i in range(10):
            time.sleep(1)  # Simula una operación costosa
            yield f'Número: {i}<br/>\n'
    
    # Utiliza stream_with_context para habilitar el streaming
    return app.response_class(stream_with_context(generate()), content_type='text/html')

if __name__ == '__main__':
    app.run(debug=True)

```

En este ejemplo, la función **generate** es una función generadora que simula la generación de datos. La función **stream_with_context** se utiliza para habilitar el streaming, y se envía cada elemento generado al cliente tan pronto como esté disponible, en lugar de esperar a que se complete todo el proceso.

En tu plantilla, puedes acceder a esta ruta como cualquier otra, por ejemplo:

```html
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Streaming Example</title>
    </head>
    <body>
        <h1>Streaming Example</h1>
        <div>
            {% for mensaje in stream %}
                {{ mensaje | safe }}
            {% endfor %}
        </div>
    </body>
</html>

```

En este ejemplo, el bucle {% for mensaje in stream %} se encarga de mostrar cada mensaje enviado por el servidor en tiempo real.

## Ejemplos
Vamos a ver unos pocos ejemplos de como utilizar Jinja2 con flask. En el primer ejemplo vamos a cargar una plantilla para la ruta principal a la cual le pasamos el nombre de un usuario para que se muestre:

```{code}
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    # Pasa una variable a la plantilla
    nombre = "Usuario"
    return render_template('ejemplo_template.html', nombre=nombre)

if __name__ == '__main__':
    app.run(debug=True)
```

```html
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Ejemplo de Plantilla Jinja2 con Flask</title>
    </head>
    <body>
        <h1>Hola, {{ nombre }}!</h1>
    </body>
</html>
```

Vamos a seguir con un ejemplo donde en vez de pasar una variable, pasemos varias:

```{code}
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    # Pasa varias variables a la plantilla
    usuario = "Usuario"
    edad = 25
    lenguajes = ['Python', 'JavaScript', 'HTML', 'CSS']
    return render_template('ejemplo_variables_template.html', usuario=usuario, edad=edad, lenguajes=lenguajes)

if __name__ == '__main__':
    app.run(debug=True)
```

```html
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Ejemplo de Variables Jinja2 con Flask</title>
    </head>
    <body>
        <h1>Hola, {{ usuario }}!</h1>
        <p>Edad: {{ edad }}</p>
        <p>Lenguajes de programación favoritos:</p>
        <ul>
            {% for lenguaje in lenguajes %}
                <li>{{ lenguaje }}</li>
            {% endfor %}
        </ul>
    </body>
</html>
```

date cuenta que también hemos utilizado el bucle for para recorrer los lenguajes y mostrarlo. Bien, todo funciona, ahora utilizemos diccionarios:

```{code}
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    # Pasa un diccionario a la plantilla
    informacion_usuario = {
        'nombre': 'Usuario',
        'edad': 25,
        'lenguajes': ['Python', 'JavaScript', 'HTML', 'CSS']
    }
    return render_template('ejemplo_diccionario_template.html', informacion_usuario=informacion_usuario)

if __name__ == '__main__':
    app.run(debug=True)
```

```html
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Ejemplo de Diccionario Jinja2 con Flask</title>
    </head>
    <body>
        <h1>Hola, {{ informacion_usuario.nombre }}!</h1>
        <p>Edad: {{ informacion_usuario.edad }}</p>
        <p>Lenguajes de programación favoritos:</p>
        <ul>
            {% for lenguaje in informacion_usuario.lenguajes %}
                <li>{{ lenguaje }}</li>
            {% endfor %}
        </ul>
    </body>
</html>
```

Ya por último, veremos un ejemplo de uso de condicionales:

```{code}
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def index():
    # Pasa un diccionario a la plantilla
    informacion_usuario = {
        'nombre': 'Usuario',
        'edad': 25,
        'lenguajes': ['Python', 'JavaScript', 'HTML', 'CSS']
    }
    return render_template('ejemplo_condicional_template.html', informacion_usuario=informacion_usuario)

if __name__ == '__main__':
    app.run(debug=True)
```

```html
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Ejemplo de Condicional Jinja2 con Flask</title>
    </head>
    <body>
        <h1>Hola, {{ informacion_usuario.nombre }}!</h1>

        {% if informacion_usuario.edad < 18 %}
            <p>Eres menor de edad.</p>
        {% elif informacion_usuario.edad >= 18 and informacion_usuario.edad < 30 %}
            <p>Eres un joven adulto.</p>
        {% else %}
            <p>Eres mayor de 30 años.</p>
        {% endif %}

        <p>Lenguajes de programación favoritos:</p>
        <ul>
            {% for lenguaje in informacion_usuario.lenguajes %}
                <li>{{ lenguaje }}</li>
            {% endfor %}
        </ul>
    </body>
</html>
```