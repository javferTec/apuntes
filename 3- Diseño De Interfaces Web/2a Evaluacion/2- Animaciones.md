
- **Transformaciones:**  
    Aplicar cambios espaciales a un elemento HTML (mover, rotar, escalar, distorsionar).  
    Se usan con la propiedad CSS `transform`.
- **Transiciones:**  
    API de CSS para suavizar cambios (por ejemplo, en estados `:hover`, `:focus`, etc.).  
    Se definen mediante la propiedad `transition`.
- **Animaciones:**  
    API de CSS más compleja para animar propiedades (movimiento, colores, opacidad, etc.).  
    Se definen en dos partes: los _fotogramas_ con `@keyframes` y los parámetros con la propiedad `animation`.  
    (En ocasiones se utiliza el término “animaciones” para referirse en general a cualquier movimiento en pantalla).

# Transformaciones

La propiedad `transform` permite:

- **Mover:** `translate(x, y)`, `translateX(n)`, `translateY(n)`
- **Escalar:** `scale(x, y)`, `scaleX(n)`, `scaleY(n)`
- **Rotar:** `rotate(angle)`
- **Distorsionar (skew):** `skew(x-angle, y-angle)`, `skewX(angle)`, `skewY(angle)`

**Ejemplos:**

Mover el elemento 50px en X y 100px en Y:

```css
div {
  transform: translate(50px, 100px);
}
```

Rotar el elemento 20 grados:

```css
div {
  transform: rotate(20deg);
}
```

Hacer el doble de grande en X y triple en Y:

```css
div {
  transform: scale(2, 3);
}
```

Hacer la mitad de grande en ambos ejes:

```css
div {
  transform: scale(0.5, 0.5);
}
```

Distorsionar el elemento 20° en X y 10° en Y:

```css
div {
  transform: skew(20deg, 10deg);
}
```

Aplicar varias transformaciones a la vez:

```css
div {
  transform: translate(50px, 100px) rotate(20deg);
}
```

Además, CSS permite **transformaciones 3D**:

- `translate3d(x,y,z)`, `translateZ(z)`, etc.
- `scale3d(x,y,z)`, `rotate3d(x,y,z,angle)`, `perspective(n)`

### Origen de la transformación

La propiedad `transform-origin` especifica el punto desde el que se aplica la transformación (por defecto, el centro).

Ejemplo, rotar respecto al centro (por defecto):

```css
.cuadrado--rotate-centro {
  transform: rotate(360deg);
  transform-origin: 50% 50%;
}
```

Rotar respecto a la esquina superior izquierda:

```css
.cuadrado--rotate-esquina-superior-izquierda {
  transform: rotate(360deg);
  transform-origin: 0 0;
}
```

#### Ejemplo completo con transiciones

```html
<!DOCTYPE html>
<html>
  <head>
    <title>transform-origin</title>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <style>
 
    </style>
 
    <style>
        .l-center {
            display: grid;
            place-items: center;
            width: 100%;
            height: 50vw;
        }
 
        .c-cuadrado {
            border: 1px solid red;
            background: lightpink;
            width:200px;
            height: 200px;
            transition: transform 4s;
            transform-origin: 0 0;
        }
 
        .c-cuadrado:hover {
            transform: rotate(360deg);
        }
 
    </style>
  </head>
 
  <body>
        <div class="l-center" >
          <div class="c-cuadrado">Hola mundo</div>
        </div>
  </body>
</html>
```

---
# Transiciones

Las transiciones suavizan cambios en estados como `:hover` o `:focus`.  
**Ejemplo sin transición:**

```html
<!DOCTYPE html>
<html>
    <head>
      <style>
        .c-button {
          padding: 10px 20px 10px 20px;
          background-color: #ffffff;
          border: 1px solid #bbd4f7;
          border-radius: 4px;
          cursor: pointer;
        }
         
        .c-button:hover {
          background-color: #deebfc;
          box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
        }
      </style>
    </head>
    <body>
      <button class="c-button">Aceptar</button>
    </body>
</html>
```

El efecto es brusco al cambiar de estilos. Para suavizarlo se añade `transition`:

```html
<!DOCTYPE html>
<html>
    <head>
      <style>
        .c-button {
          padding: 10px 20px 10px 20px;
          background-color: #ffffff;
          border: 1px solid #bbd4f7;
          border-radius: 4px;
          cursor: pointer;
          transition: background-color 1s, box-shadow 1s;
        }
         
        .c-button:hover {
          background-color: #deebfc;
          box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
        }
      </style>
    </head>
    <body>
      <button class="c-button">Aceptar</button>
    </body>
</html>
```

La sintaxis de `transition` es:

```
transition: propiedadCSS duracion timing-function retardo;
```

- **propiedadCSS:** La propiedad a transicionar.
- **duracion:** Tiempo de transición (ej. `1s`).
- **timing-function:** Velocidad de la transición (valores como `linear`, `ease`, `ease-in`, etc.).
- **retardo:** Tiempo antes de iniciar la transición (recomendable usar al menos `0.3s` en hover).

También se pueden definir por separado:

```css
transition-property: width;
transition-duration: 3s;
transition-timing-function: ease-in-out;
transition-delay: 2s;
```

---

# Animaciones

Las animaciones son similares a las transiciones pero más potentes y, a veces, se controlan desde JavaScript.  
Se componen de dos partes:

1. **Definición con `@keyframes`:**  
    Se especifican los fotogramas (ej. 0%, 50%, 100%) y los estilos en cada uno.
2. **Parámetros de la animación:**  
    Se aplican con la propiedad `animation` (o sus propiedades individuales).

**Ejemplo: Cuadrado giratorio que cambia de color**

```html
<!DOCTYPE html>
<html>
    <head>
        <style>
            .c-cuadrado {
              width: 100px;
              height: 100px;
              background-color: #bbd4f7;
              border-radius: 4px;
            }
             
            .c-cuadrado--girar {
              animation-name: animacion-girar;
              animation-duration: 3s;
            }
             
            @keyframes animacion-girar {
              0% {
                transform: rotate(0deg);
                background-color: #bbd4f7;
              }
               
              50% {
                transform: rotate(360deg);
                background-color: #1C4673;
              }
               
              100% {
                transform: rotate(0deg);
                background-color: #bbd4f7;
              }  
            }
        </style>
    </head>
    <body>
        <div style="padding:200px">
            <div id="cuadrado1" class="c-cuadrado c-cuadrado--girar">Hola</div>
        </div>
    </body>
</html>
```

### Propiedades de Animación

- **animation-name:** Nombre de la animación (nombre definido en `@keyframes`).
- **animation-duration:** Duración (ej. `3s`).
- **animation-timing-function:** Velocidad (valores: `linear`, `ease`, `ease-in`, etc.).
- **animation-delay:** Retardo antes de iniciar.
- **animation-iteration-count:** Número de repeticiones (`infinite` para repetir sin fin).
- **animation-direction:** Dirección de la animación (`normal`, `reverse`, `alternate`, `alternate-reverse`).
- **animation-fill-mode:** Estilos aplicados antes o después de la animación (`none`, `forwards`, `backwards`, `both`).
- **animation-play-state:** Estado inicial (`running` o `paused`).
- **animation:** Propiedad shorthand que agrupa todas las anteriores.

### Reiniciar la animación con JavaScript

Para volver a ejecutar una animación se puede quitar y volver a agregar la clase CSS (se usa un pequeño `setTimeout` para forzar el reinicio):

```js
function animar() {
    var cuadradoElement = document.getElementById("cuadrado1");
    cuadradoElement.classList.remove("c-cuadrado--girar");
    setTimeout(function() {
        cuadradoElement.classList.add("c-cuadrado--girar");
    }, 10);
}
```

### Animaciones Simétricas

Si se desea que la animación “vuelva” al estado inicial sin definir fotogramas de ida y vuelta, se puede usar:

- `animation-iteration-count: 2;` (dos repeticiones)
- `animation-direction: alternate;` (la segunda reproducción en sentido inverso)

**Ejemplo:**

```css
.c-cuadrado--girar {
  animation-name: animacion-girar;
  animation-duration: 1.5s;
  animation-iteration-count: 2;
  animation-direction: alternate;
}
 
 
@keyframes animacion-girar {
  0% {
    transform: rotate(0deg);
    background-color: #bbd4f7;
  }
   
  100% {
    transform: rotate(360deg);
    background-color: #1C4673;
  } 
}
```

