# [Flask](https://flask.palletsprojects.com/en/3.0.x/)
Flask es un ligero y versátil framework web para Python que ha ganado popularidad por su simplicidad y flexibilidad. Diseñado para ser fácil de aprender y rápido de implementar, Flask proporciona las herramientas esenciales para construir aplicaciones web y APIs de manera eficiente.

A diferencia de algunos frameworks más completos, Flask sigue el principio de "hazlo simple", permitiéndote elegir las herramientas y extensiones que necesitas según los requisitos específicos de tu proyecto. Esto hace que Flask sea una excelente opción tanto para principiantes como para desarrolladores experimentados que buscan un marco de trabajo ágil y fácil de entender.

Con Flask, puedes crear rápidamente aplicaciones web, APIs RESTful, o incluso prototipos, gracias a su enfoque minimalista y su amplia comunidad de desarrolladores. Además, Flask se integra fácilmente con otras bibliotecas y herramientas, lo que facilita la ampliación de funcionalidades según sea necesario.

## Variantes de Flask
Flask es conocido por su enfoque minimalista y modular, pero a lo largo del tiempo, la comunidad ha desarrollado varias extensiones y variantes que amplían las capacidades del framework base. Algunas de estas variantes y extensiones notables de Flask incluyen:

<table class="table table-bordered my-table-border">
  <thead>
    <tr class="my-table-header">
      <th class="text-center my-table-header" colspan="4">VARIANTES FLASK</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th class="left-header" scope="row">Flask-RESTful</th>
      <td  colspan="3">Diseñada específicamente para el desarrollo de APIs RESTful, esta extensión simplifica la creación de recursos, manejo de solicitudes y respuestas, y otras tareas comunes asociadas con el desarrollo de APIs.</td>
    </tr>
     <tr>
      <th class="left-header" scope="row">Flask-SQLAlchemy</th>
      <td  colspan="3">Integra el poderoso sistema de mapeo objeto-relacional SQLAlchemy con Flask, facilitando la interacción con bases de datos SQL en aplicaciones web.</td>
    </tr>
    <tr>
      <th class="left-header" scope="row">Flask-WTF</th>
      <td  colspan="3">Proporciona integración con la extensión WTForms, simplificando la creación y validación de formularios en aplicaciones Flask.</td>
    </tr>
    <th class="left-header" scope="row">Flask-Login</th>
      <td  colspan="3">Facilita la gestión de la autenticación de usuarios y las sesiones en aplicaciones Flask, permitiendo la creación de sistemas de inicio de sesión de manera eficiente.</td>
    </tr>
     <tr>
      <th scope="row" class="left-header">Flask-SocketIO</th>
      <td  colspan="3">Agrega compatibilidad con WebSocket a Flask, lo que permite la implementación de comunicación bidireccional en tiempo real entre el servidor y el cliente.</td>
    </tr>
    <tr>
      <th scope="row" class="left-header">Flask-Admin</th>
      <td  colspan="3">Proporciona una interfaz de administración generada automáticamente para las aplicaciones Flask, facilitando la gestión de modelos de bases de datos y otros aspectos administrativos.</td>
    </tr>
    <tr>
      <th scope="row" class="left-header">Flask-Security</th>
      <td  colspan="3">Ofrece herramientas y utilidades adicionales para mejorar la seguridad en aplicaciones Flask, incluyendo funciones para la gestión de roles, autorización y protección contra ataques comunes.</td>
    </tr>
    <tr>
      <th scope="row" class="left-header">Flask-RESTPlus</th>
      <td  colspan="3">Similar a Flask-RESTful, esta extensión agrega características adicionales como documentación automática de la API mediante Swagger y funcionalidades avanzadas para facilitar la creación de APIs REST.</td>
    </tr>
    <tr>
      <th scope="row" class="left-header">Flask-CORS</th>
      <td  colspan="3">Permite el manejo de solicitudes CORS (Cross-Origin Resource Sharing) en aplicaciones Flask, lo que es esencial al construir APIs que deben ser consumidas por clientes en dominios diferentes.</td>
    </tr>
  </tbody>
</table>

Estas son solo algunas de las muchas extensiones disponibles para Flask. La comunidad activa de Flask sigue contribuyendo con nuevas extensiones y herramientas, lo que hace que Flask sea aún más flexible y adecuado para una variedad de aplicaciones y escenarios de desarrollo.

## [Instalación de Flask](https://flask.palletsprojects.com/en/3.0.x/installation/)
Para instalar Flask, puedes utilizar el administrador de paquetes de Python llamado **pip** (recuerda que solemos utilizar python3):

```bash
pip3 install Flask
```

Una vez que la instalación haya finalizado, puedes verificar que Flask esté instalado correctamente ejecutando el siguiente comando:

```bash
flask --version
```

Deberías ver la versión de Flask instalada en tu sistema.

¡Eso es todo! Ahora tienes Flask instalado en tu entorno de desarrollo. Puedes comenzar a construir aplicaciones web y APIs utilizando este framework.

## [Crear una primera aplicación](https://flask.palletsprojects.com/en/3.0.x/quickstart/)
Vamos a crear nuestra primera aplicación de Flask. Crea un archivo llamado **app.py** y agrega el siguiente código:

```{code}
from flask import Flask

# Crea una instancia de la aplicación Flask
app = Flask(__name__)

# Define una ruta para la página principal
@app.route('/')
def home():
    return '¡Hola, mundo! Esta es mi primera aplicación Flask.'

# Punto de entrada para la aplicación
if __name__ == '__main__':
    # Inicia la aplicación en modo de desarrollo
    app.run(debug=True)
```

En este código, creamos una aplicación Flask mínima con una sola ruta **('/')**. Cuando alguien accede a la página principal de la aplicación, se muestra el mensaje definido en la función **home()**.

Posteriormente, guarda el archivo y ejecuta deste tu terminal:

```bash
python app.py
```

o con el comando:

```bash
flask --app app run
```

Verás un mensaje indicando que la aplicación se está ejecutando en un servidor local. Abre tu navegador web y visita **http://localhost:5000/**. Deberías ver el mensaje "¡Hola, mundo!".


También podemos meter directamente código html tal y como se muestra a continuación:

```{code}
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"
```

Adicionalmente a esto podemos ejecutar la aplicación en modo debug para que nos muestre los errores que se producen:

```bash 
flask --app app run --debug
```

## Routing
Flask utiliza decoradores para asociar funciones con rutas específicas, lo que determina cómo responde la aplicación a las solicitudes del usuario.

A continuación, se muestra un ejemplo básico del enrutamiento en Flask:

```{code}
@app.route('/')
def home():
    return 'Página de inicio'

@app.route('/about')
def about():
    return 'Acerca de nosotros'
```

En este ejemplo, la función home() se asociará a la ruta '/' y la función about() a la ruta '/about'. Cuando un usuario accede a estas rutas en el navegador, Flask ejecuta la función correspondiente y devuelve el resultado como respuesta al navegador.

Adicionalmente, podemos incluir parámetros a las rutas utilizando ángulos **(< y >)** en los decoradores. Estos valores se pasan como argumentos a la función de vista. Ejemplo:

```{code}
@app.route('/user/<username>')
def show_user_profile(username):
    return f'Usuario: {username}'
```

En este caso, cualquier ruta que coincida con **/user/<username>** invocará la función show_user_profile(username) y pasará el valor de username como argumento.

Flask convertira automáticamente cualquier variable que coincida con los siguientes tipos:


<table class="table table-bordered my-table-border">
  <tbody>
    <tr>
      <th class="left-header" scope="row">string</th>
      <td  colspan="3">(predeterminado) acepta cualquier texto sin barra</td>
    </tr>
     <tr>
      <th class="left-header" scope="row">int</th>
      <td  colspan="3">Acepta enteros positivos.</td>
    </tr>
    <tr>
      <th class="left-header" scope="row">float</th>
      <td  colspan="3">Acepta números decimales positivos.</td>
    </tr>
    <th class="left-header" scope="row">path</th>
      <td  colspan="3">Como strings pero también acepta barras</td>
    </tr>
     <tr>
      <th scope="row" class="left-header">uuid</th>
      <td  colspan="3">Acepta strings de tipo uuid</td>
    </tr>
  </tbody>
</table>

Además de esto, puedes especificar métodos HTTP permitidos para una ruta y también asociar varias rutas a una sola función de vista. Ejemplo:

```{code}
@app.route('/contact', methods=['GET', 'POST'])
@app.route('/support', methods=['GET'])
def contact_or_support():
    if request.method == 'POST':
        return 'Formulario de contacto enviado'
    else:
        return 'Página de soporte'
```

En este ejemplo, la función contact_or_support() maneja las rutas /contact y /support con diferentes métodos HTTP.

## Escape de html con Flask
Flask proporciona una función llamada **escape()** que puedes usar para realizar el escape de HTML. Esta función se utiliza para convertir caracteres especiales en entidades HTML, evitando así posibles ataques de inyección de código.

Aquí hay un ejemplo de cómo usar la función escape() en una plantilla de Flask:

```{code}
from flask import Flask, render_template, escape

app = Flask(__name__)

@app.route('/')
def home():
    # Mensaje con contenido potencialmente peligroso
    mensaje_peligroso = '<script>alert("¡Esto es un ataque!");</script>'

    # Escape de HTML para evitar la ejecución de scripts maliciosos
    mensaje_escaped = escape(mensaje_peligroso)

    # Renderiza la plantilla y pasa el mensaje escapado
    return render_template('index.html', mensaje=mensaje_escaped)
```

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flask HTML Escaping</title>
</head>
<body>
    <h1>Mensaje Escapado:</h1>
    <p>{{ mensaje | safe }}</p>
</body>
</html>
```

En este ejemplo, el filtro safe se utiliza para indicar a Jinja que confíe en el contenido HTML y no lo escape nuevamente. Ten en cuenta que debes usar safe con precaución y asegurarte de que el contenido que estás marcando como seguro sea seguro de verdad, para evitar problemas de seguridad.

Al aplicar este enfoque, te aseguras de que cualquier contenido potencialmente peligroso que se incluya en la página no se ejecute como código JavaScript y, en cambio, se muestre como texto simple.