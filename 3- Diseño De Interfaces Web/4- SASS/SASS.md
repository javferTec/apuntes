# SASS

SASS es un preprocesador de CSS. Es como añadir funcionalidad a CSS que no tiene pero no de cosas del navegador sino para ayudar a escribir menos CSS. El código se escribe en SASS y se transforma en CSS. Permite bucles, funciones, variables ,etc.

- Transformar de SASS a CSS:
```shell
sass  ./main.scss ./main.css
```

- Transformas de SASS a CSS siempre que cambie el CSS
```shell
sass  --watch ./main.scss ./main.css
```

## Variables

Las variables en SASS empiezan por el símbolo `$`.

```scss
$font-main: Helvetica, sans-serif;
$primary-color: #E4A23F;
 
 
body {
  font-family: $font-main;
  color: $primary-color;
}
```

Se transforma en:

```css
body {
  font-family: Helvetica, sans-serif;
  color: #E4A23F;
}
```

---

## Variables CSS

En CSS, las variables permiten almacenar valores reutilizables, lo que facilita la personalización y el mantenimiento del código. A diferencia de las variables de SASS, las variables CSS tienen ventajas como:

- Se pueden cambiar en tiempo de ejecución mediante JavaScript.
- Pueden existir a nivel local dentro de los selectores.

### 1. Creación y uso de variables

1. **Definición**: Las variables deben empezar con `--`. Se definen dentro del `:root` o un selector específico.
   ```css
   :root {
       --color-alternativo-5: #0056b8;
   }
```

2. **Uso**: Se utilizan dentro de las reglas CSS con `var(--nombre-variable)`.

    ```css
    .c-button {
        background-color: var(--color-alternativo-5);
    }
    ```

3. **Valor por defecto**: Se puede definir un valor por defecto en caso de que la variable no esté definida.

    ```css
    .c-button {
        background-color: var(--color-alternativo-5, #FF0000);
    }
    ```

4. **Cascada de valores por defecto**: Si la primera variable no existe, se puede usar otra, y si esa tampoco, un valor final.

    ```css
    .c-button {
        background-color: var(--color-alternativo-5, var(--color-alternativo,                #FF0000));
    }
    ```

### 2. Manipulación desde JavaScript

1. **Modificar**:

    ```javascript
    let root = document.documentElement;
    root.style.setProperty('--color-normal-5', "#FF0000");
    ```

2. **Leer**:

    ```javascript
    let root = document.documentElement;
    let colorNormal = getComputedStyle(root).getPropertyValue("--color-normal-5");
    ```

### 3. Creación de múltiples variables

Se pueden definir múltiples variables utilizando un objeto o una lista. Por ejemplo, se pueden crear variables de padding de forma dinámica en CSS:

```scss
$paddings: (
  "xs": "1px",
  "s": "2px",
  "m": "6px",
  "l": "12px",
  "xl": "20px"
);

:root {
  @each $key, $value in $paddings {
    --padding-#{$key}: $value;
  }
}
```

Esto generará el siguiente código CSS:

```css
:root {
  --padding-xs: 1px;
  --padding-s: 2px;
  --padding-m: 6px;
  --padding-l: 12px;
  --padding-xl: 20px;
}
```

### 4. Uso de variables en componentes y layouts

Las variables creadas se pueden usar en los componentes, layouts o a nivel global:

```css
.c-button {
    --c-button-padding-vertical: var(--padding-s, 6px);
    --c-button-padding-horizontal: var(--padding-m, 8px);

    padding-top: var(--c-button-padding-vertical);
    padding-bottom: var(--c-button-padding-vertical);

    padding-left: var(--c-button-padding-horizontal);
    padding-right: var(--c-button-padding-horizontal);
}

.g--padding-vertical-m {
  padding-top: var(--padding-m);
  padding-bottom: var(--padding-m);
}
```


---
## Iterables

### 1. Listas

Las listas en Sass son **colecciones de valores ordenados**, similares a los arrays en otros lenguajes. Pueden contener cualquier tipo de valor, como números, cadenas, colores, etc.

- Las listas pueden ser **separadas por comas** o **por espacios**.

**Ejemplo de lista:**

```scss
$colores: red, blue, green;
```

### 2. Mapas

Los mapas son **colecciones de pares clave-valor**. Son similares a los objetos en JavaScript o los diccionarios en otros lenguajes. En Sass, un mapa permite asociar un nombre (clave) con un valor específico, y puedes usar este par dentro de bucles.

**Ejemplo de mapa:**

```scss
$colores: (
  rojo: red,
  azul: blue,
  verde: green
);
```

---
## Bucles

### 1. **Bucle `@for`**

El bucle `@for` permite iterar a través de un rango de números.

**Sintaxis:**

```scss
@for $i from <valor_inicial> through <valor_final> {
  // Bloque de código a ejecutar
}
```

- **`$i`** es la variable que tomará el valor de cada número dentro del rango.
- **`from <valor_inicial>`** define el inicio del bucle.
- **`through <valor_final>`** define el final del bucle (inclusive).

**Ejemplo:**

```scss
@for $i from 1 through 5 {
  .item-#{$i} {
    width: 20px * $i;
  }
}
```

Este código generará las siguientes clases:

```css
.item-1 { width: 20px; }
.item-2 { width: 40px; }
.item-3 { width: 60px; }
.item-4 { width: 80px; }
.item-5 { width: 100px; }
```

### 2. **Bucle `@each`**

El bucle `@each` es útil cuando tienes una lista o un mapa y deseas iterar sobre sus elementos. Es una manera muy eficiente de trabajar con colecciones de valores en Sass.

**Sintaxis (para listas):**

```scss
@each $item in <lista> {
  // Bloque de código a ejecutar con $item
}
```

**Sintaxis (para mapas):**

```scss
@each $key, $value in <mapa> {
  // Bloque de código a ejecutar con $key y $value
}
```

- **`$item`** es la variable que tomará cada valor de la lista o cada par clave-valor del mapa.

**Ejemplo con lista:**

```scss
$colores: red, blue, green;
@each $color in $colores {
  .text-#{$color} {
    color: $color;
  }
}
```

Generará las siguientes clases:

```css
.text-red { color: red; }
.text-blue { color: blue; }
.text-green { color: green; }
```

**Ejemplo con mapa:**

```scss
$colores: (
  rojo: red,
  azul: blue,
  verde: green
);

@each $nombre, $color in $colores {
  .text-#{$nombre} {
    color: $color;
  }
}
```

Generará las siguientes clases:

```css
.text-rojo { color: red; }
.text-azul { color: blue; }
.text-verde { color: green; }
```

### 3. **Bucle `@while`**

El bucle `@while` se ejecuta mientras se cumpla una condición. Es útil cuando no sabes cuántas veces se ejecutará el bucle, pero tienes una condición de parada definida.

**Sintaxis:**

```scss
@while <condición> {
  // Bloque de código a ejecutar
}
```

- La condición debe ser una expresión que retorne `true` o `false`.

**Ejemplo:**

```scss
$i: 1;
@while $i <= 5 {
  .item-#{$i} {
    width: 20px * $i;
  }
  $i: $i + 1;
}
```

Este código genera las mismas clases que el ejemplo con `@for`:

```css
.item-1 { width: 20px; }
.item-2 { width: 40px; }
.item-3 { width: 60px; }
.item-4 { width: 80px; }
.item-5 { width: 100px; }
```


### 4. **Bucle `@for to`**

El bucle `@for to` se usa para hacer un bucle desde 0 hasta `n-1`, es decir, el índice comienza desde 0 y el rango termina en uno menos que el valor final.

**Ejemplo:**

```scss
@for $i from 0 to 4 {
  .g--border-#{$i} {
    border: 10px * $i solid #00FF00;
  }
}
```

Este código genera el siguiente CSS:

```css
.g--border-0 {
  border: 0px solid #00FF00;
}

.g--border-1 {
  border: 10px solid #00FF00;
}

.g--border-2 {
  border: 20px solid #00FF00;
}

.g--border-3 {
  border: 30px solid #00FF00;
}
```

### 5. **Bucle `@for through`**

El bucle `@for through` se usa para hacer un bucle desde 1 hasta `n` (inclusive). El índice comienza en 1 y termina en el valor especificado.

**Ejemplo:**

```scss
@for $i from 1 through 4 {
  .g--border-#{$i} {
    border: 10px * $i solid #00FF00;
  }
}
```

Este código genera el siguiente CSS:

```css
.g--border-1 {
  border: 10px solid #00FF00;
}

.g--border-2 {
  border: 20px solid #00FF00;
}

.g--border-3 {
  border: 30px solid #00FF00;
}

.g--border-4 {
  border: 40px solid #00FF00;
}
```

---

## Selectores Padre

El uso de `&` en SASS te permite escribir menos con el nombre de las clases, ya que el `&` se convierte en el nombre de la clase padre.

```scss
AAA {
  color:red;
   
  &__BBB {
    padding:5px;
  }
}
```

Se transforma en:

```scss
AAA {
  color:red;
}
   
AAA__BBB {
  padding:5px;
}
```

---
## Anidamiento

El **anidamiento** en Sass es una característica que te permite escribir reglas CSS dentro de otras reglas, lo que mejora la organización y la legibilidad de tu código. Esto es especialmente útil cuando tienes reglas que dependen de un selector principal (como un contenedor o clase) y quieres evitar repetirlo en cada declaración.

**¿Cómo funciona el anidamiento?**

En Sass, puedes anidar selectores dentro de otros, lo que simula la estructura jerárquica del HTML. Esto evita la necesidad de escribir el selector completo varias veces.

Ejemplo:

```scss
.container {
  width: 100%;
  padding: 20px;

  .header {
    background-color: #333;
    color: white;
  }

  .footer {
    background-color: #444;
    color: white;
  }
}
```

Se transforma en:

```css
.container {
  width: 100%;
  padding: 20px;
}

.container .header {
  background-color: #333;
  color: white;
}

.container .footer {
  background-color: #444;
  color: white;
}
```


- **.container** es el selector principal, y dentro de él, anidamos los selectores `.header` y `.footer`.
- Sass genera automáticamente el selector completo `.container .header` y `.container .footer` en el CSS, eliminando la necesidad de escribirlo manualmente.


---
## Módulos (`@import`)

Un **módulo** en Sass es simplemente un archivo SCSS o Sass que contiene un conjunto de reglas, funciones, mixins o variables. Puedes dividir tu código en diferentes archivos, cada uno con un propósito específico (por ejemplo, un archivo para colores, otro para tipografía, etc.), y luego usar `@use` o `@import` para combinarlos en un solo archivo principal.

```scss
@import "./_c-button.scs
```

>[!NOTE]
>** Los ficheros que importamos deben empezar por `_` para que no genere también el CSS de ese fichero** o no llevarlo para que lo genere
> 

---
## Mixin

Un **mixin** es una especie de "plantilla" o "función" en Sass que contiene un bloque de código CSS. Este bloque de código se puede incluir en cualquier lugar donde lo necesites mediante el uso de `@include`.

**Ejemplo**:

```scss
@mixin box-shadow($color) {
  -webkit-box-shadow: 2px 10px 24px $color;
  -moz-box-shadow: 2px 10px 24px $color;
  box-shadow: 2px 10px 24px $color;
}
```

- **`@mixin box-shadow($color)`** define un mixin llamado `box-shadow` que recibe un parámetro `$color`. Este parámetro puede ser cualquier color que desees usar al invocar el mixin.
- Dentro del mixin, tienes el bloque de código CSS para aplicar la propiedad `box-shadow` en diferentes navegadores (con prefijos `-webkit-` y `-moz-` para compatibilidad con versiones anteriores de algunos navegadores).

Ahora, puedes usar este mixin en cualquier lugar de tu código:

```scss
.c-button {
  color: #FF0000;
  @include box-shadow(#FF0000);
}
 
.c-panel {
  color: #00FF00;
  @include box-shadow(#00FF00);
}
```

- En el caso de **`.c-button`**, estás incluyendo el mixin `box-shadow` y pasándole el color `#FF0000` (rojo).
- En el caso de **`.c-panel`**, estás incluyendo el mismo mixin, pero con un color diferente, `#00FF00` (verde).

**Cómo se transforma:**

Cuando Sass compila este código, los mixins se "expandirán" e insertarán directamente en el CSS resultante, reemplazando la llamada `@include` por el bloque de reglas CSS correspondiente.

El CSS resultante sería:

```css
.c-button {
  color: #FF0000;
  -webkit-box-shadow: 2px 10px 24px #FF0000;
  -moz-box-shadow: 2px 10px 24px #FF0000;
  box-shadow: 2px 10px 24px #FF0000;
}
 
.c-panel {
  color: #00FF00;
  -webkit-box-shadow: 2px 10px 24px #00FF00;
  -moz-box-shadow: 2px 10px 24px #00FF00;
  box-shadow: 2px 10px 24px #00FF00;
}
```

El uso de mixins es una **excelente forma de evitar duplicación de código**, especialmente cuando necesitas aplicar un conjunto de reglas CSS similares en varios lugares de tu proyecto.

---
## Funciones

Una **función** en Sass permite realizar operaciones y devolver un valor calculado. Puedes crear una función personalizada usando la directiva `@function`, y dentro de la función puedes definir cómo se calculará y devolverá el valor. Luego, esa función se puede llamar en cualquier parte del código donde necesites el valor calculado.

**Ejemplo:**

```scss
@function getBorderSize($size) {
  @return 10px * $size;
}
```

- **`@function getBorderSize($size)`**: Aquí estamos definiendo una función llamada `getBorderSize`. Esta función toma un parámetro `$size`, que representará el valor con el que multiplicar el valor base de `10px`.
- **`@return 10px * $size`**: Dentro de la función, realizamos una operación de multiplicación con el valor pasado a `$size` y `10px`. El resultado de esta multiplicación se devuelve con `@return`.

Luego, podemos usar esta función en el resto de nuestro código CSS. En el siguiente caso, usamos la función `getBorderSize(2)` para calcular el valor del borde de un botón:

```scss
.c-button {
  color: #FF0000;
  border: getBorderSize(2) solid #00FF00;
}
```

- Aquí, estamos llamando a la función `getBorderSize(2)`, lo que devuelve `10px * 2`, es decir, `20px`.
- Así que el borde del botón será de `20px` de grosor y de color verde (`#00FF00`).

**Cómo se transforma:**

Cuando Sass compila este código, la función `getBorderSize(2)` se evalúa y se reemplaza por el valor calculado, en este caso, `20px`. El resultado final en CSS es:

```css
.c-button {
  color: #FF0000;
  border: 20px solid #00FF00;
}
```

---
## Condicionales

En Sass, **`@if`** permite agregar decisiones condicionales en tu código. Es como decir: "Si pasa esto, haz esto otro, de lo contrario, haz otra cosa".

Y si quieres agregar una opción alternativa si la condición no se cumple, puedes usar **`@else`**.

**Ejemplo con `@if` y `@else`:**

```scss
@mixin border($size) {
  // Si el tamaño es mayor o igual a 3px, cambia el color a rojo
  @if $size >= 3 {
    $color: #FF0000; // Si el tamaño es mayor o igual a 3, el color será rojo
  } @else {
    $color: #00FF00; // Si no, el color será verde
  }

  border: $size * 2 solid $color; // Establece el borde con el tamaño y color
}

.c-caja1 {
  color: #FF0000;
  @include border(2px); // Llama al mixin con tamaño 2px
}

.c-caja2 {
  color: #FF0000;
  @include border(5px); // Llama al mixin con tamaño 5px
}
```


1. **Definimos el mixin `border($size)`**:
    - Comienza con un color predeterminado: **verde (`#00FF00`)**.
    - Luego, con el condicional `@if`, verificamos si el valor de `$size` es **mayor o igual a 3**:
        - Si es así, **cambiamos el color a rojo**.
        - Si no lo es, usamos el color verde.
    - Finalmente, aplicamos el borde con un tamaño dos veces mayor que `$size` y el color calculado.
2. **Usamos el mixin en las clases `.c-caja1` y `.c-caja2`**:
    - **`.c-caja1`**: Usamos el mixin con un tamaño de `2px`. Como **`2px` no es mayor o igual a 3**, el color será verde (`#00FF00`) y el borde será `4px solid #00FF00`.
    - **`.c-caja2`**: Usamos el mixin con un tamaño de `5px`. Como **`5px` es mayor o igual a 3**, el color será rojo (`#FF0000`) y el borde será `10px solid #FF0000`.

**Resultado final en CSS:**

```css
.c-caja1 {
  color: #FF0000;
  border: 4px solid #00FF00; /* Borde verde */
}

.c-caja2 {
  color: #FF0000;
  border: 10px solid #FF0000; /* Borde rojo */
}
```


---
## Funciones predefinidas

### 1. String (Cadenas)

Las funciones de cadenas en Sass se utilizan para manipular y obtener información sobre las cadenas de texto.

| **Función**                           | **Descripción y Ejemplo**                                                                                                                                                                            |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **quote(string)**                     | Añade comillas a la cadena y devuelve el resultado. Ejemplo: `quote("¡Hola mundo!")` <br>**Resultado**: `"¡Hola mundo!"`                                                                             |
| **str-index(string, substring)**      | Devuelve el índice de la primera aparición de la subcadena dentro de la cadena. Ejemplo: `str-index("¡Hola mundo!", "H")`<br> **Resultado**: `1`                                                     |
| **str-insert(string, insert, index)** | Devuelve la cadena con el texto `insert` insertado en la posición especificada por `index`. Ejemplo: `str-insert("¡Hola mundo!", " maravilloso", 6)` <br>**Resultado**: `"¡Hola maravilloso mundo!"` |
| **str-length(string)**                | Devuelve la longitud de la cadena (en caracteres). Ejemplo: `str-length("¡Hola mundo!")` <br>**Resultado**: `12`                                                                                     |
| **str-slice(string, start, end)**     | Extrae los caracteres de la cadena desde `start` hasta `end` y devuelve el segmento. Ejemplo: `str-slice("¡Hola mundo!", 2, 5)` <br>**Resultado**: `"ola"`                                           |
| **to-lower-case(string)**             | Devuelve una copia de la cadena convertida a minúsculas. Ejemplo: `to-lower-case("¡Hola Mundo!")` <br>**Resultado**: `"¡hola mundo!"`                                                                |
| **to-upper-case(string)**             | Devuelve una copia de la cadena convertida a mayúsculas. Ejemplo: `to-upper-case("¡Hola Mundo!")` <br>**Resultado**: `"¡HOLA MUNDO!"`                                                                |
| **unique-id()**                       | Devuelve una cadena aleatoria y única sin comillas (garantizado que será única dentro de la sesión actual de Sass). Ejemplo: `unique-id()` <br>**Resultado**: `tyghefnsv`                            |
| **unquote(string)**                   | Elimina las comillas alrededor de la cadena (si las tiene) y devuelve el resultado. Ejemplo: `unquote("\"¡Hola Mundo!\"")` <br>**Resultado**: `¡Hola Mundo!`                                         |

### 2. Numéricas

Las funciones numéricas en Sass se utilizan para manipular valores numéricos.

| **Función**                | **Descripción y Ejemplo**                                                                                                                                                                                                                         |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **abs(number)**            | Devuelve el valor absoluto de un número.  <br>Ejemplo: `abs(15)`  <br>**Resultado**: `15`  <br>Ejemplo: `abs(-15)`  <br>**Resultado**: `15`                                                                                                       |
| **ceil(number)**           | Redondea el número hacia arriba al entero más cercano.  <br>Ejemplo: `ceil(15.20)`  <br>**Resultado**: `16`                                                                                                                                       |
| **comparable(num1, num2)** | Devuelve si `num1` y `num2` son comparables.  <br>Ejemplo: `comparable(15px, 10px)`  <br>**Resultado**: `true`  <br>Ejemplo: `comparable(20mm, 1cm)`  <br>**Resultado**: `true`  <br>Ejemplo: `comparable(35px, 2em)`  <br>**Resultado**: `false` |
| **floor(number)**          | Redondea el número hacia abajo al entero más cercano.  <br>Ejemplo: `floor(15.80)`  <br>**Resultado**: `15`                                                                                                                                       |
| **max(number...)**         | Devuelve el valor más alto de varios números.  <br>Ejemplo: `max(5, 7, 9, 0, -3, -7)`  <br>**Resultado**: `9`                                                                                                                                     |
| **min(number...)**         | Devuelve el valor más bajo de varios números.  <br>Ejemplo: `min(5, 7, 9, 0, -3, -7)`  <br>**Resultado**: `-7`                                                                                                                                    |
| **percentage(number)**     | Convierte el número a porcentaje (multiplica el número por 100).  <br>Ejemplo: `percentage(1.2)`  <br>**Resultado**: `120`                                                                                                                        |
| **random()**               | Devuelve un número aleatorio entre 0 y 1.  <br>Ejemplo: `random()`  <br>**Resultado**: `0.45673`                                                                                                                                                  |
| **random(number)**         | Devuelve un número entero aleatorio entre 1 y el número especificado.  <br>Ejemplo: `random(6)`  <br>**Resultado**: `4`                                                                                                                           |
| **round(number)**          | Redondea el número al entero más cercano.  <br>Ejemplo: `round(15.20)`  <br>**Resultado**: `15`  <br>Ejemplo: `round(15.80)`  <br>**Resultado**: `16`                                                                                             |

### 3. Listas

Las funciones de lista en Sass se utilizan para acceder a valores dentro de una lista, combinar listas y agregar elementos a listas.

Es importante tener en cuenta que las listas en Sass son inmutables, lo que significa que no pueden modificarse directamente. Cuando una función de lista devuelve una lista, devuelve una nueva lista en lugar de modificar la original.

Además, las listas en Sass son indexadas desde 1, no desde 0.

|**Función**|**Descripción y Ejemplo**|
|---|---|
|**append(list, value, [separator])**|Agrega un solo valor al final de la lista. El separador puede ser `auto`, `comma` o `space`, siendo `auto` el valor por defecto. Ejemplo: `append((a b c), d)` **Resultado**: `a b c d` Ejemplo: `append((a b c), (d), comma)` **Resultado**: `a, b, c, d`|
|**index(list, value)**|Devuelve la posición del índice para el valor dentro de la lista. Ejemplo: `index(a b c, b)` **Resultado**: `2` Ejemplo: `index(a b c, f)` **Resultado**: `null`|
|**is-bracketed(list)**|Verifica si la lista tiene corchetes (`[]`). Ejemplo: `is-bracketed([a b c])` **Resultado**: `true` Ejemplo: `is-bracketed(a b c)` **Resultado**: `false`|
|**join(list1, list2, [separator, bracketed])**|Une `list2` al final de `list1`. El separador puede ser `auto`, `comma` o `space` (el valor por defecto es `auto`, que usa el separador de la primera lista). El parámetro `bracketed` puede ser `auto`, `true` o `false`. Ejemplo: `join(a b c, d e f)` **Resultado**: `a b c d e f` Ejemplo: `join((a b c), (d e f), comma)` **Resultado**: `a, b, c, d, e, f` Ejemplo: `join(a b c, d e f, $bracketed: true)` **Resultado**: `[a b c d e f]`|
|**length(list)**|Devuelve la longitud de la lista (el número de elementos). Ejemplo: `length(a b c)` **Resultado**: `3`|
|**list-separator(list)**|Devuelve el separador de la lista como una cadena de texto. Puede ser `space` o `comma`. Ejemplo: `list-separator(a b c)` **Resultado**: `"space"` Ejemplo: `list-separator(a, b, c)` **Resultado**: `"comma"`|
|**nth(list, n)**|Devuelve el enésimo elemento de la lista. Ejemplo: `nth(a b c, 3)` **Resultado**: `c`|
|**set-nth(list, n, value)**|Establece el enésimo elemento de la lista con el valor especificado. Ejemplo: `set-nth(a b c, 2, x)` **Resultado**: `a x c`|
|**zip(lists)**|Combina varias listas en una lista multidimensional. Ejemplo: `zip(1px 2px 3px, solid dashed dotted, red green blue)` **Resultado**: `1px solid red, 2px dashed green, 3px dotted blue`|

### 4. Mapas

En Sass, el tipo de dato **mapa** representa uno o más pares clave/valor.

**Consejo**: También es posible usar las funciones de lista, que vimos en la sección  anterior, con mapas. En ese caso, el mapa será tratado como una lista de dos elementos (clave y valor).

Los mapas en Sass son **inmutables**, lo que significa que no se pueden modificar directamente. Las funciones que devuelven un mapa devolverán un **nuevo mapa**, y no cambiarán el mapa original.

|**Función**|**Descripción y Ejemplo**|
|---|---|
|**map-get(map, key)**|Devuelve el valor asociado con una clave específica en el mapa. Ejemplo: `$font-sizes: ("small": 12px, "normal": 18px, "large": 24px)` `map-get($font-sizes, "small")` **Resultado**: `12px`|
|**map-has-key(map, key)**|Verifica si el mapa tiene la clave especificada. Devuelve `true` o `false`. Ejemplo: `$font-sizes: ("small": 12px, "normal": 18px, "large": 24px)` `map-has-key($font-sizes, "big")` **Resultado**: `false`|
|**map-keys(map)**|Devuelve una lista con todas las claves en el mapa. Ejemplo: `$font-sizes: ("small": 12px, "normal": 18px, "large": 24px)` `map-keys($font-sizes)` **Resultado**: `"small", "normal", "large"`|
|**map-merge(map1, map2)**|Une `map2` al final de `map1`. Ejemplo: `$font-sizes: ("small": 12px, "normal": 18px, "large": 24px)` `$font-sizes2: ("x-large": 30px, "xx-large": 36px)` `map-merge($font-sizes, $font-sizes2)` **Resultado**: `"small": 12px, "normal": 18px, "large": 24px, "x-large": 30px, "xx-large": 36px`|
|**map-remove(map, keys...)**|Elimina las claves especificadas del mapa. Ejemplo: `$font-sizes: ("small": 12px, "normal": 18px, "large": 24px)` `map-remove($font-sizes, "small")` **Resultado**: `("normal": 18px, "large": 24px)` Ejemplo: `map-remove($font-sizes, "small", "large")` **Resultado**: `("normal": 18px)`|
|**map-values(map)**|Devuelve una lista con todos los valores en el mapa. Ejemplo: `$font-sizes: ("small": 12px, "normal": 18px, "large": 24px)` `map-values($font-sizes)` **Resultado**: `12px, 18px, 24px`|

### 5. Selectores

Las funciones de selector en Sass se utilizan para comprobar y manipular selectores dentro de las hojas de estilo.

| **Función**                                           | **Descripción y Ejemplo**                                                                                                                                                                                                                                               |
| ----------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **is-superselector(super, sub)**                      | Verifica si el selector `super` coincide con todos los elementos que coincide `sub`. Ejemplo: `is-superselector("div", "div.myInput")` **Resultado**: `true` Ejemplo: `is-superselector("div.myInput", "div")` **Resultado**: `false`                                   |
| **selector-append(selectors)**                        | Añade el segundo (y tercero/cuarto, etc.) selector al primer selector. Ejemplo: `selector-append("div", ".myInput")` **Resultado**: `div.myInput` Ejemplo: `selector-append(".warning", "__a")` **Resultado**: `.warning__a`                                            |
| **selector-extend(selector, extendee, extender)**     | (Función incompleta en el ejemplo, requiere más contexto sobre cómo se usa en Sass).                                                                                                                                                                                    |
| **selector-nest(selectors)**                          | Devuelve un nuevo selector que contiene una lista anidada de selectores CSS basada en la lista proporcionada. Ejemplo: `selector-nest("ul", "li")` **Resultado**: `ul li` Ejemplo: `selector-nest(".warning", "alert", "div")` **Resultado**: `.warning div, alert div` |
| **selector-parse(selector)**                          | Devuelve una lista de cadenas contenidas en un selector usando el mismo formato que el selector original. Ejemplo: `selector-parse("h1 .myInput .warning")` **Resultado**: `('h1', '.myInput', '.warning')`                                                             |
| **selector-replace(selector, original, replacement)** | Devuelve un nuevo selector donde los selectores especificados en `replacement` reemplazan a los especificados en `original`. Ejemplo: `selector-replace("p.warning", "p", "div")` **Resultado**: `div.warning`                                                          |
| **selector-unify(selector1, selector2)**              | Devuelve un nuevo selector que coincide solo con los elementos que coinciden tanto con `selector1` como con `selector2`. Ejemplo: `selector-unify("myInput", ".disabled")` **Resultado**: `myInput.disabled` Ejemplo: `selector-unify("p", "h1")` **Resultado**: `null` |
| **simple-selectors(selectors)**                       | Devuelve una lista de los selectores individuales dentro de un selector compuesto. Ejemplo: `simple-selectors("div.myInput")` **Resultado**: `div`, `.myInput` Ejemplo: `simple-selectors("div.myInput:before")` **Resultado**: `div`, `.myInput`, `:before`            |

### 6. Introspección

Las funciones de introspección son útiles principalmente para la depuración, ya que permiten obtener información sobre el estado del código, las variables, funciones, mixins, y más. Estas funciones rara vez se usan cuando se construye una hoja de estilo, pero son muy valiosas cuando algo no funciona correctamente o se necesita depurar el código.

|**Función**|**Descripción y Ejemplo**|
|---|---|
|**call(function, arguments...)**|Llama a una función con los argumentos especificados y devuelve el resultado.|
|**content-exists()**|Verifica si el mixin actual recibió un bloque `@content`.|
|**feature-exists(feature)**|Verifica si la característica especificada es compatible con la implementación actual de Sass. Ejemplo: `feature-exists("at-error")` **Resultado**: `true`|
|**function-exists(functionname)**|Verifica si la función especificada existe. Ejemplo: `function-exists("nonsense")` **Resultado**: `false`|
|**get-function(functionname, css: false)**|Devuelve la función especificada. Si `css` es `true`, devuelve una función CSS simple en su lugar.|
|**global-variable-exists(variablename)**|Verifica si la variable global especificada existe. Ejemplo: `variable-exists(a)` **Resultado**: `true`|
|**inspect(value)**|Devuelve una representación en cadena del valor especificado.|
|**mixin-exists(mixinname)**|Verifica si el mixin especificado existe. Ejemplo: `mixin-exists("important-text")` **Resultado**: `true`|
|**type-of(value)**|Devuelve el tipo de valor. Los tipos pueden ser: `number`, `string`, `color`, `list`, `map`, `bool`, `null`, `function`, `arglist`. Ejemplo: `type-of(15px)` **Resultado**: `number` Ejemplo: `type-of(#ff0000)` **Resultado**: `color`|
|**unit(number)**|Devuelve la unidad asociada con un número. Ejemplo: `unit(15px)` **Resultado**: `px`|
|**unitless(number)**|Verifica si el número especificado tiene una unidad asociada. Ejemplo: `unitless(15px)` **Resultado**: `false` Ejemplo: `unitless(15)` **Resultado**: `true`|
|**variable-exists(variablename)**|Verifica si la variable especificada existe en el ámbito actual. Ejemplo: `variable-exists(b)` **Resultado**: `true`|

### 7. Colores

En Sass, las funciones de color se dividen en tres categorías principales: funciones de establecimiento de color, funciones para obtener información del color y funciones para manipular colores. A continuación se presenta un resumen de cada tipo de función y su uso.

#### **Funciones de Establecimiento de Color en Sass**

Estas funciones se utilizan para definir colores utilizando diferentes modelos de color.

|**Función**|**Descripción y Ejemplo**|
|---|---|
|**rgb(red, green, blue)**|Establece un color usando el modelo Red-Green-Blue (RGB). Los parámetros definen la intensidad de cada color y pueden ser enteros entre 0 y 255 o valores en porcentaje. Ejemplo: `rgb(0, 0, 255)` **Resultado**: azul|
|**rgba(red, green, blue, alpha)**|Establece un color usando el modelo Red-Green-Blue-Alpha (RGBA), que incluye un canal alfa para definir la opacidad del color. Ejemplo: `rgba(0, 0, 255, 0.3)` **Resultado**: azul con opacidad|
|**hsl(hue, saturation, lightness)**|Establece un color usando el modelo Hue-Saturation-Lightness (HSL), que representa los colores como coordenadas cilíndricas. Ejemplo: `hsl(120, 100%, 50%)` **Resultado**: verde|
|**hsla(hue, saturation, lightness, alpha)**|Establece un color usando el modelo Hue-Saturation-Lightness-Alpha (HSLA), que es una extensión de HSL con un canal alfa. Ejemplo: `hsla(120, 100%, 50%, 0.3)` **Resultado**: verde con opacidad|
|**grayscale(color)**|Establece un color en escala de grises con la misma luminosidad que el color original. Ejemplo: `grayscale(#7fffd4)` **Resultado**: `#c6c6c6`|
|**complement(color)**|Devuelve el color complementario del color especificado. Ejemplo: `complement(#7fffd4)` **Resultado**: `#ff7faa`|
|**invert(color, weight)**|Devuelve el color inverso del color especificado. El parámetro `weight` es opcional y debe ser un valor entre 0% y 100%. Ejemplo: `invert(white)` **Resultado**: `black`|

#### **Funciones para Obtener Información de Color en Sass**

Estas funciones devuelven información detallada sobre un color específico.

|**Función**|**Descripción y Ejemplo**|
|---|---|
|**red(color)**|Devuelve el valor del componente rojo de un color, como un número entre 0 y 255. Ejemplo: `red(#7fffd4)` **Resultado**: `127`|
|**green(color)**|Devuelve el valor del componente verde de un color, como un número entre 0 y 255. Ejemplo: `green(#7fffd4)` **Resultado**: `255`|
|**blue(color)**|Devuelve el valor del componente azul de un color, como un número entre 0 y 255. Ejemplo: `blue(#7fffd4)` **Resultado**: `212`|
|**hue(color)**|Devuelve el valor de matiz (hue) del color como un número entre 0° y 360°. Ejemplo: `hue(#7fffd4)` **Resultado**: `160deg`|
|**saturation(color)**|Devuelve la saturación del color en el espacio HSL, como un número entre 0% y 100%. Ejemplo: `saturation(#7fffd4)` **Resultado**: `100%`|
|**lightness(color)**|Devuelve la luminosidad (lightness) del color en el espacio HSL, como un número entre 0% y 100%. Ejemplo: `lightness(#7fffd4)` **Resultado**: `74.9%`|
|**alpha(color)**|Devuelve el valor del canal alfa de un color como un número entre 0 y 1. Ejemplo: `alpha(#7fffd4)` **Resultado**: `1`|
|**opacity(color)**|Devuelve el valor del canal alfa de un color como un número entre 0 y 1. Ejemplo: `opacity(rgba(127, 255, 212, 0.5))` **Resultado**: `0.5`|

#### **Funciones para Manipular Colores en Sass**

Estas funciones permiten ajustar, mezclar o modificar colores de diversas maneras.

|**Función**|**Descripción y Ejemplo**|
|---|---|
|**mix(color1, color2, weight)**|Crea un color que es una mezcla de `color1` y `color2`. El parámetro `weight` controla la cantidad de cada color en la mezcla, y debe estar entre 0% y 100%. Ejemplo: `mix(#ff0000, #0000ff, 50%)` **Resultado**: morado|
|**adjust-hue(color, degrees)**|Ajusta el matiz de un color por una cantidad de grados entre -360° y 360°. Ejemplo: `adjust-hue(#7fffd4, 80deg)` **Resultado**: `#8080ff`|
|**adjust-color(color, red, green, blue, hue, saturation, lightness, alpha)**|Ajusta uno o más parámetros de un color por la cantidad especificada. Ejemplo: `adjust-color(#7fffd4, blue: 25)` **Resultado**: modifica el componente azul del color|
|**change-color(color, red, green, blue, hue, saturation, lightness, alpha)**|Cambia uno o más parámetros del color a los nuevos valores especificados. Ejemplo: `change-color(#7fffd4, red: 255)` **Resultado**: `#ffffd4`|
|**scale-color(color, red, green, blue, saturation, lightness, alpha)**|Escala uno o más parámetros del color, multiplicando su valor por un factor.|
|**rgba(color, alpha)**|Crea un nuevo color basado en `color` con el canal alfa especificado. Ejemplo: `rgba(#7fffd4, 30%)` **Resultado**: `rgba(127, 255, 212, 0.3)`|
|**lighten(color, amount)**|Crea un color más claro aumentando la luminosidad entre 0% y 100%.|
|**darken(color, amount)**|Crea un color más oscuro reduciendo la luminosidad entre 0% y 100%.|
|**saturate(color, amount)**|Crea un color más saturado aumentando la saturación entre 0% y 100%.|
|**desaturate(color, amount)**|Crea un color menos saturado reduciendo la saturación entre 0% y 100%.|
|**opacify(color, amount)**|Crea un color más opaco aumentando el canal alfa entre 0 y 1.|
|**fade-in(color, amount)**|Crea un color más opaco aumentando el canal alfa entre 0 y 1.|
|**transparentize(color, amount)**|Crea un color más transparente reduciendo el canal alfa entre 0 y 1.|
|**fade-out(color, amount)**|Crea un color más transparente reduciendo el canal alfa entre 0 y 1.|

---

![[Sass(SCSS) and Compass Cheat Sheet.pdf]]