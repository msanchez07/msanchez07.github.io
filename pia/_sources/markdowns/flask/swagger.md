# Documentación de una api
La documentación de un API REST es un conjunto de información detallada que describe cómo interactuar y utilizar un servicio web basado en arquitectura REST. Este tipo de documentación es esencial para que los desarrolladores comprendan cómo consumir y trabajar con el API de manera efectiva.

Aquí hay algunos elementos clave que suele incluir la documentación de un API REST:

1. **Introducción y Descripción General**: Consiste en explicacar el propósito y funcionalidad del API y añadir información sobre los casos de uso típicos.

2. **Endpoint y URL**: Lista de todos los endpoints (puntos finales) disponibles con las URLs completas para cada endpoint.

3. **Métodos HTTP**: Especificación de los métodos HTTP admitidos por cada endpoint (GET, POST, PUT, DELETE, etc.). y la descripción de qué hace cada método en un contexto específico.

4. **Parámetros de la Solicitud**: Detalles sobre los parámetros que se deben incluir en una solicitud además de la información sobre si los parámetros son obligatorios o opcionales. Adicionalmente, se pueden ofrecer ejemplos de cómo incluir los parámetros en la solicitud.

5. **Cuerpo de la Solicitud (si es aplicable)**: Descripción de la estructura y formato del cuerpo de la solicitud en caso de métodos que requieran datos en el cuerpo (por ejemplo, en las solicitudes POST y PUT). Se añaden ejemplos de datos de solicitud válidos.

6. **Encabezados de Solicitud y Respuesta**: Especificación de los encabezados de solicitud que deben incluirse y la descripción de los encabezados de respuesta que se pueden esperar.

7. **Formato de Respuesta**: Descripción detallada del formato de la respuesta (generalmente en JSON o XML). Algunos ejemplos de respuestas exitosas y posibles mensajes de error.

8. **Códigos de Estado HTTP**: Lista de códigos de estado HTTP posibles y su significado con la indicación de cómo interpretar estos códigos en el contexto del API.

9. **Autenticación y Autorización**: Información sobre cómo autenticar las solicitudes al API con los detalles sobre los permisos necesarios para acceder a ciertos recursos.

10. **Ejemplos de Uso**: Ejemplos prácticos de cómo realizar solicitudes al API y casos de uso comunes con código de muestra.

11. **Notas de Versión**: Información sobre las versiones del API y cualquier cambio importante. Instrucciones sobre cómo migrar entre versiones, si es necesario.

## [Swagger](https://swagger.io/specification/)
Swagger es un conjunto de herramientas para diseñar, construir, documentar y consumir servicios web RESTful. El proyecto Swagger, ahora conocido como OpenAPI, proporciona un estándar para describir de manera uniforme las APIs RESTful. La especificación OpenAPI (anteriormente conocida como Swagger Specification) define un formato legible por máquina (en formato JSON o YAML) que permite describir la estructura de una API, incluidos los recursos disponibles, los métodos de operación, los parámetros de entrada, los formatos de respuesta y más.

El objetivo principal de Swagger/OpenAPI es mejorar la experiencia de desarrollo y la interoperabilidad al proporcionar una forma estándar y consistente de describir las API RESTful. Esto simplifica la comunicación entre los desarrolladores que crean servicios web y aquellos que los consumen, ya que todos pueden referirse a una documentación uniforme y clara. Además, la especificación OpenAPI es independiente del lenguaje de programación, lo que significa que se puede utilizar con APIs desarrolladas en diversos entornos.

Las principales componentes de Swagger/OpenAPI incluyen:

1. **Especificación OpenAPI (Swagger Specification)**: Este es el documento principal que describe la API. Puede estar en formato JSON o YAML y sigue un conjunto de reglas para definir la estructura y la información detallada sobre la API.

2. **Swagger UI**: Es una interfaz de usuario basada en web que interpreta y visualiza la especificación OpenAPI. Proporciona una documentación interactiva de la API, lo que facilita que los desarrolladores comprendan rápidamente cómo interactuar con los endpoints y qué esperar como respuesta. Además, Swagger UI permite realizar solicitudes directamente desde la interfaz, lo que facilita las pruebas.

3. **Swagger Editor**: Es una herramienta en línea que permite editar y validar archivos de especificación OpenAPI. Ofrece resaltado de sintaxis, autocompletado y validación en tiempo real, lo que facilita la creación y edición de la documentación de la API.

4. **Generadores de Código**: Con la especificación OpenAPI, es posible generar automáticamente código cliente y servidor en varios lenguajes de programación. Esto facilita la implementación de clientes que consuman el servicio API de manera más sencilla.

### Instalación de Swagger
Podemos instalar swagger en nuestro sistema solo tenemos que instalar el paquete swagger-ui:

```bash
pip3 install swagger-ui-py
```

Con esto ya tendríamos todo preparado para poder trabajar.

### Primeros pasos
Una vez instalado swagger, podemos empezar a definir su fichero de configuración:

```yaml
openapi: 3.0.0
info:
  title: Mi API
  version: 1.0.0
paths:
  /saludo:
    get:
      summary: Obtiene un saludo
      responses:
        '200':
          description: Respuesta exitosa
          content:
            application/json:
              example:
                mensaje: "¡Hola, mundo!"

```

Este es un ejemplo simple que define un endpoint /saludo con un método GET que devuelve un mensaje de saludo. Este proceso lo podemos simplificar utilizando el [swagger editor](https://editor.swagger.io/).

En el Swagger Editor, puedes ver la documentación generada automáticamente en la pestaña "Swagger UI". Aquí, puedes explorar la estructura de tu API, probar los endpoints y obtener información detallada sobre cómo interactuar con la API.

Una vez finalizado el proceso de editar tu fichero, guardalo en un archivo (con extensión .yaml o .json). Este archivo es esencial para compartir la especificación de tu API con otros desarrolladores y para generar código posteriormente.

Ahora, ya podemos agregar este fichero a nuestro proyecto:

```{code}
from swagger_ui import flask_api_doc
from flask import Flask

app = Flask(__name__)
flask_api_doc(app, config_path='./conf/test.yaml', url_prefix='/api/doc', title='API doc')


@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"

@app.route("/saludo")
def saludo():
    return "¡Hola, mundo!"

```

### Archivo de configuración
Swagger utiliza un archivo de configuración llamado Swagger/OpenAPI Specification (OAS) para describir y documentar APIs. Este archivo generalmente tiene formato JSON o YAML. A continuación, se presentan algunos de los parámetros comunes en un archivo de configuración Swagger:

1. **swagger**: La versión de Swagger que estás utilizando. Puede ser "2.0" para Swagger 2.0.

```yaml
swagger: "2.0"
```

2. **info**: Contiene información sobre la API, como el título, la versión y la descripción.

```yaml
info:
  version: "1.0.0"
  title: "Mi API"
  description: "Descripción de mi API"
```

3. **paths**: Define las rutas de la API, los métodos HTTP permitidos y las operaciones asociadas.

```yaml
paths:
  /usuarios:
    get:
      summary: "Obtener la lista de usuarios"
      description: "Devuelve una lista de todos los usuarios"
      responses:
        '200':
          description: "Operación exitosa"
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Usuario'
```

donde: 
- **/usuarios** es la ruta de la API. Indica que este bloque se aplica a las solicitudes que van a la ruta /usuarios.

- **get**  indica que este bloque se aplica a las solicitudes HTTP GET a la ruta /usuarios.

- **summary** proporciona un resumen breve y descriptivo de lo que hace esta operación (endpoint).

- **description** proporciona una descripción más detallada de la operación.

- **responses** define las respuestas que puede devolver la operación. En este caso, hay una respuesta para el código de estado HTTP 200.

- **content** indica el tipo de contenido que se espera en la respuesta. En este caso, se espera que la respuesta tenga el tipo de contenido "application/json".

- **schema** define el esquema (schema) del cuerpo de la respuesta. En este caso, se espera un array de objetos, donde cada objeto sigue el esquema definido en #/components/schemas/Usuario.



4. **components/schemas**: Define los modelos de datos utilizados en la API.

```yaml
components:
  schemas:
    Usuario:
      type: object
      properties:
        id:
          type: integer
        nombre:
          type: string
```

- **components/schemas** se utiliza para definir modelos de datos.
- **Usuario** es el nombre del modelo.
- **type: object** indica que el modelo es un objeto.
- **properties** define las propiedades del objeto, en este caso, id y nombre.

esto posteriormente lo podriamos utilizar de la siguiente forma:

```yaml
paths:
  /usuarios:
    get:
      summary: "Obtener la lista de usuarios"
      description: "Devuelve una lista de todos los usuarios"
      responses:
        '200':
          description: "Operación exitosa"
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Usuario'
```

El uso de **$ref: '#/components/schemas/Usuario'** indica que estamos haciendo referencia al esquema (schema) definido para Usuario.

5. **parameters**: Define los parámetros que se pueden pasar en las solicitudes.

```yaml
paths:
  /usuarios/{usuarioId}:
    parameters:
      - name: usuarioId
        in: path
        description: "ID del usuario"
        required: true
        type: integer
        format: int64
```

donde: 

- **/usuarios/{usuarioId}** es la ruta de la API que incluye un parámetro de ruta llamado usuarioId. Esto indica que este bloque se aplica a solicitudes que van a rutas como /usuarios/123, donde 123 es un valor específico para usuarioId.

- **parameters** es una lista de parámetros que puede tomar la operación en la ruta /usuarios/{usuarioId}.

  - **name**: usuarioId especifica el nombre del parámetro.

  - **in**: path indica que este es un parámetro de ruta.

  - **description**: "ID del usuario" proporciona una descripción del propósito del parámetro.

  - **required**: true indica que este parámetro es obligatorio.

  - **schema** define el esquema del parámetro. En este caso, se espera un valor de tipo entero (integer) con el formato de un entero de 64 bits (int64).


6. **responses**: Define las respuestas que la API puede devolver.

```yaml
paths:
  /usuarios:
    get:
      responses:
        200:
          description: "Operación exitosa"
          schema:
            type: array
            items:
              $ref: "#/definitions/Usuario"
```

- **/usuarios** es la ruta de la API y get indica que este bloque se aplica a las solicitudes HTTP GET a la ruta /usuarios.

- **responses** define las respuestas que puede devolver la operación.

  - **'200'** es el código de estado HTTP. En este caso, 200 indica que la operación se completó con éxito.

  - **description**: "Operación exitosa" proporciona una descripción del significado de la respuesta con el código de estado 200.

  - **content** indica el tipo de contenido que se espera en la respuesta. En este caso, se espera que la respuesta tenga el tipo de contenido "application/json".

  - **schema** define el esquema del cuerpo de la respuesta. En este caso, se espera un array de objetos, donde cada objeto sigue el esquema definido en #/components/schemas/Usuario.