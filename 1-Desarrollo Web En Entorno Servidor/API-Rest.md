# API-REST

Cualquier aplicación web se basa en una arquitectura cliente-servidor, donde un servidor queda a la espera de conexiones de clientes, y los clientes se conectan a los servidores para solicitar ciertos recursos.

Estas comunicaciones se realizan mediante HTTP o HTTPS, donde el cliente solicita un recurso y el servidor intenta ofrecerlo.

Para solicitar un recurso se realiza mediante una URL, la cual consta de varias partes:

- El __protocolo__ empleado (HTTP o HTTPS)
- El __nombre de dominio__, que identifica al servidor y lo localiza en la red.
- La **ruta hacia el recurso solicitado**, dentro del propio servidor. Esta última parte también suele denominarse URI (identificador uniforme de recurso, o en inglés, Uniform Resource Identifier). Esta URI identifica unívocamente el recurso buscado entre todos los demás recursos que pueda albergar el servidor.

## Los servicios REST

REST son las siglas de *Representational State Transfer*, y designa un estilo de arquitectura de aplicaciones distribuidas, como las aplicaciones web. En un sistema REST, identificamos cada recurso a solicitar con una URI (identificador uniforme de recurso), y definimos un conjunto delimitado de comandos o métodos a realizar, que típicamente son:

- **GET**: para obtener resultados de algún tipo (listados completos o filtrados por alguna condición)
- **POST**: para realizar inserciones o añadir elementos en un conjunto de datos
- **PUT**: para realizar modificaciones o actualizaciones del conjunto de datos
- **DELETE**: para realizar borrados del conjunto de datos

Existen otros tipos de comandos o métodos, como por ejemplo **PATCH** (similar a PUT, pero para cambios parciales), **HEAD** (para consultar sólo el encabezado de la respuesta obtenida), etc. Nos centraremos, no obstante, en los cuatro métodos principales anteriores.

Por lo tanto, identificando el recurso a solicitar y el comando a aplicarle, el servidor que ofrece esta API REST proporciona una respuesta a esa petición. Esta respuesta típicamente viene dada por un mensaje en formato JSON o XML.

## Códigos de estado

- **Códigos 1XX**: representan información sobre una ==PETICIÓN INCOMPLETA==. No son muy habituales, pero se pueden emplear cuando la petición es muy larga, y se envía antes una cabecera para comprobar si se puede procesar dicha petición.

- **Códigos 2xx**: representan peticiones que se han podido atender satisfactoriamente, ==PETICIONES EXITOSAS==. El código más habitual es el 200, respuesta estándar para las peticiones que son correctas. Existen otras variantes, como el código 201, que se envía cuando se ha insertado o creado un nuevo recurso en el servidor (una inserción en una base de datos, por ejemplo), o el código 204, que indica que la petición se ha atendido bien, pero no se ha devuelto nada como respuesta.

- **Códigos 3xx**: son códigos de ==REDIRECCIÓN==, que indican que de algún modo la petición original se ha redirigido a otro recurso del servidor. Por ejemplo, el código 301 indica que el recurso solicitado se ha movido permanentemente a otra URL. El código 304 indica que el recurso solicitado no ha cambiado desde la última vez que se solicitó, por si se quiere recuperar de la caché local en ese caso.

- **Códigos 4xx**: indican un error por parte del ==CLIENTE==. El más típico es el error 404, que indica que estamos solicitando una URL o recurso que no existe. Pero también hay otros habituales, como el 401 (cliente no autorizado), o 400 (los datos de la petición no son correctos, por ejemplo, porque los campos del formulario no sean válidos).

- Códigos 5xx: indican un error por parte del ==SERVIDOR==. Por ejemplo, el error 500 indica un error interno del servidor, o el 504, que es un error de timeout por tiempo excesivo en emitir la respuesta.


## Endpoints

Un endpoint se refiere a una URL específica a la que se puede realizar una solicitud HTTP (GET, POST, PUT, DELETE…) para interactuar con un recurso o conjunto de recursos. Cada endpoint está asociado con una operación y puede devolver o manipular datos en formato JSON, XML u otro formato, según lo definido por la API.

Hay una serie de buenas prácticas a la hora de crear tus endpoints. Algunas de ellas son:

- Deberían siempre ser sustantivos, nunca verbos. El tipo de acción (el verbo) viene determinado por el método HTTP (GET, PUT, POST, DELETE…).
- Los recursos tienen que estar en plural, aunque se devuelva uno sólo.
- Para relacionar recursos, se van anidando recursos específicos en la URL.

Vamos a ver varios ejemplos para clarificar lo anterior:

- GET /books - Devuelve el listado de todos los libros.
- GET /books/12 - Devuelve el libro con id 12.
- POST /books - Crea un nuevo libro
- PUT /books/12 - Actualiza el libro con id 12.
- DELETE /books/12 - Elimina el libro con id 12
- GET /books/12/authors - Devuelve el listado de autores del libro con id 12.

