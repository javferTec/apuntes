# COMUNICACIÓN ASÍNCRONA

La programación **asíncrona** es una técnica que **permite a tu programa iniciar una tarea de larga duración y seguir respondiendo a otros eventos mientras esa tarea se ejecuta**, en lugar de tener que esperar hasta que esa tarea haya terminado. Una vez que dicha tarea ha finalizado, tu programa presenta el resultado.

La comunicación asíncrona ofrece varias ventajas en el desarrollo web, entre las que podemos destacar:

- **Mejora la experiencia de usuario**
- **Aumenta la escalabilidad**
- **Simplifica el código**

Sin embargo, presenta una serie de problemas:

- Gestionar múltiples peticiones asíncronas puede llevarnos muchos problemas, al ser asíncrono cada petición acabará en un tiempo indeterminado y seguro que no acaban en el orden en que se lanzan.
- Podemos tener peticiones asíncronas que dependan de la finalización de otra.
- Podemos querer lanzar un conjunto de peticiones asíncronas y querer esperar a que todas hayan acabado para poder realizar acciones con todos los datos recibidos

Se usa en una amplia variedad de aplicaciones web, como por ejemplo:

- **Carga de datos**: Cuando un usuario carga una página web, se pueden cargar datos de forma asíncrona para evitar que la página se bloquee mientras se espera a que todos los datos estén disponibles.
- **Peticiones a APIs REST**: Las APIs REST se suelen consumir de forma asíncrona para obtener datos de servidores remotos.
- **Chat en tiempo real**: Las aplicaciones de chat en tiempo real utilizan la comunicación asíncrona para enviar y recibir mensajes de forma instantánea.
- **Juegos online**: Los juegos online necesitan una comunicación asíncrona para sincronizar las acciones de los jugadores en tiempo real.

JavaScript ofrece actualmente varios mecanismos para la comunicación asíncrona:

- **Callbacks**: es una función que se pasa como argumento a otra función y se ejecuta después de que la función principal termina su tarea, generalmente asincrónica.

- **Promesas**: es un objeto que representa un valor que puede estar disponible ahora, en el futuro, o nunca.

- **Async/await**: `async` es una palabra clave que se usa para declarar una función asincrónica, mientras que `await` se utiliza para pausar la ejecución de una función `async` hasta que una promesa se resuelva.

Pero, independientemente del mecanismo que utilicemos por debajo de él esta **AJAX**.

## AJAX

JavaScript Asíncrono + XML (AJAX) no es una tecnología por sí misma, es un término que describe un nuevo **modo de utilizar conjuntamente varias tecnologías existentes**. Esto incluye: HTML o XHTML, CSS, JavaScript, DOM, XML, XSLT, y lo más importante, el objeto XMLHttpRequest. 

Cuando estas tecnologías se combinan en un modelo AJAX, es posible lograr aplicaciones web capaces de actualizarse continuamente sin tener que volver a cargar la página completa. Esto crea aplicaciones más rápidas y con mejor respuesta a las acciones del usuario.

![[classic-web-app-communication-model.jpg]]

**XMLHttpRequest es un objeto de navegador incorporado que permite realizar solicitudes HTTP en JavaScript.**

### Funcionamiento del objeto XMLHttpRequest

El funcionamiento básico del objeto XMLHttpRequest es el siguiente: 

1. Crear el objeto: Crear objeto XMLHttpRequest.
```javascript
let xhr = new XMLHttpRequest();
```

2. Inicializar el objeto: Configurar la solicitud.
```javascript
xhr.open(method, URL, [async, user, password])
```

- **_method_** método HTTP. Por lo general "GET" o "POST".
- **_URL_** la URL de la petición
- **_async_** si se establece explícitamente en false, entonces la solicitud es síncrona
- **_user, password_** inicio de sesión y contraseña para la autenticación HTTP básica (si es necesario).

3. Enviar el objeto: Este método abre la conexión y envía la solicitud al servidor. GET y DELETE no tienen body, POST, PUT y PATCH si.
```javascript
xhr.send([body])
```

4. Esperar respuesta del servidor: Una vez enviada la petición el objeto XMLHttpRequest estará “escuchando” lo que va sucediendo con el estado de la petición, para ello utiliza los eventos del objeto xhr.

	- **_load_** cuando se completa la solicitud (incluso si el estado HTTP es como 400 o 500), y la respuesta se descarga completamente.
	```javascript
	xhr.onload = function() { 
		alert(`Loaded: ${xhr.status} ${xhr.response}`); 
	};
	```

	- **_error_** cuando no se pudo realizar la solicitud, por ejemplo, red inactiva o URL no válida.
	```javascript
	xhr.onerror = function() {
		alert(`Network Error`);	
	};
	```

5. Trabajar con la información recibida: Una vez que el servidor ha respondido, podemos recibir el resultado en las siguientes propiedades del objeto xhr:

	- **_status_** HTTP código de estado (un número): 200, 201, 404, 403 y así sucesivamente.
	
	- **_statusText_** Mensaje de estado HTTP (una cadena): generalmente OK para 200, Not Found para 404, Forbidden para, 403 etc.
	
	- **_response_** La respuesta del servidor, aquí es donde estará la información que nos manda el servidor. Existen diferentes formatos de respuesta del servidor. Podemos usar la propiedad `xhr.responseType` para establecer el formato de respuesta:
	
		- `""` (predeterminado): obtener como cadena 
		- `"text"` llega como string
		- `"arraybuffer"` llega como ArrayBuffer para datos binarios
		- `"blob"` usado para datos binarios 
		- `"document`" llega como documento XML (puede usar XPath y otros métodos XML), 
		- `"json"` llega como JSON (analizado automáticamente). _(ES EL HABITUAL)_


Una petición completa quedaría de la siguiente forma:
```javascript
let xhr = new XMLHttpRequest();
xhr.open(method, URL, [async, user, password])
xhr.responseType = 'json';
xhr.send([body])

xhr.onload = function() {
	alert(`Loaded: ${xhr.status} ${xhr.response}`);
};

//Error en petición
xhr.onerror = function() {
	alert(`Network Error`);
};
```

### Petición GET

Se utiliza para solicitar datos de una API sin enviar información adicional al servidor.

```javascript
const xhr = new XMLHttpRequest();
xhr.open("GET", "https://rickandmortyapi.com/api/character");

xhr.onload = function() {
    if (xhr.status == 200) {
        const personajes = JSON.parse(xhr.responseText);
        console.log(personajes);
    }
};
xhr.send();
```

### Petición DELETE

Se utiliza para eliminar un registro en el servidor.

```javascript
const url = "http://localhost:3000/articulos";

function deleteArticulo() {
    let id = prompt("Dime el id del articulo...");
    const xhr = new XMLHttpRequest();
    
    xhr.open("DELETE", `${url}/${id}`);
    
    xhr.onload = function() {
        if (xhr.status == 200) {
            console.log("El articulo se ha borrado");
        } else {
            console.log("ERROR. El articulo NO se ha borrado");
        }
    };
    
    xhr.send();
}
```

### Enviar datos al servidor: POST, PUT y PATCH

1. **POST**: Se utiliza para crear un nuevo registro en el servidor.
```javascript
const url = "http://localhost:3000/articulos";  
  
function postArticulo() {  
    let id = prompt("Dime el id del articulo...");  
    let nombre = prompt("Dime el nombre del articulo...");  
    let precio = parseInt(prompt("Dime el precio del articulo..."));  
    let articulo = JSON.stringify({"id": id, "nombre": nombre, "precio": precio});  
    const xhr = new XMLHttpRequest();  
    xhr.open("POST", url);  
    xhr.setRequestHeader('Content-Type', 'application/json; charset=utf-8');  
    xhr.send(articulo);  
    
    xhr.onload = function () {  
        if (xhr.status == 201) {  
            console.log("El articulo se ha insertado.");  
        } else {  
            console.log("ERROR. El articulo NO se ha insertado.");  
        }  
    };  
}
```

2. **PUT**: Se utiliza para modificar un registro existente en el servidor.
```javascript
const url = "http://localhost:3000/articulos";  
  
function putArticulo() {  
    let id = prompt("Dime el id del articulo a modificar...");  
    let nombre = prompt("Dime el nuevo nombre del articulo...");  
    let precio = parseInt(prompt("Dime el nuevo precio del articulo..."));  
    let articulo = JSON.stringify({"id": id, "nombre": nombre, "precio": precio});  
    const xhr = new XMLHttpRequest();  
    xhr.open("PUT", `${url}/${id}`);  
    xhr.setRequestHeader('Content-Type', 'application/json; charset=utf-8');  
    xhr.send(articulo);  
    
    xhr.onload = function () {  
        if (xhr.status == 200) {  
            console.log("El articulo ha sido modificado.");  
        } else {  
            console.log("ERROR. El articulo NO se ha modificado.");  
        }  
    };  
}
```

## Promesas

Usar `XMLHttpRequest` implica gestionar peticiones asíncronas mediante callbacks. En peticiones simples no hay ningún problema, pero si queremos hacer algo más complejo y necesitamos hacer peticiones anidadas, donde cada petición depende del resultado de la anterior, el código se vuelve complejo y difícil de mantener, dando lugar al "callback hell" o "pyramid of doom".

---

Pongamos un ejemplo:

 Si queremos obtener el precio de un artículo vendido por un proveedor, primero hacemos una petición GET para el proveedor y luego otra para el artículo.
 
Debido a la asincronía, la segunda petición debe lanzarse en el onload de la primera, lo que complica el código cuando hay varias peticiones en secuencia.

---

Para solucionar esto, ECMAScript 6 (ES6) introdujo las promesas para facilitar la gestión de código asíncrono.

**Una promesa es un objeto que representa el resultado de una operación asíncrona (éxito o fracaso).**

Las **CARACTERÍSTICAS** principales de las promesas son:

- **Asíncrona**: No bloquea la ejecución del código.
- **Finalización**: La promesa puede cumplirse (`resolve`) o rechazarse (`reject`). Un resolve indica éxito y un reject, error.

Sus **VENTAJAS** son:

- **Simplifican** el manejo de código asíncrono en operaciones que requieren esperar, como las peticiones a servidores.
- Permiten **encadenar operaciones** asíncronas en secuencia.
- Mejoran la **legibilidad** del código frente a los callbacks tradicionales.

Además tiene varios **ESTADOS**:

- **Pendiente**: Estado inicial.
- **Resuelta**: Promesa completada exitosamente.
- **Rechazada**: Promesa fallida.

Al lanzarse, la promesa está en estado "pendiente". Si se cumple, pasa a "resuelta" y se gestiona con `.then()`. Si falla, pasa a "rechazada" y se gestiona con `.catch()`.


### .then()

Es el método que nos permite gestionar la finalización de una forma correcta de la promesa.

```javascript
promise.then( function(result) { /* gestión resultados */ }) // NO HABITUAL
promise.then( result => { /* gestión resultados */ }) // HABITUAL
```

### .catch()

Es el método que nos permite gestionar la finalización con error de la promesa.

```javascript
promise.catch( function(error) { /* gestión error */ }) // NO HABITUAL
promise.catch( error => { /* gestión error */ }) // HABITUAL
```


### Fetch

`Fetch` es una API de JavaScript para realizar peticiones HTTP de forma asíncrona. Es el nuevo estándar en JavaScript para hacer peticiones web y reemplaza al objeto `XMLHttpRequest`.

Representa una serie de **VENTAJAS**:

- **Sencillez**: Su interfaz es fácil de usar, lo que hace que el código sea más claro y mantenible.
- **Promesas**: Usa promesas, lo que permite manejar el éxito o el error de una petición de manera elegante.
- **Flexibilidad**: Soporta diferentes métodos HTTP (GET, POST, PUT, DELETE, etc.), y permite personalizar encabezados y cuerpos de las peticiones.

`Fetch` se encarga de crear, configurar y enviar la petición HTTP y devuelve el resultado en una promesa. Los resultados se gestionan con los métodos `.then()` para el éxito y `.catch()` para el error, el cual se puede omitir ya que se usa solo cuando Fetch no puede realizar una solicitud a la API, como por ejemplo si no hay conexión de red o no se encuentra la URL..

La función `fetch()` acepta dos parámetros:
- **URL**: La URL a la que se envía la petición (obligatorio).
- **Opciones**: Configuración adicional de la petición, como el método HTTP (opcional).

```javascript
fetch('url', {})
	.then(response => {
		// Gestionamos la respuesta de la petición aqui
	})
	.catch(error => {
		// Si hay un error de red lo gestionamos aqui
	});
```

###  Petición GET

Realiza una petición `GET` a la URL proporcionada y gestiona el resultado.

```javascript
let url = 'http://localhost:3000/articulos';
fetch(url)
	.then(response => response.json()) // Convierte la respuesta a JSON
    .then(articulos => console.log(articulos)) // Muestra los datos
    .catch(error => console.log("Network error"));
```

   - **Descripción del objeto `Response`**:
     - `status`: Código HTTP (e.g., 200: éxito, 404: no encontrado).
     - `statusText`: Texto del estado HTTP (e.g., "OK", "Not Found").
     - `headers`: Encabezados de la respuesta.
     - `body`: Cuerpo de la respuesta, que puede ser texto, JSON, blob, etc.
     - `ok`: Booleano que indica si la petición fue exitosa.

   - **Control de errores**:
```javascript
let url = 'http://localhost:3000/articulos/5';
fetch(url)
    .then(response => {
        if (!response.ok) {
            throw new Error(`Error ${response.status} ${response.statusText}`);
        }
        return response.json();
    })
    .then(articulo => console.log(articulo))
    .catch(error => alert(error));
```

### Petición DELETE

 Elimina un recurso específico usando `DELETE`, indicando el ID del recurso en la URL.
 
```javascript
let url = 'http://localhost:3000/articulos/2';
fetch(url, { method: 'DELETE' })
    .then(response => {
       if (!response.ok) {
            throw new Error(`Error ${response.status} ${response.statusText}`);
        }
       return response.json(); // Normalmente devuelve un objeto vacío
   })
	.then(data => console.log("Artículo eliminado:", data))
	.catch(error => alert(error));
```

### Enviar Datos al Servidor (POST, PUT y PATCH)

   - **POST**: Inserta un nuevo recurso.
   
     Configura el encabezado `Content-Type` y convierte el objeto en cadena JSON usando `JSON.stringify`.
     
```javascript
let url = 'http://localhost:3000/articulos';
let id = prompt("Dime el id: ");
let nombre = prompt("Dime el nombre: ");
let precio = parseInt(prompt("Dime el precio: "));
let articuloNuevo = JSON.stringify({ "id": id, "nombre": nombre, "precio": precio });

let opciones = {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: articuloNuevo
};

fetch(url, opciones)
    .then(response => {
        if (!response.ok) {
            throw new Error(`Error ${response.status} ${response.statusText}`);
        }
        return response.json();
    })
    .then(articulo => console.log("Artículo insertado:", articulo))
    .catch(error => alert(error));
```

**PUT**: Modifica un recurso existente.

```javascript
let url = 'http://localhost:3000/articulos';
let id = prompt("Dime el id del registro a modificar: ");
let nombre = prompt("Dime el nuevo nombre: ");
let precio = parseInt(prompt("Dime el nuevo precio: "));
let articuloMod = JSON.stringify({ "id": id, "nombre": nombre, "precio": precio });

let opciones = {
    method: 'PUT',
    headers: { 'Content-Type': 'application/json' },
    body: articuloMod
};

fetch(`${url}/${id}`, opciones)
    .then(response => {
        if (!response.ok) {
            throw new Error(`Error ${response.status} ${response.statusText}`);
        }
        return response.json();
    })
    .then(articulo => console.log("Artículo modificado:", articulo))
    .catch(error => alert(error));
```

### Encadenamiento de promesas + Refactorización en Fetch

##### Encadenamiento de Promesas

Para realizar peticiones dependientes en secuencia, usamos el encadenamiento de promesas para evitar "callback hell". Primero, se realiza una petición `fetch` para obtener datos de un proveedor, y una vez obtenidos, con el `idArticulo` de ese proveedor, se realiza una segunda petición para obtener datos de un artículo específico. El encadenamiento permite manejar el flujo de peticiones en un código más limpio, ya que cada `.then()` devuelve una promesa al siguiente, y un solo `.catch()` gestiona todos los errores.

```javascript
let url = 'http://localhost:3000/';
let idProveedor = prompt("Dime el id del proveedor: ");

fetch(url + "proveedores/" + idProveedor)
    .then(response => {
        if (!response.ok) throw new Error(`Error proveedor ${response.status}: ${response.statusText}`);
        return response.json();
    })
    .then(p => {
        console.log(p);
        return fetch(url + "articulos/" + p.idArticulo);
    })
    .then(response => {
        if (!response.ok) throw new Error(`Error artículo ${response.status}: ${response.statusText}`);
        return response.json();
    })
    .then(a => console.log(a))
    .catch(error => alert(error));
```

##### Refactorización con Funciones Reutilizables

Para mejorar la reutilización, se encapsulan las peticiones `fetch` en funciones que retornan una promesa. Así, podemos hacer peticiones repetidas sin duplicar código, simplemente llamando a funciones con los parámetros necesarios. Ejemplo: `getArticulo()` para obtener un artículo, y `getProveedor()` para obtener un proveedor.

```javascript
function getArticulo(id) {
    return fetch(url + "articulos/" + id)
        .then(response => {
            if (!response.ok) throw new Error(`Error en artículo ${response.status}: ${response.statusText}`);
            return response.json();
        });
}

function getProveedor(id) {
    return fetch(url + "proveedores/" + id)
        .then(response => {
            if (!response.ok) throw new Error(`Error en proveedor ${response.status}: ${response.statusText}`);
            return response.json();
        });
}

// Uso de las funciones
getProveedor(1)
    .then(p => {
        console.log(p);
        return getArticulo(p.idArticulo);
    })
    .then(a => console.log(a))
    .catch(error => alert(error));
```

###### Función Genérica `getEntidad`

Se puede simplificar aún más creando una función genérica `getEntidad` que recibe como parámetros el tipo de entidad y el `id`. Esto permite obtener datos de cualquier entidad con una sola función.

```javascript
function getEntidad(entidad, id) {
    return fetch(url + entidad + "/" + id)
        .then(response => {
            if (!response.ok) throw new Error(`Error en ${entidad} con id ${id}: ${response.statusText}`);
            return response.json();
        });
}

// Ejemplo de uso
getEntidad("proveedores", 1)
    .then(p => {
        console.log(p);
        return getEntidad("articulos", p.idArticulo);
    })
    .then(a => console.log(a))
    .catch(error => alert(error));
```

Con esta estructura, el código es más modular y fácil de leer, además de ser adaptable para futuras modificaciones y ampliaciones.

### Async / Await

`async/await` es una forma simplificada de manejar promesas, que permite escribir código asíncrono de forma más secuencial. Algunos aspectos clave de `async/await` son:

- No se utiliza `.then()` para manejar el resultado de las promesas, sino que se espera directamente con `await`.

- No se dispone de un manejador `.catch()`, sino que los errores se gestionan con un bloque `try/catch`.

- Cambia el modelo de ejecución de no bloqueante a bloqueante, ya que `await` detiene la ejecución hasta que se resuelve la promesa.


Para obtener todos los artículos, el código podría verse así, aunque debe estar dentro de una función `async` para que `await` funcione.

```javascript
let url = 'http://localhost:3000/articulos';

async function getArticulos() {
    const response = await fetch(url);
    const articulos = await response.json();
    console.log(articulos);
}
```

Si queremos acceder a un artículo en concreto, podemos definir una función `async` que recibe un `id` como parámetro. Este código necesita gestionar errores, como un artículo no encontrado (404), para lo cual usamos un bloque `try/catch`.

```javascript
async function getArticulo(id) {
    try {
        const response = await fetch(url + "/" + id);
        if (!response.ok) throw new Error(`Error en artículo con id ${id}`);
        const articulo = await response.json();
        console.log(articulo);
    } catch (error) {
        console.log(error);
    }
}
```

###### Ejemplo de Petición Encadenada para Obtener Datos del Artículo que Vende un Proveedor

Para realizar una secuencia de peticiones donde primero obtenemos los datos de un proveedor y luego usamos el `idArticulo` del proveedor para obtener el artículo correspondiente, podemos utilizar `async/await` con un manejo de errores centralizado en `try/catch`.

```javascript
async function getArticuloProveedor() {
    let url = 'http://localhost:3000/';
    let idProveedor = prompt("Dime el id del proveedor: ");

    try {
        // Petición para obtener el proveedor
        let response = await fetch(url + "proveedores/" + idProveedor);
        if (!response.ok) throw new Error(`Error en proveedor con id ${idProveedor}`);
        let proveedor = await response.json();

        // Petición para obtener el artículo del proveedor
        response = await fetch(url + "articulos/" + proveedor.idArticulo);
        if (!response.ok) throw new Error(`Error en artículo con id ${proveedor.idArticulo}`);
        let articulo = await response.json();

        console.log(articulo);
    } catch (error) {
        console.log(error);
    }
}
```

1. **Primera Petición (Proveedor):** Realiza una solicitud `fetch` para obtener los datos de un proveedor. Si no se obtiene una respuesta satisfactoria (`ok`), se lanza un error.

2. **Segunda Petición (Artículo):** Con el `idArticulo` del proveedor obtenido en la primera solicitud, se realiza una segunda petición `fetch` para obtener los datos del artículo correspondiente.

3. **Manejo de Errores con `try/catch`:** Cualquier error en las peticiones, como respuestas no válidas, se gestiona en el bloque `catch`.

