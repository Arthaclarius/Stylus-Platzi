Stylus
=====

<!-- TOC -->

- [1. Introducción al curso](#1-introducción-al-curso)
  - [1.1. UI/Copiladores](#11-uicopiladores)
    - [1.1.1. [Codekit](https://codekitapp.com/) - Trial|$34](#111-codekithttpscodekitappcom---trial34)
      - [1.1.1.1. Características](#1111-características)
    - [1.1.2. [Prepos](https://prepros.io/) - Trial|$29](#112-preposhttpspreprosio---trial29)
      - [1.1.2.1. Características](#1121-características)
    - [1.1.3. [Webpack](https://platzi.com/clases/webpack/)](#113-webpackhttpsplatzicomclaseswebpack)
  - [1.2. Projecto _[PlatziMusic]-Stylus_](#12-projecto-_platzimusic-stylus_)
- [2. Cómo funciona Stylus](#2-cómo-funciona-stylus)
  - [2.1. Anidaciones](#21-anidaciones)
- [3. Instalacion Webpack](#3-instalacion-webpack)
- [4. Herramientas de Stylus](#4-herramientas-de-stylus)
  - [4.1. Variables](#41-variables)
  - [4.2. Estructura de CSS](#42-estructura-de-css)
  - [4.3. Mixins](#43-mixins)
  - [4.4. Funciones internas](#44-funciones-internas)
  - [4.5. Condicionales](#45-condicionales)
  - [4.6. Directiva For](#46-directiva-for)

<!-- /TOC -->


# 1. Introducción al curso

Stylus es un pre-procesador de css. Lo que quire decir que este código se copila para luego guardarlo en un archivo CSS. Por lo tanto se traduce del lenguaje de Stylus al lenguaje de CSS.

Stylus trabaja con NodeJS

## 1.1. UI/Copiladores

### 1.1.1. [Codekit](https://codekitapp.com/) - Trial|$34
> macOS

Build websites faster and better

Sass, Less, Stylus, CSS, CoffeeScript, Pug, Slim, Haml, TypeScript, JavaScript, ES6, Markdown, JSON, SVG, PNG, GIF and JPEG

#### 1.1.1.1. Características

* Refrescar automáticamente los navegadores
* Cualquier dispositivo
* No requiere mucha/ninguna configuración
* Optimizacion y Minificacion
* Instalación de Frameworks
* Debuger

### 1.1.2. [Prepos](https://prepros.io/) - Trial|$29
> Mac, Windows & Linux

Compile Sass, Less, Stylus, Jade, CoffeeScript on Mac, Windows & Linux with Live Browser Reload

Sass, Less, Stylus, Cssnext, Jade/Pug, Markdown, Slim, Coffeescript etc.

#### 1.1.2.1. Características

* Debuger
* Refrescar automáticamente los navegadores
* Optimizacion y Minificacion
* Prevista desde la red para distintos dispositivos
* Inspector remoto
* Temas claros y oscuros

### 1.1.3. [Webpack](https://platzi.com/clases/webpack/)
> Mac, Windows & Linux

Puedes copilarlo utilizando webpack. Lo único que requiere es que lo configures. En Platzi tiene un curso de webpack el cual enseñan a configurar webpack y también como utilizarlo con Stylus y demas pre/post-procesadores de estilos.


## 1.2. Projecto _[PlatziMusic]-Stylus_

Se recomienda __no__ guardar los estilos en la raíz. En mi caso creare una carpeta `./src` para todos los archivos "Fuentes" que utilize mi proyecto y una carpeta interna `./src/styles` para guardar los estilos no procesados. Tambien voy a requerir una carpeta `dist/css` para los output(los archivos finales).

Ahora crearemos el primer archivo en `./src/styles`

> Deberías configurar el output de tu archivo. Eso dependera de tu UI. En mi caso sera `./dist/css`

_styles.styl_
```
body
  color: red
```

_[output]/styles.css_
```
body{color:#f00}
```

# 2. Cómo funciona Stylus

En stylus no requeriremos el uso de

**{ ... }**

_css_
```
body {
  background: #lightyellow;
}
```
_stylus_
```
body
  background: lightyellow
```

**punto y coma**
_css_
```
body {
  background: #ffffe0;
  color: #2c2c2c;
}
```
_stylus_
```
body
  background: lightyellow
  color: #2c2c2c
```

**la coma**
_css_
```
body,
.light-theme {
  background: #ffffe0;
  color: #2c2c2c;
}
body .header,
.light-theme .header {
  font-family: monospace;
}
```
_stylus_
```
body
.light-theme
  background: lightyellow
  color: #2c2c2c
  .header
    font-family: monospace
```

## 2.1. Anidaciones

Con stylus tenemos acceso a hacer anidaciones interesantes.

_sub_
> Hacemos referencia a todos los elementos que estén dentro de las etiquetas padres
```
body, .light-theme
  background lightyellow
  color #2c2c2c

  .primer-hijo
    margin-bottom 24px
```

_child_
> Con el uso de ">" hacemos referencia a los hijos directos del elemento padre
```
body, .light-theme
  background lightyellow
  color #2c2c2c

  > .primer-hijo
    margin-bottom 24px
```

_reference_
> Con el uso de "&" hacemos referencia al nombre del elemento padre
```
.psudoe-element
  width 300px

  &:before
    content 'hola'
  
  .ie-8 &
    &:before
      content 'ciao'
```

> **NOTA:** No anidar mas de 3 veces

_ejemplo de modulación_
```
.btn
  background white
  color black
  border-radius 3px

  &-alert
    background red
    color white

  &-warn
    background orange
    color white
```

# 3. Instalacion Webpack
_package.json_
```
"scripts": {
  "build": "webpack --mode development",
  "build:dev": "webpack --watch --mode development",
  "build:prod": "webpack --mode production"
},
...
"devDependencies": {
  "css-loader": "^0.28.10",
  "extract-text-webpack-plugin": "^4.0.0-beta.0",
  "style-loader": "^0.20.2",
  "stylus": "^0.54.5",
  "stylus-loader": "^3.0.2",
  "webpack": "^4.1.1",
  "webpack-cli": "^2.0.10"
}
```

_index.js_
```
import '../styles/styles.styl'

console.log("styles loaded")
```

_styles.styl_
```
.btn
  background white
  color black
  border-radius 3px

  &-alert
    background red
    color white

  &-warn
    background orange
    color white

  &-info
    background lightblue
    color white
    
```

_webpack.config.js_
```
const path = require('path')
const ExtractTextPlugin = require('extract-text-webpack-plugin')

module.exports = {
  entry: path.resolve(__dirname, 'src/js/index.js'),
  output: {
    path: path.resolve(__dirname, 'dist/js'),
    filename: "index.js"
  },
  module: {
    rules: [
      {
        test: /\.styl$/,
        use: ExtractTextPlugin.extract({
          fallback: "style-loader",
          use: [
            'css-loader',
            'stylus-loader'
          ]
        })
      }
    ]
  },
  plugins: [
    new ExtractTextPlugin("stylesWP/styles.css")
  ]
}
```

# 4. Herramientas de Stylus

## 4.1. Variables

Las variables nos permiten controlar el entorno de nuestros estilos. Desde la reutilizacion de valores hasta ajustes desde un pequeño cambio.

_styles.styl_
```
// Variables
font-size-normal = 18px
font-size-small = font-size-normal - 2px
font-size-paragraph = font-size-normal

// Texts
p
  font-size font-size-paragraph

span
  font-size font-size-normal

  &.small
    font-size font-size-small
```

## 4.2. Estructura de CSS

Siguiendo el ejemplo del profesor tendríamos una estructura similar a la siguiente

* index.html
* ./src
  * ./styles
    * styles.styl
    * ./base
    * ./components
    * ./layout
    * ./lib
* ./dist
  * ./css
    * styles.css

_index.html_
```
<link rel="stylesheet" href="./dist/css/styles.css">
```

_styles.styl_
```
@import "lib/_variables.styl"
@import "lib/_mixins.styl"
@import "lib/_functions.styl"

@import "layout/_site.styl"
@import "layout/_blocks.styl"

@import "base/_links.styl"
@import "base/_buttons.styl"
@import "base/_typography.styl"
@import "base/_tables.styl"

@import "components/_grid.styl"
@import "components/_utilities.styl"
```

## 4.3. Mixins

Los mixins nos permiten agregar "funciones" que nos devuelven contenido de clases en base a los parámetros

> NOTA: Al declarar un mixin **siempre** nombrarlos con el prefijo mixin `mixin-[name] ()`

_mixins.styl_
```
mixin-max-width()
  max-width: 80%
  margin-left: auto
  margin-right: auto

.container-mixin
  margin-bott
  mixin-max-width()
```

_styles.css_
```
.container-mixin {
  max-width: 80%;
  margin-left: auto;
  margin-right: auto;
}
```

Ahora bien, si deseamos que nuestro mixin no siempre tengan el mismo valor `80%` en el caso anterior podemos usar los **Mixin Parametricos**

_mixins.styl_
```
page-max-width = 80%
mixin-max-width(width = page-max-width)
  max-width: width
  margin-left: auto
  margin-right: auto

.container-mixin
  mixin-max-width(80%)

.container 
  mixin-max-width(800px)
```

_styles.css_
```
.container-mixin {
  max-width: 80%;
  margin-left: auto;
  margin-right: auto;
}
.container {
  max-width: 800px;
  margin-left: auto;
  margin-right: auto;
}
```

## 4.4. Funciones internas
Podemos utilizar funciones, incluso mismas funciones que nos brinda stylus

_styles.styl_
```
func-grid-div(cols)
  100% / 12 * cols

.col
  &-1
    width func-grid-div(1)
  &-6
    width func-grid-div(6)
```

_styles.css_
```
.col-1 {
  width: 8.333333333333334%;
}
.col-6 {
  width: 50%;
}
```

## 4.5. Condicionales

```
func-compare(a, b)
  ifa > b
    higher
  elseif a < b
    lower
  else
    equal
```

## 4.6. Directiva For
Utilizando ciclos podemos realizar grandes cosas en css utilizando pocas lineas en Stylus

_styles.styl_
```
func-grid-div(cols)
  (100% / 12 * cols)

gridSize = (0..12)

.col
  display flex
  flex-wrap wrap
  position relative
  justify-content flex-start
  flex-direction row
  for i in gridSize
    &, &-{i}
      width func-grid-div(i)
```

_styles.css_
```
.col {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;
  position: relative;
  -webkit-box-pack: start;
  -ms-flex-pack: start;
  justify-content: flex-start;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
  -ms-flex-direction: row;
  flex-direction: row;
}
.col,
.col-0 {
  width: 0%;
}
.col,
.col-1 {
  width: 8.333333333333334%;
}
...
.col,
.col-10 {
  width: 83.33333333333334%;
}
.col,
.col-11 {
  width: 91.66666666666667%;
}
.col,
.col-12 {
  width: 100%;
}

```
