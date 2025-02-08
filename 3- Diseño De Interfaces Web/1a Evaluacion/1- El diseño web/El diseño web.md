# EL DISEÑO WEB

## Conceptos básicos

- **Framework CSS**: Es una colección de herramientas y estilos predefinidos que facilitan el diseño y la maquetación web, ofreciendo clases, componentes y utilidades listas para usar (por ejemplo, Bootstrap, Tailwind CSS).
- **Preprocesadores CSS**: Herramientas que extienden CSS con características como variables, anidación y mixins. Generan CSS estándar a partir de un código más organizado (por ejemplo, Sass, LESS).
- **Postprocesadores CSS**: Herramientas que optimizan o transforman el CSS ya escrito, agregando compatibilidad con navegadores o mejoras automáticas (por ejemplo, PostCSS).

## Normas de diseño

1. Las cosas que no estén relacionadas, con bastante separación.
2. Los diseño no tienen que ocupar el 100% de la pantalla ya que en pantallas muy grandes queda mal.
3. Haz que las cosas estén alineadas a una recta imaginaria que va de arriba a abajo.
4. Resalta lo importante
5. Repele la atención de lo que no es importante (más pequeño, más espacioso, de menor contraste).
6. Evita usar `label` o `captions`. Si ves `ventas@persianas.com` ya sabes que es un correo, no hace falta indicar que es el correo. Pero si usas un `label` que forme parte de una frase. "3 en stock" en vez de "Stock:3". Y aun así, si las usas, que estén desenfatizadas
7. Los títulos `<h1>` no tienen porque destacar ya que a veces no son importantes ya que es obvio el título. `<h1>` es para que el buscador sepa que eso es importante (SEO).
8. Las esquinas cuadradas indican seriedad. Las Esquinas muy muy redondeadas son muy informales.`(border-radious`)
9. Para enfatizar en vez de un mayor tamaño de letra, usa negrita. Pero para desenfatizar, usa un color de letra gris en vez del negro del texto.
10. Nunca usar un carrusel.

## Colores

Los colores de pueden definir en CSS con formato RGB o HSL.
Una web necesita muchos colores, un ejemplo de una paleta de colores sería la siguiente:

![[colors.png]]
### Color Alternativo VS Principal

En diseño, los conceptos de **color principal** y **color alternativo** son fundamentales para crear una identidad visual coherente:

- **Color principal**: Es el color predominante que representa la marca o diseño. Se usa para destacar elementos clave como el logo, encabezados o botones principales. Ejemplo: el azul en Facebook.

- **Color alternativo**: Es un color complementario o secundario que acompaña al principal. Se utiliza para contrastar, equilibrar o diferenciar secciones menos destacadas, como botones secundarios o fondos. Ejemplo: el verde en WhatsApp frente a su azul secundario.

>[!NOTE]
>La gama de blancos y grises la usas para hacer las cosas muy claras u oscuras. La gama del color principal obviamente la usas para casi todo, mientras que la gama del color alternativo la usas para destacar algo. Por último, los colores rojo, verde, amarillo, etc, son para cosas concretas que necesitan ese color. Por ejemplo para avisar del borrado de algo usar el rojo.


## La Luz Viene del Cielo

Las cosas que están "**encima**" debe ser **más claras** que las que están abajo.

![[luzCielo.png]]

## Contraste de Colores

Al hacer un interfaz de usuario, hay que jugar con dos colores que hagan contraste. Como por ejemplo:

Rueda de colores de contraste:

![[ruedaContraste.png]]

## Botones

Los botones tienen 2 características:

- *Importancia*: Es si queremos o no que el usuario pulse ahí. A mayor importancia es que queremos que mas veces pulse en ese botón.
- *Función*: Es para decir al usuario que tipo de acción está realizando. Por ejemplo , la función "Peligrosa" es roja y nos quiere decir que tengamos cuidado al pulsar ahí.

| **Importancia** | **Función** | **Primaria**                         | **Secundaria**                       | **Terciaria**                        |
| --------------- | ----------- | ------------------------------------ | ------------------------------------ | ------------------------------------ |
| **Normal**      |             | ![[normalPrimaria.png]] | ![[normalSecundaria.png]] | ![[normalTerciaria.png]] |
| **Alternativa** |             | ![[alternativaPrimaria.png]] | ![[alternativaSecundaria.png]] | ![[alternativaTerciaria.png]] |
| **Peligrosa**   |             | ![[peligrosaPrimaria.png]] | ![[peligrosaSecundaria.png]] | ![[peligrosaTerciaria.png]] |

## Sistema de tamaños

Al igual que en los colores nos ceñimos a un conjunto limitado de colores, se debe hacer lo mismo con los tamaños de margenes, fuentes, etc.

#### Padding o Margin

```css
0px, 4px, 6x, 8px, 10px, 12px, 16px, 20px, 24px, 32px, 40px, 48px, 64px, 80px, 96px, 128px, 160px, 192px, 224px, 256px, 320px, 480px, 640px
```
#### Tamaño de fuente

```css
12px, 14px, 16px, 18px, 20px, 24px, 30px, 36px, 48px, 64px
```
#### Border Radius

```css
0px, 2px, 4px, 6px, 8px, 16px
```

>[!NOTE]
>Obviamente se puede elegir los tamaños que se deseen pero se tiene que tener en cuenta que a mayor tamaño , mas debe ser el incremento entre uno y otro.

## Experiencia de usuario

La experiencia de usuario es conseguir que el usuario se sienta cómodo usando la aplicación (**UX**).






