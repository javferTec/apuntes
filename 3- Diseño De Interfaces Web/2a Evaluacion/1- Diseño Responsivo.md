El **diseño responsivo** es una técnica de diseño web que permite que una página se adapte automáticamente al tamaño de la pantalla y al dispositivo desde el que se accede.

# Responsivo vs Adaptativo

Hacer un diseño responsivo es que la misma página se adapte a distintos tamaños de pantalla. Hacer un diseño adaptativo es hacer páginas distintas según el tamaño de la pantalla.

# Viewport

Añadir a todas las páginas la siguiente linea en el `<head>` del HMTL. Con esto se consigue que la página tenga el tamaño del dispositivo, ya que sino se pone , el dispositivo podría hacer que la página se haga mas grande y crear barras de desplazamiento.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

# Unidades

## viewport

Podemos hacer ciertos tamaños que sean en función del tamaño de la pantalla. Para ello se usan las unidades como `vw` o `vh` que hacen referencia al tamaño de la pantalla.

- `vh` Es la altura de la ventana. Un valor de 1vh es igual al 1% del alto.
- `vw` Es el ancho de la ventana. Un valor de 1vw es igual al 1% del ancho.
- `vmin` Mínimo entre el ancho y el alto. Es la dimensión más pequeña de la ventana. Si el alto de la ventana gráfica es menor que el ancho, el valor de 1vmin será igual al 1% de la altura. De manera similar, si el ancho es menor que la altura, el valor de 1vmin será igual al 1% del ancho.
- `vmax` Máximo entre el ancho y el alto. Es la dimensión más grande de la ventana. Si el alto de la ventana gráfica es mayor que el ancho, el valor de 1vmin será igual al 1% de la altura. De manera similar, si el ancho es mayor que la altura, el valor de 1vmin será igual al 1% del ancho.

## rem

La unidad `rem` hace referencia al tamaño de fuente del HTML. El tamaño en píxeles se obtiene de multiplicar el valor de `rem` por el tamaño de la fuente de la página.

## em

La unidad `em` hace referencia al tamaño de fuente del elemento donde está. El tamaño en píxeles se obtiene de multiplicar el valor de `em` por el tamaño de la fuente de ese elemento.

# Cálculos en CSS

## 1. Introducción a `clamp()`

La función `clamp()` en CSS permite definir un valor que se encuentra entre un mínimo y un máximo, ajustándose dinámicamente en función del ancho de la pantalla.

La sintaxis es:

```css
clamp(min, preferred, max)
````

- **min:** Valor mínimo (por ejemplo, `12px`).
- **preferred:** Valor dinámico (por ejemplo, `2.1621622vw + 7.02702694px`).
- **max:** Valor máximo (por ejemplo, `20px`).

_Ejemplo:_

```css
font-size: clamp(12px, 2.1621622vw + 7.02702694px, 20px);
```

---

## 2. Modelo Lineal para Valores Dinámicos

Queremos que el valor de una propiedad (por ejemplo, `font-size`) varíe de forma lineal según el ancho de la pantalla. Para ello, expresamos el valor de la propiedad de la siguiente forma:

$$
valor(w)=A⋅w100+B\text{valor}(w) = A \cdot \frac{w}{100} + B
$$
donde:

- ww es el ancho de la pantalla en píxeles.
- AA es el factor de escala que se aplicará a cada 1vw (1vw = 1% del ancho de la pantalla).
- BB es el desplazamiento (offset) en píxeles.

Queremos que se cumplan las siguientes condiciones:

1. Para $$w=wlowerw = w_{\text{lower}}$$ (ancho mínimo), se obtenga el valor mínimo:
    
    $$A⋅wlower100+B=minValueA \cdot \frac{w_{\text{lower}}}{100} + B = \text{minValue}$$
2. Para $$w=wupperw = w_{\text{upper}}$$ (ancho máximo), se obtenga el valor máximo:
    
    $$A⋅wupper100+B=maxValueA \cdot \frac{w_{\text{upper}}}{100} + B = \text{maxValue}$$

---

## 3. Derivación de la Fórmula

### Paso 1: Calcular la Pendiente AA

Dadas las dos ecuaciones:

1. $$A⋅wlower100+B=minValueA \cdot \frac{w_{\text{lower}}}{100} + B = \text{minValue}$$
2. $$A⋅wupper100+B=maxValueA \cdot \frac{w_{\text{upper}}}{100} + B = \text{maxValue}$$

Restamos la primera ecuación de la segunda para eliminar BB:

$$A⋅(wupper−wlower100)=maxValue−minValueA \cdot \left( \frac{w_{\text{upper}} - w_{\text{lower}}}{100} \right) = \text{maxValue} - \text{minValue}$$

Despejando AA:

$$A=(maxValue−minValue)⋅100wupper−wlowerA = \frac{(\text{maxValue} - \text{minValue}) \cdot 100}{w_{\text{upper}} - w_{\text{lower}}}$$

> **Nota:** Este AA es la pendiente que se usará en la parte de `vw`.

### Paso 2: Calcular el Coeficiente de Posición BB

Usando la primera ecuación:

$$A⋅wlower100+B=minValueA \cdot \frac{w_{\text{lower}}}{100} + B = \text{minValue}$$

Despejamos BB:

$$B=minValue−A⋅wlower100B = \text{minValue} - A \cdot \frac{w_{\text{lower}}}{100}$$

> **Nota:** BB es el desplazamiento (offset) en píxeles.

---

## 4. Ejemplo Práctico

Supongamos que queremos configurar el `font-size` con las siguientes condiciones:

- $$wlower=230 pxw_{\text{lower}} = 230\,\text{px}$$
- $$wupper=600 pxw_{\text{upper}} = 600\,\text{px}$$
- $$minValue=12 px\text{minValue} = 12\,\text{px}$$
- $$maxValue=20 px\text{maxValue} = 20\,\text{px}$$

### Cálculo de la Pendiente AA:

$$A=(20−12)⋅100600−230=8⋅100370≈2.1621622A = \frac{(20 - 12) \cdot 100}{600 - 230} = \frac{8 \cdot 100}{370} \approx 2.1621622$$

### Cálculo del Coeficiente BB:

$$B=12−2.1621622⋅230100=12−2.1621622⋅2.3≈12−4.975≈7.02702694B = 12 - 2.1621622 \cdot \frac{230}{100} = 12 - 2.1621622 \cdot 2.3 \approx 12 - 4.975 \approx 7.02702694$$

Con estos cálculos, la función lineal es:

$$valor(w)=2.1621622 vw+7.02702694 px\text{valor}(w) = 2.1621622\,\text{vw} + 7.02702694\,\text{px}$$

Y el CSS queda:

```css
font-size: clamp(12px, 2.1621622vw + 7.02702694px, 20px);
```

---

## 5. Función en Sass

Para automatizar estos cálculos, se puede crear una función en **Sass** que genere el valor de `clamp()`:

```scss
@function calcular-clamp($min-value, $max-value, $min-width, $max-width) {
  // Calcula la pendiente (valor en vw)
  $pendiente: (($max-value - $min-value) / ($max-width - $min-width)) * 100;

  // Calcula el coeficiente de posición (valor en px)
  $coef-posicion: $min-value - ($pendiente / 100 * $min-width);

  // Retorna el valor clamp con formato CSS
  @return clamp(#{$min-value}px, #{$pendiente}vw + #{$coef-posicion}px, #{$max-value}px);
}

// Ejemplo de uso:
.c-titulo {
  font-size: calcular-clamp(12, 20, 230, 600);
}
```

### Explicación de la función:

- **Parámetros:**
    
    - `$min-value`: Valor mínimo (ej. 12).
    - `$max-value`: Valor máximo (ej. 20).
    - `$min-width`: Ancho de pantalla mínimo (ej. 230).
    - `$max-width`: Ancho de pantalla máximo (ej. 600).
- **Cálculos:**
    
    - **Pendiente:**
        
        $pendiente=(maxValue−minValue)⋅100wupper−wlower\text{\$pendiente} = \frac{(\text{maxValue} - \text{minValue}) \cdot 100}{w_{\text{upper}} - w_{\text{lower}}}
    - **Coeficiente:**
        
        $coef-posicion=minValue−$pendiente100⋅wlower\text{\$coef-posicion} = \text{minValue} - \frac{\text{\$pendiente}}{100} \cdot w_{\text{lower}}
- **Resultado:** Se retorna un `clamp()` formateado para CSS.
    

---

## 6. Resumen

1. **Modelo Lineal:**  
    Se expresa el valor dinámico como:
    
    $$valor(w)=A⋅w100+B\text{valor}(w) = A \cdot \frac{w}{100} + B$$
2. **Derivación de AA:**
    
    $$A=(maxValue−minValue)⋅100wupper−wlowerA = \frac{(\text{maxValue} - \text{minValue}) \cdot 100}{w_{\text{upper}} - w_{\text{lower}}}$$
3. **Derivación de BB:**
    
    $$B=minValue−A⋅wlower100B = \text{minValue} - A \cdot \frac{w_{\text{lower}}}{100}$$
4. **Ejemplo Práctico:**  
    Con $$wlower=230w_{\text{lower}} = 230, wupper=600w_{\text{upper}} = 600, minValue=12\text{minValue} = 12 y maxValue=20\text{maxValue} = 20:$$
    
    - $$A≈2.1621622A \approx 2.1621622$$
    -$$ B≈7.02702694B \approx 7.02702694$$
        
    - CSS:
        ```css
        font-size: clamp(12px, 2.1621622vw + 7.02702694px, 20px);
        ```
        
5. **Función en Sass:**  
    La función `calcular-clamp()` automatiza estos cálculos para generar el valor `clamp()` en CSS.

# Imágenes

Hay muchas opciones al respecto de las imágenes responsivas. La técnica consiste principalmente en usar una imagen u otra en función de:

- Ancho o alto del dispositivo
- Pixel-ratio del dispositivo
- Tipos soportados por el navegador.

```html
<picture>
  <source media="(min-width: 900px)" srcset="https://logongas.es/lib/exe/fetch.php?media=responsive-large.jpg" />
  <source media="(min-width: 500px)" srcset="https://logongas.es/lib/exe/fetch.php?media=responsive-medium.jpg" />
  <img src="https://logongas.es/lib/exe/fetch.php?media=responsive-small.jpg" alt="Responsive image" />
</picture>
```

# Tablas

Para hacer tablas responsivas, realmente lo único que podemos hacer es que haya barras de Scroll. Para eso ponemos un div sobre la tabla con la propiedad `overflow: auto;`

```html
<html>
    <head>
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <style>
            .c-table {
              overflow: auto;
            }
            .c-table__head {
               
            }
            .c-table__head--min-width-1 {
              min-width: 100px;
            }
            .c-table__head--min-width-2 {
              min-width: 150px;
            }
            .c-table__head--min-width-3 {
              min-width: 200px;
            }
            .c-table__head--max-width-1 {
              max-width: 100px;  
            }
            .c-table__head--max-width-2 {
              max-width: 150px;  
            }
            .c-table__head--max-width-3 {
              max-width: 200px;  
            }
 
            .c-table__head--width-1 {
              width: 100px;
              min-width: 100px;  
            }
            .c-table__head--width-2 {
              width: 150px;
              min-width: 150px;  
            }
            .c-table__head--width-3 {
              width: 200px;
              min-width: 200px;  
            }
        </style>
    </head>
    <body>
        <h1 >Ejemplo de tablas responsivas</h1>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
 
        <div class="c-table">
            <table>
            <thead>
              <tr>
                <th class="c-table__head c-table__head--min-width-2 c-table__head--max-width-3">Author</th>
                <th class="c-table__head c-table__head--min-width-2 c-table__head--max-width-3 ">Title</th>
                <th class="c-table__head c-table__head--min-width-1 c-table__head--max-width-2">Year</th>
                <th class="c-table__head c-table__head--width-3">ISBN-13</th>
                <th class="c-table__head c-table__head--width-2">ISBN-10</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Miguel De Cervantes</td>
                <td>The Ingenious Gentleman Don Quixote of La Mancha</td>
                <td>1605</td>
                <td>9783125798502</td>
                <td>3125798507</td>
              </tr>
              <tr>
                <td>Gabrielle-Suzanne Barbot de Villeneuve</td>
                <td lang="fr">La Belle et la Bête</td>
                <td>1740</td>
                <td>9781910880067</td>
                <td>191088006X</td>
              </tr>
              <tr>
                <td>Sir Isaac Newton</td>
                <td>The Method of Fluxions and Infinite Series: With Its Application to the Geometry of Curve-lines</td>
                <td>1763</td>
                <td>9781330454862</td>
                <td>1330454863</td>
              </tr>
              <tr>
                <td>Mary Shelley</td>
                <td>Frankenstein; or, The Modern Prometheus</td>
                <td>1818</td>
                <td>9781530278442</td>
                <td>1530278449</td>
              </tr>
              <tr>
                <td>Herman Melville</td>
                <td>Moby-Dick; or, The Whale</td>
                <td>1851</td>
                <td>9781530697908</td>
                <td>1530697905</td>
              </tr>
              <tr>
                <td >Emma Dorothy Eliza Nevitte Southworth</td>
                <td>The Hidden Hand</td>
                <td>1888</td>
                <td>9780813512969</td>
                <td>0813512964</td>
              </tr>
              <tr>
                <td>F. Scott Fitzgerald</td>
                <td>The Great Gatsby</td>
                <td>1925</td>
                <td>9780743273565</td>
                <td>0743273567</td>
              </tr>
              <tr>
                <td>George Orwell</td>
                <td>Nineteen Eighty-Four</td>
                <td>1948</td>
                <td>9780451524935</td>
                <td>0451524934</td>
              </tr>
              <tr>
                <td>Nnedi Okorafor</td>
                <td>Who Fears Death</td>
                <td>2010</td>
                <td>9780756406691</td>
                <td>0756406692</td>
              </tr>
            </tbody>
        </table>
    </div>
 
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
     
    </body>
 
</html>
```

# CSS Media Queries

Permiten tener un CSS distinto según el tamaño de la pantalla. Como vemos para cada resolución se usa un CSS distinto y por lo tanto el tamaño es distinto según la resolución.

```html
.c-titulo {
    font-size: 40px;
}
 
  
@media (min-width: 576px) {
    .c-titulo {
        font-size: 50px;
    }
}
  
@media (min-width: 768px) {
    .c-titulo {
        font-size: 55px;
    }
}
  
@media (min-width: 992px) {
    .c-titulo {
        font-size: 70px;
    }
}

<p class="c-titulo">Hola mundo</p>
```

# Arquitectura responsiva

Pasemos ahora a ver como poder hacer las cosas responsivas con una simple arquitectura.

En el ejemplo por defecto el tamaño de la fuente será de 40px pero en resoluciones mayores de 992px será de 55px.

Lo que hacemos es crear todas los modificadores globales o modificadores de bloques para las distintas resoluciones pero añadiendo el sufijo `@tablet` , `@desktop` o `@fulldesktop`. E indicando en el HTML que tamaño usar según la resolución de la pantalla.

```html
.g--font-size-1 {
    font-size: 40px;
}
.g--font-size-2 {
    font-size: 50px;
}
.g--font-size-3 {
    font-size: 55px;
}
.g--font-size-4 {
    font-size: 70px;
}
  
@media (min-width: 576px) {
    .g--font-size-1\@tablet {
        font-size: 40px;
    }
    .g--font-size-2\@tablet {
        font-size: 50px;
    }
    .g--font-size-3\@tablet {
        font-size: 55px;
    }
    .g--font-size-4\@tablet {
        font-size: 70px;
    }
}
  
@media (min-width: 768px) {
    .g--font-size-1\@desktop {
        font-size: 40px;
    }
    .g--font-size-2\@desktop {
        font-size: 50px;
    }
    .g--font-size-3\@desktop {
        font-size: 55px;
    }
    .g--font-size-4\@desktop {
        font-size: 70px;
    }
}
  
@media (min-width: 992px) {
    .g--font-size-1\@fulldesktop {
        font-size: 40px;
    }
    .g--font-size-2\@fulldesktop {
        font-size: 50px;
    }
    .g--font-size-3\@fulldesktop {
        font-size: 55px;
    }
    .g--font-size-4\@fulldesktop {
        font-size: 70px;
    }
}

<p class="g--font-size-1  g--font-size-3@fulldesktop">Hola mundo</p>
```


# Breakpoints

Al crear la arquitectura responsiva es necesario indicar los pixeles de cada pantalla así como los tamaños. En los siguientes artículos se indica cuales se usan en diversos frameworks css.

- Bootstrap
<table>
  <tr>
    <th>Nombre</th>
    <th>Descripción</th>
    <th>Ancho Mínimo</th>
  </tr>
  <tr>
    <td>--</td>
    <td>Extra small devices (portrait phones)</td>
    <td>none</td>
  </tr>
  <tr>
    <td>sm</td>
    <td>Small devices (landscape phones)</td>
    <td>576px</td>
  </tr>
  <tr>
    <td>md</td>
    <td>Medium devices (tablet)</td>
    <td>768px</td>
  </tr>
  <tr>
    <td>lg</td>
    <td>Large devices (desktops)</td>
    <td>992px</td>
  </tr>
  <tr>
    <td>xl</td>
    <td>Extra large devices (large desktops)</td>
    <td>1200px</td>
  </tr>
  <tr>
    <td>xxl</td>
    <td>Extra Extra large devices (extra large desktops)</td>
    <td>1400px</td>
  </tr>
</table>

# Menu responsivo

```html
<div class="main-menu">
    <ul class="main-menu__items main-menu__items--movil-hide">
        <li class="main-menu__item"><a href="#home">Home</a></li>
        <li class="main-menu__item"><a href="#news">News</a></li>
        <li class="main-menu__item"><a href="#contact">Contact</a></li>
        <li class="main-menu__item"><a href="#about">About</a></li>
    </ul>
    <a href="javascript:void(0);" class="main-menu__hamburger" onclick="toggleVisibilityMenu()">☰</a>
</div>
<h1 style="text-align: center">Mi empresa</h1>
<p style="height: 1200px;width: 500px;"></p>
```

```css
.main-menu {
    display: flex;
    flex-direction: row;
}
 
@media (max-width: 499px) {
    .main-menu {
        position: fixed;
        top: 0;
        left: 0;
    }
}
 
.main-menu__hamburger {
    display: none;
}
@media (max-width: 499px) {
    .main-menu__hamburger {
        display: block;
    }
}
 
 
 
 
.main-menu__items {
    display: flex;
    flex-direction: row;
}
@media (max-width: 499px) {
    .main-menu__items {
        flex-direction: column;
    }
}
 
 
.main-menu__item {
    padding: 10px;
    color: #ffffff;
    background-color: #c0c0c0;
}
@media (max-width: 499px) {
    .main-menu__item {
        padding-left: 2px;
        background-color: #00ff00;
    }
}
 
 
@media (max-width: 499px) {
    .main-menu__items--movil-visible {
        display: block;
    }
 
    .main-menu__items--movil-hide {
        display: none;
    }
}
```

```JavaScript
function toggleVisibilityMenu() {
    var itemsElements = document.getElementsByClassName("main-menu__items");
    var hamburgerElements = document.getElementsByClassName("main-menu__hamburger");
 
if (itemsElements[0].className.indexOf("main-menu__items--movil-visible") >= 0) {
        itemsElements[0].className = " main-menu__items main-menu__items--movil-hide";
    hamburgerElements[0].innerHTML = "☰";
} else {
    itemsElements[0].className = "main-menu__items main-menu__items--movil visible";
    hamburgerElements[0].innerHTML = "Cerrar";
  }
}
```

# Resumen técnicas responsivas

Hemos visto varias formas de hacer las cosas responsivas. Veamos ahora una tabla en la que se explican las 4 formas posibles:

|         | Interno                                                                 | Externo                                                                 |
|---------|------------------------------------------------------------------------|------------------------------------------------------------------------|
| **Fluido**    | El propio componente decide cómo se hace responsivo y lo hace de forma fluida al tamaño del dispositivo. | El que usa el componente decide cómo se hace responsivo y lo hace de forma fluida al tamaño del dispositivo. |
| **Escalonado** | El propio componente decide cómo se hace responsivo y lo hace solo para diversos tamaños de pantalla. | El que usa el componente decide cómo se hace responsivo y lo hace solo para diversos tamaños de pantalla. |

El tipo **Externo/Escalonado** es el más normal y es el que usan frameworks como **Tailwind** o **Bootstrap**.

#### Interno/Fluido: Las tablas

```css
.c-titulo {
  font-size: 10vw;
}
````

```html
<h1 class="c-titulo">Hola mundo</h1>
```

#### Interno/Escalonado: Se usa en un menú responsivo con hamburguesa.

```css
.c-titulo {
    font-size: 40px;
}

@media (min-width: 768px) {
    .c-titulo {
        font-size: 55px;
    }
}
```

```html
<h1 class="c-titulo">Hola mundo</h1>
```

#### Externo/Fluido: Se usa muy poco.

```html
<thead>
  <tr>
    <th class="c-table__head c-table__head--min-width-2 c-table__head--max-width-3">Author</th>
    <th class="c-table__head c-table__head--min-width-2 c-table__head--max-width-3">Title</th>
    <th class="c-table__head c-table__head--min-width-1 c-table__head--max-width-2">Year</th>
    <th class="c-table__head c-table__head--min-width-1 c-table__head--max-width-2">ISBN-13</th>
    <th class="c-table__head c-table__head--min-width-1 c-table__head--max-width-2">ISBN-10</th>
  </tr>
</thead>
```

#### Externo/Escalonado: Es el que usamos con `@tablet` o `@desktop`, etc.

```html
<p class="g--font-size-1  g--font-size-3@tablet">Hola mundo</p>
```


