Pasemos ahora a ver como es un servidor web integrado. Para entenderlo vamos a usar el lenguaje NodeJS como ejemplo y la librería que tendrá el servidor será Express.

- Instalar paquete express:

``` node
npm install express
```

- Ejemplo básico: Ejemplo Hello world. Crear el fichero "_index.js_" con el siguiente contenido.

``` node
#!/usr/bin/env node
 
const express = require('express')
const app = express()
const port = 8080
 
app.get('/', (request, response) => {
  response.send('Hello from Express!')
})
 
 
app.listen(port, (err) => {
  console.log(`server is listening on ${port}`)
})
```

Ahora debemos ejecutar el fichero index.js

``` node
node index.js
```

Y si navegamos a `http://localhost:8080` veremos el texto `"Hello from Express!"`

- Servir páginas estáticas:  Deberemos crear dentro del proyecto la carpeta "_HTML_" y ahí crear el fichero "_index.html_". Crear el fichero "_index.js_" con el siguiente contenido.

``` node
#!/usr/bin/env node
 
const express = require('express')
const app = express()
const port = 8080
 
app.get('/', (request, response) => {
  response.send('Hello from Express!')
})
app.use('/html', express.static(__dirname + '/html'));
 
 
app.listen(port, (err) => {
  console.log(`server is listening on ${port}`)
})
```

Ahora debemos ejecutar el fichero index.js

``` node
node index.js
```

Y si navegamos a `http://localhost:8080/html/index.html` veremos la página que hemos creado.