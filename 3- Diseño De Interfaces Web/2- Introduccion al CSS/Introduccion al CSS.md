# INTRODUCCIÓN AL CSS

## Introducción al Layout con CSS

### GRID

El layout de **GRID** es un tipo de layout que se usa en navegadores modernos para colocar las etiquetas HTML. Dispone de muchas opciones pero ahora solo vamos a ver lo mas básico.

- `display: grid;` Define al contenedor como un contenedor de grid, permitiendo que sus hijos se posicionen dentro de una cuadrícula.
- `grid-teplate-areas` Especifica un diseño basado en áreas con nombre. Cada área se representa con un identificador textual en un formato similar al de una cuadrícula. Las filas están separadas por saltos de línea, y las columnas se delimitan por los espacios entre las palabras.
  
  En este caso:
 ```css
  grid-template-areas:
  "cabecera cabecera cabecera cabecera cabecera"
  "lateral-izquierdo cuerpo cuerpo cuerpo lateral-derecho"
  "pie pie pie pie pie";
  ```

- `grid-area` Asigna un elemento hijo del grid a una de las áreas nombradas en `grid-template-areas`.

   Por ejemplo: 
 ```css
  .cabecera {
      grid-area: cabecera;
  }
 ```

   Esto indica que el elemento con la clase .cabecera ocupará el área llamada cabecera.

**Estructura general del diseño:**

- *Cabecera* ocupa toda la parte superior de la página.
- *Lateral-izquierdo* está en la parte izquierda de la segunda fila.
- *Cuerpo* ocupa la parte central de la segunda fila.
- *Lateral-derecho* está en la parte derecha de la segunda fila.
- *Pie* ocupa toda la parte inferior.

```html
<!DOCTYPE html>
<html>
    <head>
        <title>TODO supply a title</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <style>
            .contenedor {
                display: grid;
                grid-template-areas:
                  "cabecera cabecera cabecera cabecera cabecera"
                  "lateral-izquierdo cuerpo cuerpo cuerpo lateral-derecho"
                  "pie pie pie pie pie";
            }
 
            .cabecera {
                grid-area: cabecera;
            }
 
            .cuerpo {
                grid-area: cuerpo;
            }
 
            .lateral-izquierdo {
                grid-area: lateral-izquierdo;
            }
 
            .lateral-derecho {
                grid-area: lateral-derecho;
            }
 
            .pie {
                grid-area: pie;
            }
 
 
        </style>        
    </head>
 
    <body>
        <div class="contenedor">
            <div class="cabecera">CABECERA</div>
            <div class="lateral-izquierdo">IZQUIERDA</div>
            <div class="cuerpo">CUERPO</div>
            <div class="lateral-derecho">DERECHA</div>
            <div class="pie">PIE</div>
        </div>
    </body>
</html>
```

### FLEXBOX

Esto con **FLEXBOX** sería de la siguiente manera:

```html
<!DOCTYPE html>
<html>
    <head>
        <title>TODO supply a title</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <style>
            .contenedor {
                display: flex;
                flex-direction: column; /* Organiza las secciones en filas */
                height: 100vh; /* Altura completa de la ventana */
            }

            .fila {
                display: flex; /* Contenedor para organizar elementos en fila */
                flex: 1; /* Divide las filas proporcionalmente */
            }

            .cabecera {
                flex: 0.2; /* Ocupa menos espacio vertical */
                background-color: lightblue;
                text-align: center;
            }

            .lateral-izquierdo,
            .lateral-derecho {
                flex: 1; /* Ocupan espacio igual dentro de la fila */
                background-color: lightgray;
                text-align: center;
            }

            .cuerpo {
                flex: 3; /* Ocupa más espacio en la fila */
                background-color: lightgreen;
                text-align: center;
            }

            .pie {
                flex: 0.2; /* Ocupa menos espacio vertical */
                background-color: lightcoral;
                text-align: center;
            }
        </style>
    </head>
    <body>
        <div class="contenedor">
            <!-- Cabecera -->
            <div class="cabecera">CABECERA</div>

            <!-- Fila intermedia -->
            <div class="fila">
                <div class="lateral-izquierdo">IZQUIERDA</div>
                <div class="cuerpo">CUERPO</div>
                <div class="lateral-derecho">DERECHA</div>
            </div>

            <!-- Pie -->
            <div class="pie">PIE</div>
        </div>
    </body>
</html>
```


##### Visualmente se vería algo como:

```scss
CABECERA (ancho completo)
+-----------------------------------------------+

IZQUIERDA   |        CUERPO        | DERECHA
(estrecha)   (ancha)                (estrecha)

PIE (ancho completo)
+-----------------------------------------------+
```


## Reset CSS

Cada navegador tiene propiedades cuyos valores por defecto son distintos unos de otros.E s necesario tener un CSS que ponga los valores de esas propiedades siempre iguales para que no haya tanta diferencia entre navegadores.

Incluir en todos los proyectos los siguientes CSS:

- https://necolas.github.io/normalize.css/8.0.1/normalize.css
- https://meyerweb.com/eric/tools/css/reset/




