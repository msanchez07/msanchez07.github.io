# Base de datos
En Flask, el acceso a una base de datos generalmente se realiza a través de una extensión llamada [SQLAlchemy](https://www.sqlalchemy.org/), que es un popular ORM (Mapeo Objeto-Relacional) en Python. SQLAlchemy proporciona una forma de interactuar con la base de datos utilizando objetos y consultas en lugar de escribir SQL directamente.

En esta pequeña introducción que estamos ahciendo de Flask, no vamos a entrar en Alchemy, y vamos a optar por acceder de manera tradicional. Para ello, en función de la base de datos, va os a necesitar un tipo de conector u otro. Por ejemplo, puedes utilizar la extensión **sqlite3** que viene integrada con Python para bases de datos SQLite o **psycopg2** para bases de datos PostgreSQL:

```{code}
from flask import Flask, render_template
import sqlite3

app = Flask(__name__)

# Configuración de la ruta de la base de datos SQLite
app.config['DATABASE'] = 'mi_base_de_datos.db'

# Función para conectar a la base de datos
def conectar_bd():
    conexion = sqlite3.connect(app.config['DATABASE'])
    conexion.row_factory = sqlite3.Row
    return conexion

# Función para inicializar la base de datos
def inicializar_bd():
    with app.app_context():
        db = conectar_bd()
        with app.open_resource('esquema.sql', mode='r') as f:
            db.cursor().executescript(f.read())
        db.commit()

# Ruta de ejemplo para interactuar con la base de datos
@app.route('/')
def home():
    conexion = conectar_bd()
    cursor = conexion.cursor()

    # Ejemplo de creación de una tabla y una inserción
    cursor.execute('CREATE TABLE IF NOT EXISTS usuarios (id INTEGER PRIMARY KEY, nombre TEXT, email TEXT)')
    cursor.execute('INSERT INTO usuarios (nombre, email) VALUES (?, ?)', ('John Doe', 'john@example.com'))
    conexion.commit()

    # Ejemplo de consulta a la base de datos
    cursor.execute('SELECT * FROM usuarios')
    usuarios = cursor.fetchall()

    conexion.close()

    return render_template('index.html', usuarios=usuarios)

if __name__ == '__main__':
    app.run(debug=True)

```

En este ejemplo, se utiliza SQLite y se crea una tabla llamada usuarios. Luego, se inserta un usuario y se realiza una consulta para obtener todos los usuarios. La función **conectar_bd** se encarga de establecer la conexión a la base de datos.

Asegúrate de tener un archivo esquema.sql con el esquema de tu base de datos:

```sql
CREATE TABLE IF NOT EXISTS usuarios (
    id INTEGER PRIMARY KEY,
    nombre TEXT,
    email TEXT
);
```

Otra opción sería gestionar los accesos a la base de datos a través un fichero de configuración:

```{code}
import sqlite3

import click
from flask import current_app, g


def get_db():
    if 'db' not in g:
        g.db = sqlite3.connect(
            current_app.config['DATABASE'],
            detect_types=sqlite3.PARSE_DECLTYPES
        )
        g.db.row_factory = sqlite3.Row

    return g.db


def close_db(e=None):
    db = g.pop('db', None)

    if db is not None:
        db.close()
```

donde:

- **g**: Es un objeto llamado "context globals" en Flask que se utiliza para almacenar datos globales durante la solicitud. A diferencia de variables de sesión, los datos almacenados en g están disponibles solo durante el ciclo de vida de la solicitud y no persisten entre solicitudes.

- **current_app**: Es un objeto que proporciona acceso a la instancia de la aplicación Flask actual. Puede ser utilizado para acceder a la configuración de la aplicación y realizar operaciones relacionadas con la aplicación.
  
- **sqlite3.connect()**:  Establece una conexión con la base de datos.

- **sqlite3.Row**:  Indica a la conexión que devuelva las filas como diccionarios. Esto permite acceder a las columnas por su nombre.
  
- **close_db**: Cierra la conexión con la base de datos.


## Ejemplo de acceso a postgresql
Vamos a ver un ejemplo de acceso a la base de datos de tipo postgresql. Recuerda que previamente debes instalar los drivers de acceso:

```bash
pip3 install Flask psycopg2
```

A continuación veamos un ejempl de consulta e inserción de datos.

```{code}
from flask import Flask, render_template, request
import psycopg2

app = Flask(__name__)

# Configura las credenciales de tu base de datos PostgreSQL
db_params = {
    'dbname': 'tu_basededatos',
    'user': 'tu_usuario',
    'password': 'tu_contraseña',
    'host': 'localhost',
    'port': '5432'
}

# Ruta para mostrar los datos de la base de datos
@app.route('/')
def mostrar_datos():
    # Conéctate a la base de datos
    conn = psycopg2.connect(**db_params)
    cursor = conn.cursor()

    # Ejemplo: Selecciona todos los registros de una tabla llamada 'usuarios'
    cursor.execute("SELECT * FROM usuarios")
    #Devuelve un listado de tuplas con los datos
    registros = cursor.fetchall()

    # Cierra la conexión
    cursor.close()
    conn.close()

    return render_template('mostrar_datos.html', registros=registros)

# Ruta para agregar un nuevo usuario a la base de datos
@app.route('/agregar_usuario', methods=['POST'])
def agregar_usuario():
    if request.method == 'POST':
        # Obtiene los datos del formulario
        nombre = request.form['nombre']
        edad = request.form['edad']

        # Conéctate a la base de datos
        conn = psycopg2.connect(**db_params)
        cursor = conn.cursor()

        # Ejemplo: Inserta un nuevo usuario en la tabla 'usuarios'
        cursor.execute("INSERT INTO usuarios (nombre, edad) VALUES (%s, %s)", (nombre, edad))

        # Hace commit y cierra la conexión
        conn.commit()
        cursor.close()
        conn.close()

    # Redirige a la página principal después de agregar un usuario
    return mostrar_datos()

if __name__ == '__main__':
    app.run(debug=True)

```