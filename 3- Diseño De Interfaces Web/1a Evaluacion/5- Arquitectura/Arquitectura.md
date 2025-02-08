# ARQUITECTURA

Debemos organizar las clases CSS de una manera estructurada y mantenible, para ello podermos usar una metodología conocida como **BEM** (Block, Element, Modifier). Esta metodología se utiliza para evitar el caos en el código CSS y mejorar la escalabilidad de los proyectos. Aquí te explico los conceptos clave que mencionas:

## 1. **BEM: Metodología de Nombres en CSS**

BEM es una convención de nombres para clases CSS que ayuda a hacer el código más claro y modular. Los nombres de las clases están estructurados en tres partes principales:

- **Bloques (Block)**: Un bloque es una parte independiente de la interfaz de usuario. Es un componente reutilizable que puede incluir otros elementos dentro de él. Por ejemplo, un bloque puede ser un panel, un botón o un menú.

    **Ejemplo**: `c-panel` (donde "c" es un prefijo que indica que es un bloque visual).

- **Elementos (Element)**: Son las partes internas de un bloque. Estos no pueden existir por sí solos, solo dentro de un bloque. Se indican con el nombre del bloque seguido de dos guiones `__`.

    **Ejemplo**: `c-panel__titulo` (el título dentro del bloque `c-panel`).

- **Modificadores (Modifier)**: Se utilizan para modificar el estilo de un bloque o elemento, normalmente para cambiar su apariencia o comportamiento (por ejemplo, un color diferente, un tamaño distinto, etc.). Se añaden después del nombre del bloque o elemento, separadas por dos guiones `--`.

    **Ejemplo**: `c-panel--warning` (un modificador de color para un bloque `c-panel` que aplica un estilo de advertencia).

---
## 2. **Estructura de Clases**

Las clases de CSS se organizan de la siguiente manera:

- **Clase de Bloque**: Se define con el nombre del componente, precedido por un prefijo `c-`. Ejemplo: `c-button`, `c-header`.
- **Clase de Elemento**: Se define combinando el nombre del bloque y el nombre del elemento, separados por `__`. Ejemplo: `c-button__icon`.
- **Clase de Modificador**: Se añade un modificador al nombre del bloque o elemento, precedido por `--`. Ejemplo: `c-button--primary`.

---
## 3. **Bloques y Elementos**

En el ejemplo de un panel:

```html
<div class="c-panel">
    <div class="c-panel__titulo">Cabecera</div>
    <div class="c-panel__contenido">Contenido</div>
</div>
```

- El bloque es `c-panel`.
- Los elementos dentro de este bloque son `c-panel__titulo` y `c-panel__contenido`.

---
## 4. **Modificadores**

Si quieres que un bloque tenga una variante (por ejemplo, un panel con un color de advertencia), puedes agregar un modificador al bloque y a sus elementos:

```html
<div class="c-panel c-panel--warning">
    <div class="c-panel__titulo c-panel__titulo--warning">Cabecera</div>
    <div class="c-panel__contenido c-panel__contenido--warning">Contenido</div>
</div>
```

Aquí, `c-panel--warning` es el modificador que cambia el estilo del panel, y también se aplican modificadores a los elementos como `c-panel__titulo--warning`.

---
## 5. **Prefijos de Clases**

Además de los bloques de tipo "componente", existen otros tipos de bloques:

- **`l-`**: Para bloques de tipo **layout**, que se usan para organizar otros bloques en la página.

    **Ejemplo**: `l-page` (es un layout que organiza el contenido de la página).

- **`g--`**: Para modificadores **globales** que afectan a todos los componentes. Se utilizan para aspectos comunes como márgenes, paddings, etc.

    **Ejemplo**: `g--margin-4` (modificador global para márgenes).

---
## 6. **Estructura de Archivos**

En proyectos grandes, es importante organizar los archivos CSS (o SASS) de manera estructurada. Aquí hay una sugerencia de cómo organizar los archivos SASS según la metodología BEM:

```
/css
    main.css
/scss
    /01_utilities
        _css-variables.scss
        _functions.scss
    /02_base
        _reset.scss
        _typography.scss
    /03_layout
        _l-page.scss
    /04_components
        _c-button.scss
        _c-panel.scss
    /05_pages
        _page-home.scss
    /06_global
        _g--margin.scss
    main.scss
```

- **`01_utilities`**: Archivos de utilidades como variables y mixins.
- **`02_base`**: Estilos básicos como reset de CSS y tipografía.
- **`03_layout`**: Estilos para los bloques de layout (por ejemplo, la estructura de la página).
- **`04_components`**: Estilos para los bloques de tipo componente (botones, paneles, etc.).
- **`05_pages`**: Estilos específicos de páginas concretas.
- **`06_global`**: Estilos globales como márgenes o padding que se usan en todo el proyecto.

![[arquitecturaEsquema.png]]

*Script de Creación automática*:

```bash
#!/bin/bash

# Crear la estructura de carpetas
mkdir -p css
mkdir -p scss/{01_utilities,02_base,03_layout,04_components,05_pages,06_global}

# Crear los archivos necesarios
touch css/main.css
touch scss/01_utilities/{_css-variables.scss,_functions.scss}
touch scss/02_base/{_reset.scss,_typography.scss}
touch scss/03_layout/_l-page.scss
touch scss/04_components/{_c-button.scss,_c-panel.scss}
touch scss/05_pages/_page-home.scss
touch scss/06_global/_g--margin.scss
touch scss/main.scss

echo "Estructura creada con éxito."
```

```powershell
# Crear la estructura de carpetas
New-Item -ItemType Directory -Path css
New-Item -ItemType Directory -Path scss\01_utilities
New-Item -ItemType Directory -Path scss\02_base
New-Item -ItemType Directory -Path scss\03_layout
New-Item -ItemType Directory -Path scss\04_components
New-Item -ItemType Directory -Path scss\05_pages
New-Item -ItemType Directory -Path scss\06_global

# Crear los archivos necesarios
New-Item -ItemType File -Path css\main.css
New-Item -ItemType File -Path scss\01_utilities\_css-variables.scss
New-Item -ItemType File -Path scss\01_utilities\_functions.scss
New-Item -ItemType File -Path scss\02_base\_reset.scss
New-Item -ItemType File -Path scss\02_base\_typography.scss
New-Item -ItemType File -Path scss\03_layout\_l-page.scss
New-Item -ItemType File -Path scss\04_components\_c-button.scss
New-Item -ItemType File -Path scss\04_components\_c-panel.scss
New-Item -ItemType File -Path scss\05_pages\_page-home.scss
New-Item -ItemType File -Path scss\06_global\_g--margin.scss
New-Item -ItemType File -Path scss\main.scss

Write-Host "Estructura creada con éxito."
```

