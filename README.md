# Reservamos CSS / Sass Styleguide
Guía de estilos para código CSS / SSCC

## Objetivos
- Utilizar el menor código posible
- Reutilizar el mayor código posible
- SCSS Escalable
- HTML semántico
- Estandarizar Font-Styles
- Tener un Color System

## Instalación
Instrucciones para usar stylelint para enforzar ciertas reglas en la [wiki](https://github.com/reservamos/css/wiki/Installation)

## Tabla de contenido

1. [Estructura Scss](#estructura-scss)
    - [Index](#index)
    - [White Label Color System](#white-label-color-system)
    - [Default Color System](#default-color-system)
    - [Lib Variables](#lib-variables)
    - [Lib Mixins](#lib-mixins)
    - [Lib Font-Styles](#lib-font-styles)
    - [White Label](#white-label)
1. [SCSS](#scss)
    - [Formato](#formato)
    - [Declaración de Propiedades](#declaración-de-propiedades)
    - [Clases Anidadas](#clases-anidadas)
    - [Reutilizar Código](#reutilizar-código)
    - [Bordes](#bordes)
    - [Comentarios](#comentarios)
    - [Colores](#colores)
    - [Mixins](#mixins)
    - [SVG icons](#svg-icons)
    - [Variables](#variables)
1. [Font-Styles: Mixin v Extend](#font-styles-mixin-v-extend)
    - [Mixin](#mixin)
    - [Extend](#extend)
    - [Each Loops](#each-loops)
1. [Back to the basics](#back-to-the-basics)
    - [HTML 5](#html-5)
        - [Atributos](#atributos)
        - [div, p and span tags](#div-p-and-span-tags)
        - [Label tag](#label-tag)
    - [Bourbon Hints](#bourbon-hints)
        - [12 columnas](#12-columnas)
        - [Clearfix](#clearfix)
    - [Finder](#finder)

---

# Estructura Scss

Estructura de las hojas de estilos de Reservamos.

```
styles/
|
|-- lib/                    # Principal Styles
|   |-- _index.scss         # Imports for all theme styles
|   |-- _wl-colorsys.scss   # Default overrides of the White Label theme
|   |-- _default.scss       # Default styles for the Reservamos theme
|   |-- _variables.scss     # Variables
|   |-- _mixins.scss        # Mixins
|   |-- _fontstyles.scss    # Font-Styles extends
|   |-- _white-label.scss   # WL Override variables and Font-Styles
|   ...
|
|-- general/                # General styles for the project
|   ...
|
|-- components/             # Components styles
|   ...
|
`-- app.scss                # Primary Scss file
```

**[⬆ back to top](#tabla-de-contenido)**

## index

`_index.scss`

```
@import "wl-colorsys";
@import "default";
@import "variables";
@import "mixins";
@import "Font-Styles";
@import "white-label";
```

**[⬆ back to top](#tabla-de-contenido)**

## White Label Color System

`_wl-colorsys.scss`

En esta hoja únicamente se incluirán los valores para el sistema de colores y la tipografía principal del white-label.

- Ninguno de los valores de las variables incluirá la etiqueta `!default`.

**[⬆ back to top](#tabla-de-contenido)**

## Default Color System

`_defult.scss`

En esta hoja solo estarán los valores del sistema de colores y la tipografía principal de Reservamos (denominado; tema Default).

1. Principal font-family
2. Primary color scale
3. Accent color scale
4. Gray color scale
5. Complementary colors

- Cada valor declarado en esta hoja incluirá la etiqueta `!default` al final.
- Para futuros diseños se debe tomar en cuenta los colores que están en este sistema
- Para agregar o modificar alguna variable se tendrá que evaluar con el equipo de diseño para encontrar la mejor solución

**[⬆ back to top](#tabla-de-contenido)**

## Lib Variables

`_variables.scss`

En esta hoja se encuentran todas las variables del proyecto.
Cada componente que pueda ser utilizado en los white-labels deberá contar con variables las cuales estarán en este archivo.

- Las únicas variables asignadas como valor, serán las que pertenecen al archivo `_default.scss`
- Es preferible evitar utilizar colores únicos.
- No utilizar variables que solamente sean usadas en esta hoja
- No utilizar variables que solamente sean usadas en la hoja de fontsyles

**[⬆ back to top](#tabla-de-contenido)**

## Lib Mixins

`_mixins.scss`

En esta hoja están los mixins que se usan en todo el proyecto.

**[⬆ back to top](#tabla-de-contenido)**

## Lib Font-Styles

`_fontstyles.scss`

En esta hoja solamente estarán incluidos los `font-styles` que son utilizados en los white-labels o que se puedan utilizar para facilitar la modificación de los mismos.

- Para declarar cada `font-style` se usarán extends
- Cada extend comenará con `%font...`
- No deberán de existir variables únicas para definir el color, familia, o peso para los Font-Styles que utilicen extends
- Al igual que en la hoja de `_variables.scss`, los colores y la tipografía deberán de estar declarados con la variable de la hoja `_default.scss`
- Evitar usar colores únicos

**[⬆ back to top](#tabla-de-contenido)**

## White Label

`_white-label.scss`

En esta hoja está dedicada únicamente a todas las correcciones que sean necesarias para el funcionamiento del White Label.
La hoja se dividirá en dos partes para tener una mejor organización.

- Primera parte: Variables
- Segunda parte: Font-Styles extends

**[⬆ back to top](#tabla-de-contenido)**

---

# SCSS

## Formato

- Utilizar syntaxis de SCSS
- Por legibilidad usar dos espacios simples para indentación (no usar tab)
- Preferible usar guiones en lugar de camelCasing en los nombres de clases
- No utilizar selectores ID
- Al usar múltiples selectores en una declaración, cada selector deberá de tener su propia línea
- Agregar un espacio antes de un bracket abierto `{`
- En las propiedades, solamente agregar un espacio después de `:`
- El bracket cerrado `}` deberá estar en una línea nueva
- Agregar una línea en blanco entre cada clase

###### Bad

```
.trip{
    border-radius:50%;
    border:1px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```

###### Good

```
.trip {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

**[⬆ back to top](#tabla-de-contenido)**

## Declaración de propiedades

- Ordenar las propiedades alfabéticamente
- Colocar los `@include` al principio de las propiedades
- Clases anidadas estarán al final; Se brincará una línea en blanco entre la última propiedad y la clase anidada

```
.footer {
  @include position(fixed, null 0 0 0);
  background-color: white;
  border-top: $border-footer;
  height: 40px;
  padding: 10px 15px;

  ul {
    margin: 0;
    padding: 0;
  }
}
```

**[⬆ back to top](#tabla-de-contenido)**

## Clases anidadas

No anidar clases más de tres niveles de profundidad.

```
.page-container {
  .content {
    .element {
      // DONE!
    }
  }
}
```

Cuando las clases se vuelven tan largas, es probable que escribamos SCSS que sea:

- Fuertemente acoplado al HTML (frágil)
- Muy específico (poderoso)
- No reutilizable

>Again: **never nest ID selectors!**

**[⬆ back to top](#tabla-de-contenido)**

## Reutilizar código

- Al pegar bloques de código que procedan de otros proyectos revisarlo con el fin de evitar que no tengamos código duplicado o que contenga código que no se utilice.

**[⬆ back to top](#tabla-de-contenido)**

## Bordes

Utilizar `0` en lugar de `none` para especificar que un estilo no tiene borde.

###### Bad

```
.button {
  border: none;
}
```

###### Good

```
.button {
  border: 0;
}
```

**[⬆ back to top](#tabla-de-contenido)**

## Comentarios

- Usar preferentemente los comentarios inline `//` de SCSS a los comentarios de bloque `/*`, `*/` de CSS
- Brincar un espacio simple después de `//` en los comentarios
- Comentarios van en una sola línea y no al final de la línea

**[⬆ back to top](#tabla-de-contenido)**

## Colores

- Usar colores en su valor hexadecimal con mayúsculas `#CE348B`
- Al usar colores en RGBA también es posible usarlos con su valor hexadecimal
`rgba(#A1A1A1, 0.5)` ó `rgba(white, 0.3)`
- Es preferible usar la variable del ColorSystem en lugar de usar el color en su valor hexadecimal
`$primary-700`, `$accent-500`
- Usar string `black` en lugar de `#000000`
- Usar string `white` en lugar de `#FFFFFF`

**[⬆ back to top](#tabla-de-contenido)**

## Mixins

Los mixins serán utilizados para compactar el código, agregar claridad o complejidad abstracta de la misma manera que las funciones.

- No usar mixins como `@extend`

**[⬆ back to top](#tabla-de-contenido)**

## SVG icons

Usar imágenes en SVG nos simplificará el proceso de reemplazar imágenes en los white-labels, ya que desde el código podemos cambiar solamente el valor del color sin tener que abrir algún programa como illustrator para editar el archivo.

**[⬆ back to top](#tabla-de-contenido)**

## Variables

- Es preferible usar guiones en lugar de camelCasing en los nombres
- No utilizar variables con nombres específicos:
`$white: #ffffff;`, `$black: #000000;`
- Utilizar nombres que puedan ser escalables incluso en diferentes proyectos como White Labels
`$principal-font`, `$color-success`
- Es preferible no utilizar variables únicas para modificar Font-Styles (`$summary-font-weight`), es mejor crear un extend para modificar los estilos
- Evitar el uso de variables que solo sean utilizadas en la hoja: `_variables.scss`
- Las listas de variables que sean utilizadas para algún `@each`loop deben ser declaradas en las primeras líneas de la misma hoja Scss del componente

**[⬆ back to top](#tabla-de-contenido)**

---

# Font-Styles: Mixin v Extend

Lo común para editar un White Label es que en su hoja de estilos solamente sean agregadas las correcciones necesarias para su funcionamiento, aprovechando las propiedades del tema Default y que no cuente con código duplicado que ya se encuentra en los estilos Default.

Aplicando ésta lógica para hacer las correcciones teniendo `@mixin` en los Font-Styles no nos sería posible ya que el funcionamiento del mixin es parecido al de las variables; al sobrescribir su valor éste último que declaremos será el valor en los estilos de salida y se perderían las propiedades que anteriormente fueron asignadas a ese mixin.

Reservamos: `_fontstyles.scss`

```
@mixin payment-methods-link-font {
  @include font-styles($color-info, $principal-font, 14px, 400, normal);
}
```

White Label: `_white-label.scss`

```
@mixin payment-methods-link-font {
  color: $gray-900;
}
```

`Output CSS:`

```
.payment-methods-link-font {
 color: #4A4A4A;
}
```

**[⬆ back to top](#tabla-de-contenido)**


## Mixin

En este ejemplo el color es la única propiedad diferente al tema Default, pero para poder tener las propiedades de `font-family`, `font-size`, etc. anteriormente asignados en el tema Default es necesario volver a usar el `@include` completo.


Reservamos: `_fontstyles.scss`

```
@mixin payment-methods-link-font {
  @include font-styles(red, $principal-font, 14px, 400, normal);
}
```

White Label: `_white-label.scss`

```
@mixin payment-methods-link-font {
  @include font-styles(blue, $principal-font, 14px, 400, normal);
}
```

`Output CSS:`

```
.payment-methods-link-font {
 color: blue;
 font-family: OpenSans;
 font-size: 14px;
 font-weight: 400;
}
```

**[⬆ back to top](#tabla-de-contenido)**


## Extend

Usando `@extend` lograremos seguir utilizando (realmente) las propiedades del tema Default y en la hoja del White Label únicamente tener las correcciones necesarias para el tema.

Reservamos: `_fontstyles.scss`

```
%payment-methods-link-font {
  @include font-styles(red, $principal-font, 14px, 400, normal);
}
```

White Label: `_white-label.scss`

```
%payment-methods-link-font {
  color: blue;
}
```

`Output CSS:`

```
.payment-methods-link-font {
 color: blue;
}

.payment-methods-link-font {
 ~~color: red;~~
 font-family: OpenSans;
 font-size: 14px;
 font-weight: 400;
}
```

### Nota:

Para dar de alta algún extend en la hoja `_fontstyles.scss`; en los casos que cuente con alguna variable especifica (que solo sea utilizada en un lugar) como `$summary-font-color` o `$summary-font-weight;`, la variable se tiene que deshabilitar y se agregará el valor de esa variable directamente al nuevo extend en la hoja  `_fontstyles.scss`.

###### Bad

```
// Variables _variables.scss

$font-color-error: red;

// Font-Styles _fontstyles.scss

%error-font {
  @include font-styles($font-color-error, $principal-font, 14px, 400, normal);
}

// WhiteLabel _white-label.scss

$font-color-error: blue;

// Output:
.error-font {
  color: red;
  font-family: OpenSans;
  font-size: 14px;
  font-weight: 400;
}
```

###### Good

```
// Font-Styles _fontstyles.scss

%error-font {
  @include font-styles(red, $principal-font, 14px, 400, normal);
}

// WhiteLabel _white-label.scss

%error-font {
  color: blue;
}

// Output:
.error-font {
 color: blue;
}
.error-font {
 ~~color: red;~~
 font-family: OpenSans;
 font-size: 14px;
 font-weight: 400;
}
```

**[⬆ back to top](#tabla-de-contenido)**

## Each Loops

En este ejemplo utilizamos un `@each` para declarar seis clases diferentes con las mismas propiedades.

De esta manera ahorramos líneas de código sin dejar de cubrir la posibilidad de que alguna de ellas tenga estilos diferentes en el White Label.

###### Bad

```
.g-input-placeholder {
 @include font-styles($gray-600, $principal-font, 14px, 400, normal);
 }

.g-select-font {
 @include font-styles($gray-600, $principal-font, 14px, 400, normal);
 }

.checkboxes-label-font {
 @include font-styles($gray-600, $principal-font, 14px, 400, normal);
 }

.checkboxes-label-disabled-font {
 @include font-styles($gray-600, $principal-font, 14px, 400, normal);
 }

.itinerary-button-font {
 @include font-styles($gray-600, $principal-font, 14px, 400, normal);
 }

.payment-methods-description-font {
 @include font-styles($gray-600, $principal-font, 14px, 400, normal);
 }
```

###### Good

```
$gray600-p14-400: g-input-placeholder,
g-select-font,
checkboxes-label-font,
checkboxes-label-disabled-font,
itinerary-button-font,
payment-methods-description-font;
@each $styleclass in $gray600-p14-400 {
  %#{$styleclass} {
    @include font-styles($gray-600, $principal-font, 14px, 400, normal);
  }
}
```

**[⬆ back to top](#tabla-de-contenido)**

---

# Back to the basics

> Always keep your code tidy, clean, and well-formed.

## HTML 5

#### Atributos

- Usar atributos en minúsculas

###### Bad

```
<div CLASS="menu">
```

###### Good

```
<div class="menu">
```

**[⬆ back to top](#tabla-de-contenido)**

---

#### div, p and span tags

- Por semántica de HTML, no escribir texto dentro de un `<div>` sin alguna etiqueta `<p>` o `<span>` que englobe el texto

###### Bad

```
<div>
  Some text...
</div>
```

###### Good

```
<div>
  <p class="class-name">Some text...</p>
</div>
```

---

- No utilizar `<div>`'s dentro de la etiqueta `<p>` o `<span>`

###### Bad

```
<p class="class-name">Some text... <div class="small-text">Small text</div></p>
```

###### Good

```
<p class="class-name">Some text... <span class="small-text">Small text</span></p>
```

---

- No utilizar etiquetas `<span>` innecesesarias

###### Bad

```
<div class="star-wrap">
  <span>
    <i class="star-item"></i>
  </span>
  <span>
    <i class="star-item"></i>
  </span>
  <span>
    <i class="star-item"></i>
  </span>
  <span>
    <i class="star-item"></i>
  </span>
  <span>
    <i class="star-item empty"></i>
  </span>
</div>
```

###### Good

```
<div class="star-wrap">
  <i class="star-item"></i>
  <i class="star-item"></i>
  <i class="star-item"></i>
  <i class="star-item"></i>
  <i class="star-item empty"></i>
</div>
```

**[⬆ back to top](#tabla-de-contenido)**

---

#### Label tag

- Usar la etiqueta `<label>` únicamente para ligar texto a algún input
- No utilizar `.label` para declarar alguna clase

###### Bad

```
<div class="ts-stopover">
  <span class="label">Paradas:</span>
  <label class="ts-item">1</label>
</div>
```

###### Good

```
<div class="ts-stopover">
  <p class="ts-label">Paradas:
  <span class="ts-item">1</span></p>
</div>
```

###### Much Better

```
<label for="Name">Click me</label>
<input type="text" placeholder="Name" />
```

**[⬆ back to top](#tabla-de-contenido)**

---

## Bourbon hints

No utilizar funciones de bourbon cuando sea más sencillo escribir directamente la propiedad que necesitamos. De esta manera será más sencillo leer el código sin tener que investigar la función.

Ejemplo: Utilizar `margin-right: 0;` en lugar de `@include omega();`

```
// SCSS
.element-one {
  @include omega;
}
.element-two {
  margin-right: 0;
}
```

`Output CSS:`

```
.element-one {
  margin-right: 0;
}
.element-two {
  margin-right: 0;
}
```

**[⬆ back to top](#tabla-de-contenido)**

---

#### 12 columnas

En ocasiones utilizamos 12 columnas cuando en realidad no son necesarias, un claro ejemplo es cuando utilizamos `l-container`.

El div `l-container` debe ser usado teniendo en mente que es un ROW centrado (horizontalmente), con `width: 100%` de nuestro layout.

###### Bad (...)

```
// White Container Mixin
@mixin white-container {
  @include span-columns(12);
  box-shadow: $tp-shadow;
  background-color: white;
  padding: 0;
}

// SCSS
.trip-provider {
  @include span-columns(12);
  padding-bottom: 30px;
  ...

  .tp-container {
    @include span-columns(12);
    @include white-container;
    padding: 0 20px;
    ...
  }

  .tp.left {
    ...
  }
}

// HTML
<div class="trip-provider">
  <div class="l-container">
    <div class="tp-container">
      <div class="tp-left">
      </div>
    </div>
  </div>
</div>
```

`Output CSS:`

```
.trip-provider {
  float: left;
  display: block;
  margin-right: 2.35765%;
  width: 100%;
  padding-bottom: 30px;
  position: relative;
}

.tp-container {
  ~~float: left;~~
  ~~display: block;~~
  ~~margin-right: 2.35765%;~~
  ~~width: 100%;~~
  float: left;
  display: block;
  ~~margin-right: 2.35765%;~~
  width: 100%;
  box-shadow: 0px 2px 2px 0px rgba(151, 151, 151, 0.5);
  background-color: white;
  ~~padding: 0;~~
  max-height: 150px;
  min-height: 150px;
  padding: 0 20px;
  position: relative;
}
```

###### Much better

```
// White Container Mixin
%white-container {
  background: white;
  box-shadow: $tp-shadow;
  padding: 0 20px;
}

// SCSS
.trip-provider {
  padding-bottom: 30px;
  ...

  .tp-container {
    @extend %white-container; // refactored mixin...
    ...
  }

  .tp.left {
    ...
  }
}

// HTML
<div class="trip-provider">
  <div class="l-container">
    <div class="tp-container">
      <div class="tp-left">
      </div>
    </div>
  </div>
</div>
```

`Output CSS:`

```
.trip-provider {
  padding-bottom: 30px;
  position: relative;
}

.tp-container {
  box-shadow: 0px 2px 2px 0px rgba(151, 151, 151, 0.5);
  background-color: white;
  max-height: 150px;
  min-height: 150px;
  padding: 0 20px;
  position: relative;
}
```

###### Even better

```
// White Container Mixin
%white-container {
  background: white;
  box-shadow: $tp-shadow;
  padding: 0 20px;
}

// SCSS
.trip-provider {
  padding-bottom: 30px;
  ...

  .tp-container {
    @extend %white-container; // refactored mixin...
    ...
  }

  .tp.left {
    ...
  }
}

// HTML
<div class="trip-provider">
  <div class="tp-container"> // .l-container merged
    <div class="tp-left">
    </div>
    ...
  </div>
</div>
```

`Output CSS:`

```
.trip-provider {
  padding-bottom: 30px;
  position: relative;
}

.tp-container {
  max-width: 1200px;  (.l-container style extended)
  margin-left: auto;  (.l-container style extended)
  margin-right: auto; (.l-container style extended)
  box-shadow: 0px 2px 2px 0px rgba(151, 151, 151, 0.5);
  background-color: white;
  max-height: 150px;
  min-height: 150px;
  padding: 0 20px;
  position: relative;
}
```

---

###### Bad

```
//SCSS
.payment-section {
  @include span-columns(12);
  ...

  .section-content {
    @include span-columns(12);
    ...
  }

  .section-title {
    ...

    h2 {
      ...
    }
  }
}

// HTML
<div class="payment-section">
  <div class="l-container">
    <div class="section-content">
      <div class="section-title">
        <h2>Title</h2>
      </div>
    </div>
  </div>
</div>
```

###### Good

```
// SCSS
.payment-section {
  ... // margin-top and margin-bottom

  .section-content {
    @include span-columns(12);
    ...
  }

  .section-title {
    ...

    h2 {
      ...
    }
  }
}

//HTML
<div class="payment-section">
  <div class="l-container">
    <div class="section-content">
      <div class="section-title">
        <h2>Title</h2>
      </div>
    </div>
  </div>
</div>
```

###### Much Better

```
// SCSS
.payment-section {
  ... // margin-top and margin-bottom

  .section-content {
    // padding
    ...
  }

  .section-title {
    ...

    h2 {
      ...
    }
  }
}

//HTML
<div class="payment-section">
  <div class="l-container section-content">
    <div class="section-title">
        <h2>Title</h2>
      </div>
  </div>
</div>
```

**[⬆ back to top](#tabla-de-contenido)**

---

### Clearfix

Clearfix aplica un "break" para el contenido flotado, debe ser utilizado en casos cuando no se utilice algún contenedor como `l-container` y cuando se requiera obtener un brinco de línea cuando el total de columnas sea menor a 12.

###### Bad

```
// SCSS
.payment-content {
  @include span-columns(12);
  ...
}

//HTML
<div class="payment-content">
  ...
</div>
<div class="payment-content">
  ...
</div>
```

###### Good

```
// SCSS
.payment-content {
  @include span-columns(12);
  @include clearfix;
  ...
}

//HTML
<div class="payment-content">
  ...
</div>
<div class="payment-content">
  ...
</div>
```

---

###### Bad

```
// SCSS
.content-4col,
.payment-side {
  @include span-columns(4);
  ...
}


//HTML
<div class="content-4col">
  ...
</div>
<div class="payment-side">
  ...
</div>
```

###### Good

```
// SCSS
.content-4col,
.payment-side {
  @include span-columns(4);
  @include clearfix;
  ...
}

.payment-side {
  @include clearfix;
}

//HTML
<div class="content-4col">
  ...
</div>
<div class="payment-side">
  ...
</div>
```

**[⬆ back to top](#tabla-de-contenido)**

---

## Finder

Para una mejor organización y facilitar la localización de las imágenes es recomendable que los nombres de los archivos se encuentren agrupados y se puedan ordenar alfabéticamente.

De esta manera las imágenes no quedarían dispersas dentro de la carpeta del proyecto y tendríamos identificados los diferentes grupos de imágenes

###### Bad

```
duration-floating-icon.png
location-floating-icon.png
sort-floating-icon.png
```

###### Good

```
floating-icon-duration.png
floating-icon-location.png
floating-icon-sort.png
```

**[⬆ back to top](#tabla-de-contenido)**
