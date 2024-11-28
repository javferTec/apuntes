# CSS

## ¿Cómo añadir CSS?

1. Con un fichero externo y añadiendo en el `<head>`:
```html
<link rel="stylesheet" href="main.css">
```

2. Añadiendo la etiqueta `<style>`
```html
<style>
body {
  background-color: #FF00FF;
}
 
h1 {
  color: #FE56A2;
  margin-left: 40px;
}
</style>
```

3. CSS dentro del propio elemento con el atributo `style`.
```html
<h1 style="color:blue;text-align:center;">This is a heading</h1>
```

>[!NOTE]
>Solo se debería añadir el CSS en ficheros externo y en algún caso concreto con "style" como por ejemplo la imagen de background.

---
## Selectores y especificidad

Se deben usar prácticamente siempre únicamente selectores de clase. Cuando mas complejo sea el selector tendrá una Especificidad mas alta y queremos que sea baja. Por ello solo de debe usar el **selector de clase que empieza por un `.`**

---

## Modelo de caja

El modelo de java le dice al navegador si cuando indicamos el ancho, ese ancho incluye o no al padding y al borde. Por defecto no los incluye pero lo ideal es que el ancho si que incluya el padding y el borde, por eso hay que usar la propiedad **box-sizing: border-box** de CSS.

**Como indicar correctamente el box-sizing:**
```css
html {
  box-sizing: border-box;
}
 
*, *:before, *:after {
  box-sizing: inherit;
  }
```

*Ejemplo:*
```css
.caja {
      width: 300px;
      height: 150px;
      padding: 20px;
      border: 10px solid #000;
      background-color: lightblue;
}
```

---

## Display

En la propiedad "display" de CSS hay muchos posibles valores , ahora vamos a ver los 5 siguientes:

- `inline`: Para un elemento que forma parte de un párrafo.
- `inline-block`: Como `inline` pero permite especificar el ancho y el alto.
- block: Después del elemento se genera un salto de línea y también permite especificar el ancho y el alto.
- `display: none` es como si el elemento no existiera por lo que el resto de elementos se desplazan para ocupar su hueco
- `visibility: hidden` el elemento es invisible pero sigue ocupando su hueco.

*Ejemplo:*
```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ejemplo Display</title>
  <style>
    .inline { display: inline; }
    .inline-block { display: inline-block; width: 100px; height: 50px; background-color: lightcoral; }
    .block { display: block; width: 100px; height: 50px; background-color: lightgreen; }
    .none { display: none; }
    .hidden { visibility: hidden; }
  </style>
</head>
<body>
  <div class="inline">Elemento inline</div>
  <div class="inline-block">Elemento inline-block</div>
  <div class="block">Elemento block</div>
  <div class="none">Elemento no visible (display: none)</div>
  <div class="hidden">Elemento invisible (visibility: hidden)</div>
</body>
</html>
```
---
## &nbsp;

Hace que un espacio con "&nbsp;" sea como una letra mas por lo que no partirá la frase por ese espacio.

*Ejemplo:*
```html
<p>Este es un ejemplo&nbsp;de uso de&nbsp;espacios no separables.</p>
```
---

## Sombras

Las sombras se usan para dar sensación de profundidad sin necesidad de bordes. Suponemos que la luz viene de arriba.

Se usa la propiedad `box-shadow`.

![[sombras.png]]

*Ejemplo:*
```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ejemplo Sombras</title>
  <style>
    .sombra {
      width: 200px;
      height: 100px;
      background-color: lightblue;
      box-shadow: 10px 10px 15px rgba(0, 0, 0, 0.3);
    }
  </style>
</head>
<body>
  <div class="sombra"></div>
</body>
</html>
```

---

## Meter & Progress

Etiquetas HTML para:

Barra de progreso: Etiqueta `<progress>`
Barra de medida: Etiqueta `<meter>`

*Ejemplo:*
```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ejemplo Meter y Progress</title>
</head>
<body>
  <h3>Progreso de descarga:</h3>
  <progress value="70" max="100"></progress>

  <h3>Medición de temperatura:</h3>
  <meter value="30" min="0" max="100" low="20" high="80" optimum="60"></meter>
</body>
</html>
```
---

## Flexbox

**Flexbox**, abreviatura de _Flexible Box Layout_, es una técnica en CSS diseñada para distribuir espacio y alinear elementos en un contenedor, incluso cuando su tamaño es dinámico. Es útil tanto para diseño horizontal como vertical y es ideal para ajustar componentes en interfaces.
### Conceptos Básicos

1. **Contenedor Flexible**:
    
    - Un elemento padre con `display: flex;`.
    - Los hijos dentro de este contenedor son los "items flexibles" o _flex items_.
    - Controla cómo se distribuyen y alinean los items.
2. **Ítems Flexibles**:
    
    - Los elementos hijos directos del contenedor flexible.
    - Se comportan según las reglas de flexbox: crecen, se encogen o mantienen un tamaño fijo según el espacio disponible.

### Propiedades del Contenedor Flexible

#### **`flex-direction`**

Controla la dirección de los items:

- `row`: Horizontal (por defecto). ![](https://logongas.es/lib/exe/fetch.php?media=clase:daw:diw:1eval:flex-row.png)
- `row-reverse`: Igual que `row`, pero invierte el orden.
- `column`: Vertical.
![](https://logongas.es/lib/exe/fetch.php?media=clase:daw:diw:1eval:flex-colum.png)
- `column-reverse`: Igual que `column`, pero invierte el orden.

#### **`justify-content`**

Distribuye los items a lo largo del eje principal:

- `flex-start`: Al principio.
- `flex-end`: Al final.
- `center`: Centrados.
- `space-between`: Espaciados equitativamente, con el primer y último item pegados a los bordes.
- `space-around`: Espaciados equitativamente con márgenes a los extremos.
- `space-evenly`: Espaciados uniformemente.

![](https://logongas.es/lib/exe/fetch.php?media=clase:daw:diw:1eval:flex-justify-content.png)

#### **`align-items`**

Alinea los items en el eje perpendicular al principal (por ejemplo, vertical si `flex-direction: row`):

- `flex-start`: Arriba.
- `flex-end`: Abajo.
- `center`: Centrado.
- `stretch`: Los items llenan el eje.
- `baseline`: Alineados con la línea base del texto.

![](https://logongas.es/lib/exe/fetch.php?media=clase:daw:diw:1eval:flex-align-items.png)

#### **`flex-wrap`**

Controla si los items se ajustan a varias líneas si no caben en una sola:

- `nowrap`: (Por defecto) Todo en una línea.
- `wrap`: Los items se ajustan a nuevas líneas.
![](https://logongas.es/lib/exe/fetch.php?media=clase:daw:diw:1eval:flex-wrap.png)
- `wrap-reverse`: Igual que `wrap`, pero invierte el orden de las líneas.

#### **`align-content`**

Distribuye las líneas cuando hay varias filas o columnas (solo tiene efecto con `flex-wrap: wrap`):

- Valores similares a `justify-content`, pero para líneas: `flex-start`, `flex-end`, `center`, `space-between`, `space-around`, `stretch`.

![](https://logongas.es/lib/exe/fetch.php?media=clase:daw:diw:1eval:flex-align-content.png)

### Propiedades de los Items Flexibles

#### **`flex-grow`**

Permite que un item crezca proporcionalmente para ocupar espacio sobrante.

- `0` (por defecto): El item no crece.
- Un número mayor (e.g., `1`, `2`): Determina cuánto crecerá un item en relación con otros. Por ejemplo, un item con `flex-grow: 2` crecerá el doble que uno con `flex-grow: 1`.
![](https://logongas.es/lib/exe/fetch.php?media=clase:daw:diw:1eval:flex-grow.png)

#### **`flex-shrink`**

Controla cuánto puede reducirse un item si el contenedor es más pequeño que el total de items.

- `1` (por defecto): Se encoge en proporción.
- `0`: No se encoge.

#### **`flex-basis`**

Determina el tamaño inicial del item antes de aplicar `flex-grow` o `flex-shrink`. Puede ser un valor fijo (`px`, `%`) o `auto` (el tamaño de su contenido).

#### **`flex`**

Shorthand para definir las tres propiedades anteriores en una línea: `flex-grow`, `flex-shrink` y `flex-basis`.

- Ejemplo: `flex: 1 0 auto;`.

#### **`align-self`**

Ajusta la alineación de un item individual, sobrescribiendo `align-items` del contenedor.

- Valores: `flex-start`, `flex-end`, `center`, `stretch`, `baseline`.

---

### Ejemplos Prácticos

#### Ejemplo 1: Distribución básica con `flex-grow`

```html
<div style="display: flex;">
    <div style="flex-grow: 1; border: 1px solid red;">Item 1</div>
    <div style="flex-grow: 2; border: 1px solid red;">Item 2</div>
    <div style="flex-grow: 1; border: 1px solid red;">Item 3</div>
</div>
```

- **Resultado**: `Item 2` ocupará el doble de espacio que `Item 1` y `Item 3`.

---

#### Ejemplo 2: Distribución vertical con `flex-wrap`

```html
<div style="display: flex; flex-wrap: wrap; height: 200px;">
    <div style="flex: 1 1 100px; border: 1px solid blue;">A</div>
    <div style="flex: 1 1 100px; border: 1px solid blue;">B</div>
    <div style="flex: 1 1 100px; border: 1px solid blue;">C</div>
    <div style="flex: 1 1 100px; border: 1px solid blue;">D</div>
</div>
```

- **Resultado**: Los items `A`, `B`, `C` y `D` se ajustarán a nuevas filas si no caben.

#### Ejemplo 3: Uso de `margin: auto`

```html
<div style="display: flex;">
    <div>Item 1</div>
    <div>Item 2</div>
    <div style="margin-left: auto;">Item 3</div>
</div>
```

- **Resultado**: `Item 3` estará alineado a la derecha, mientras que `Item 1` y `Item 2` quedarán a la izquierda.

#### Ejemplo Base:

```html
<div class="l-flex l-flex--direction-row l-flex--justify-content-center">
  <div clas="l-flex__area">Item1</div>
  <div clas="l-flex__area">Item2</div> 
  <div clas="l-flex__area l-flex__area--grow-2 ">Item3</div>
  <div clas="l-flex__area">Item4</div> 
  <div clas="l-flex__area">Item5</div> 
</div>
```

```css
.l-flex {
  display:flex;
}
 
 
.l-flex--direction-row {
  flex-direction:row
}
 
.l-flex--justify-content-center {
  justify-content:center
}
 
.l-flex__area--grow-2 {
  flex-grow:2
}
```

---
## Grid Layout 


El sistema **CSS Grid** permite organizar contenido en dos dimensiones: filas y columnas. A diferencia de **Flexbox**, diseñado para layouts en una sola dimensión (horizontal o vertical), **Grid** facilita la creación de diseños más complejos mediante rejillas.

### **Propiedades Básicas**

#### **Definir un contenedor Grid**

```css
.container {
    display: grid;
}
```

Esto transforma al elemento en un contenedor Grid, permitiendo configurar filas, columnas y la distribución de sus elementos.


### **Configuración de Columnas y Filas**

#### **`grid-template-columns`**

Define el tamaño de las columnas.

- **Unidades de medida:**
    - **px**: Tamaño fijo.
    - **auto**: Se ajusta al contenido.
    - **fr**: Una fracción del espacio restante.

**Ejemplos:**

```css
.container {
    grid-template-columns: 1fr 2fr 3fr; /* 3 columnas, proporciones 1:2:3 */
    grid-template-columns: 100px auto 50px; /* Columna fija, ajustada y fija */
}
```

#### **`grid-template-rows`**

Funciona igual, pero aplica a filas.

#### **Repetir columnas o filas**

```css
.container {
    grid-template-columns: repeat(4, 1fr); /* 4 columnas iguales */
    grid-template-columns: repeat(auto-fit, 100px); /* Columnas dinámicas de 100px */
}
```

- **`auto-fit`**: Crea tantas columnas como quepan en el espacio disponible.
- **`minmax`**: Define un rango para el tamaño de las celdas.

```css
.container {
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr)); /* Mínimo 100px, máximo flexible */
}
```

### **Posicionamiento de Elementos**

#### **`gap`**

Espaciado entre celdas (horizontal y vertical).

```css
.container {
    gap: 15px; /* 15px entre filas y columnas */
    gap: 15px 10px; /* 15px entre filas, 10px entre columnas */
}
```

![](https://logongas.es/lib/exe/fetch.php?media=clase:daw:diw:1eval:grid-gap.png)
#### **`grid-column` y `grid-row`**

Permiten que un elemento ocupe varias columnas o filas.

```css
.item {
    grid-column: span 2; /* Ocupa 2 columnas */
    grid-row: span 3;    /* Ocupa 3 filas */
}
```


### **Ejemplo Práctico de Grid**

```html
<div class="container">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    <div class="item">5</div>
</div>

<style>
.container {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    gap: 10px;
}
.item {
    border: 1px solid black;
    padding: 10px;
    text-align: center;
}
</style>
```

**Explicación:**

- 3 columnas con proporciones 1:2:1.
- Separación de 10px entre celdas.
- Cada elemento ocupa una celda por defecto.

### **Ejemplo con `span`**

```html
<div class="container">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item item-span">4 (Span)</div>
    <div class="item">5</div>
</div>

<style>
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
}
.item {
    border: 1px solid black;
    text-align: center;
    padding: 10px;
}
.item-span {
    grid-column: span 2;
}
</style>
```

**Resultado:** El elemento 4 ocupa dos columnas.

### **Grid y Responsividad**

#### **Ejemplo Responsivo:**

```css
.container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    gap: 15px;
}
```

**Comportamiento:**

- Cada celda tendrá un mínimo de 100px.
- Si hay espacio adicional, las celdas se expanden.
- Las filas se ajustan automáticamente para acomodar más elementos.

---
## Comparativa: Grid vs Flexbox

|**Características**|**Grid**|**Flexbox**|
|---|---|---|
|**Dimensiones**|2D (filas y columnas)|1D (fila o columna)|
|**Distribución Compleja**|Ideal para layouts completos|Ideal para alineación lineal|
|**Auto-ajuste**|Soporte con `auto-fit` y `minmax`|Limitado a elementos flexibles|

**Conclusión:**

- Usa **Grid** para layouts en dos dimensiones (tablas, rejillas).
- Usa **Flexbox** para alineación simple o distribuciones en una dimensión (menús, botones).

---

![[css3-cheatsheet-lite.pdf]]

