# Introducción a JavaScript

**JavaScript** es uno de los lenguajes de programación más usados y populares del mundo. **Nació en 1995** para darle interactividad a las páginas web y desde entonces ha evolucionado hasta convertirse en un **lenguaje de programacion de proposito general.**

## Tipos de Datos

En JavaScript **existen 9 tipos de datos** que se dividen en dos grupos: **primitivos y no primitivos**. Los primitivos, los tipos de datos más atomicos, más sencillos, más puros, **los no primitivos son los objetos y las funciones.**

*Existen 7 datos primitivos*:

1. `number`
2. `string`
3. `boolean`
4. `null`
5. `undefined`
6. `symbol`
7. `bigint`

Los primeros 3 son los más utilizados:

- `number`: datos más básicos que se pueden representar en JavaScript, **en JavaScript no hay diferencia entre números enteros y decimales**, todos son de tipo `number`:
  
```js
7
3.14
19.95
2.998e8 // exponencial
-1
Infinity // tipo de número especial
```
  
- `string`: son cadenas de texto. En JavaScript las cadenas de texto se representan entre comillas simples, dobles o acentos graves (backticks):
  
```js
'Cadena de texto'
"Otra cadena de texto"
`Otra cadena de texto más`

`Primera linea de la cadena de texto,
segunda linea de la cadena de texto` // multilinea por defecto
```
  
- `booleans`: representan solo dos valores: `true` o `false`. Ejemplo de como se puede responder con un valor booleano:
  
```js
true
false
```

## Operadores aritméticos

Con los números se pueden realizar operaciones aritméticas. En JavaScript existen los siguientes operadores aritméticos:

- **`+`**: suma
- **`-`**: resta
- `*`: multiplicación
- **`/`**: división
- **`%`**: módulo (resto de la división)
- **`*`**: exponente

```js
2 + 2 // 4
4 - 2 // 2
3 * 2 // 6
2 / 2 // 1
6 % 2 // 0
3 ** 3 // 27
```

Las operaciones **siguen un orden de precedencia**, pero s**e puede usar el paréntisis para cambiar el orden de las operaciones**:

```js
2 + 2 * 3 // 8
(2 + 2) * 3 // 12
```

Con los strings el operador aritmético `+` sirve para concatenar, es decir, **unir dos cadenas de texto**:

```js
'Esta cadena ' + 'se une con esta' // 'Esta cadena se une con esta'
```

## Operadores de comparación

**Permiten comparar dos valores** y siempre devuelven `true` o `false`.

```js
5 > 3 // true
5 < 3 // false
5 >= 3 // true
5 >= 5 // true
5 <= 3 // false
5 <= 5 // true
5 === 5 // true
5 !== 5 // false
```

También se pueden comparar strings y otros tipos de datos, se pueden comparar strings que utilizan comillas simples, dobles o backtick:

```js
'JavaScript' === 'JavaScript' // true
'JavaScript' === 'Java' // false
"JavaScript" !== 'PHP' // true
`Estoy Aprendiendo JavaScript` === 'Estoy Aprendiendo JavaScript' // true
```

**¿Y si se usa el operador > strings?**

No es muy común pero se puede usar los peradores `>`, `≥`, `<`, `≤` para comparar strings. JavaScript comprará los strings según el valor de su código *unicode.*

Por ejemplo si la letra A tiene un valor de 65 y la letra B tiene un valor de 66. Por lo tanto, la letra A es menor que la letra B. **Las letras mayúsculas tienen un valor menor que las letras minúsculas.**

```js
'Alfa' > 'Beta' // false
'Omega' > 'Beta' // true
'alfa' > 'Alfa' // true
```

También se puede comparar *booleanos* con los operadores de comparación.

```js
true === true // true
true === false // false
false !== false // false
```

El comportamiento de los operadores `>` y `<` en datos booleanos no tiene sentido, pero `true` es mayor que `false`.

```js
true > false // true
false < true // true
true > true // false
false < false // false
```

En JavaScript es posible comparar valores de diferentes tipos, sin embargo **no es recomendable**. 

## Operadores lógicos

Los operadores lógicos en JavaScript (y en muchos otros lenguajes) **se usan para evaluar expresiones lógicas**.

En JavaScript, hay tres operadores lógicos: *AND* (`&&`), *OR* (`||`) y *NOT* (`!`).

**Operador logico *AND* `&&`:**

Devuelve `true` cuando ambos valores que conecta son `true`:

```js
true && true // → true
true && false // → false
false && false // → false
```

**Operador logico *OR* `||`:**

Devuelve `true` cuando cualquiera de valores que conecta es `true`:

```js
true || true // → true
true || false // → true
false || false // → false
```

**Operador lógico *NOT* `!`:**

Invierte el valor de un booleano. Se pone delante del valor que queremos invertir:

```js
!true // → false
!false // → true
```

Los operadores lógicos y los operadores de comparación **se pueden combinar** para crear operaciones más complejas:

```js
2 < 3 && 3 < 4 // → true
```

Se puede usar paréntesis para agrupar operaciones y usar operadores lógicos y aritmeticos:

```js
(2 + 2) < 3 && (10 < (8 * 2)) // → false
```

Las operaciones aritméticas tienen precedencia sobre las operaciones de comparación:

```js
(2 + 2) < 3 && (10 < (8 * 2))
// Primero se hacen las operaciones aritméticas:
// → 4 < 3 && 10 < 16
// Ahora las comparaciones:
// → false && true
// Finalmente:
// → false
```

Los operadores lógicos pueden usarse con más de dos operandos, también se puede mezclar operadores lógicos:

```js
true && true && true // → true
true && true || false // → true
!true && !true // → false
false && true || !true // → false
```

## Variables

Para crear variables en JavaScript se usa la palabra reservada `let` y luego se le da el nombre a la variable:

```js
let numero
```

Para asignar un valor a una variable se usa el operador de asignación `=`:

```js
let numero = 1
let welcomeText = 'Hola'
let isCool = true
```

Una variable se puede reasignar:

```js
numero = 2
welcomeText = 'Bienvenido'
isCool = false
```

Las constantes son variables que no pueden ser reasignadas. Para crearlas se usa la palabra reservada `const`:

```js
const PI = 3.1415
```

Si se intenta reasignar el valor de una constante da un error:

```js
PI = 3 // -> TypeError: Assignment to constant variable.
```

Como no se pueden reasignar, **las constantes siempre deben ser inicializadas con algún valor**. Esto es otra diferencia respecto a `let`, que no es necesario inicializarla con un valor.

```js
let numero // ✅
const RADIUS // ❌ SyntaxError: Missing initializer in const declaration
```

Es más reconmendable usar constantes para que el código sea más predicible.

**Variables** `var`**:**

Se puede crear variables usando la palabra reservada `var`. Es la forma más antigua. Sin embargo, a día de hoy, **no es recomendable usar** `var` ya que tiene comportamientos extraños que pueden causar errores.

**El nombre de las variables**

Los nombres de las variables pueden contener letras, números y el guion bajo (_). El primer carácter no puede ser número.

**Los nombres de las variables son sensibles a las mayúsculas y minusculas**, es decir, `miVariable` y `mivariable` son variables diferentes:

```js
let miVariable = 1
let mivariable = 2
miVariable + mivariable // -> 1 + 2
```

Los nombres de las variables deben ser descriptivos, es decir, si se tiene una variable para almacenar el nombre de usuario, lo ideal seria llamar a la variable `userName`.

**Convenciones y nomenclaturas**

En JavaScript, existen diferentes nomenclaturas para nombrar las variables: **camelCase**, **snake_case** y **SCREAMING_CASE**.

**camelCase** es la forma más común de nombrar las variables en JavaScript. Consiste en escribir la primera palabra en minúsculas y las siguientes palabras con su primera letra en mayúsculas. Por ejemplo:

```js
let camelCase = 1
let camelCaseIsCool = 2
let userName = 'lucascodev'
```

**snake_case** es una forma de nombrar que consiste en escribir todas las palabras en minúsculas y separarlas con guiones bajos. Por ejemplo:

```js
let snake_case = 1
let snake_case_is_cool = 2
let user_name = 'lucascodev'
```

En JavaScript no es tan comun como en otros lenguajes usar el snake_case, pero todavía se puede encontrar código que lo use.

Existe **kebab-case**, que es una forma de nombrar que consiste en escribir todas las palabras en minúsculas y separarlas con guiones. Por ejemplo: `mi-archivo.js`. Es muy similar a **snake_case** pero con guiones en vez de guiones bajos. No se puede usar para nombrar variables pero sí es común usarlo en los nombres de archivos.

**SCREAMING_CASE** es una forma de nombrar que consiste en escribir todas las palabras en mayúsculas y separarlas con guiones bajos. Por ejemplo:

```js
const SCREAMING_CASE = 1
const SCREAMING_CASE_IS_COOL = 2
const USER_NAME = 'lucascodev'
```

Para las constantes, con valores que no van a cambiar, es muy común usar **SCREAMING_CASE**. Así se puede distinguir fácilmente de las variables que sí cambian de valor. Por eso, no debes usarla para nombrar variables con `let`.

## `null` y `undefined`

Aunque son similares, tienen ligeras diferencias. La particularidad de estos dos tipos de datos es que cada uno sólo tiene un valor. El tipo `null` sólo puede tener el valor `null` y el tipo `undefined` sólo puede tener el valor `undefined`.

La diferencia radica en que `null` significa que algo no tiene valor alguno, `undefinded` significa que algo no está definido. Por ejemplo si se crea una variable sin asignarle un valor, su valor será `undefined`:

```js
let papelHigienico // -> undefined
```

También se puede asignar directamente el valor `undefined` a una variable:

```js
let papelHigienico = undefined // -> undefined
```

Para que una variable tenga el valor `null`, sólo se puede conseguirlo asignándole explícitamente ese valor:

```js
let papelHigienico = null
```

Una imagen que puede ayudar a entender la diferencia entre `null` y `undefined` es la siguiente:

![https://www.aprendejavascript.dev/images/null-undefined.jpg](https://www.aprendejavascript.dev/images/null-undefined.jpg)

Al usar la igualdad estricta, `null` y `undefined` son considerados diferentes entre sí:

```js
null === undefined *// -> false*
```

Sólo cuando se compara `null` con `null` o `undefined` con `undefined` se obtiene `true`:

```js
null === null *// -> true*
undefined === undefined *// -> true*
```

## Operador `typeof`

El operador `typeof` devuelve un string que indica el tipo de dato de un operando. Se puede usar con cualqueir tipo de operando, incluyendo variables y literales.

```js
const MAGIC_NUMBER = 7
typeof MAGIC_NUMBER // "number"
```

También se puede usar directamente con los valores que se quiera comprobar:

```js
typeof undefined // "undefined"
typeof true // "boolean"
typeof 42 // "number"
typeof "Hola mundo" // "string"
```

Existe, sin embargo, un valor especial en JavaScript, `null`, que es considerado un bug en el lenguaje. El operador `typeof` devuelve `"object"` cuando se usa con `null`:

```js
typeof null // "object"
```

Lo correcto seria que `typeof null` devolviera `“null”`, pero es un **error historico que no se puede corregir sin romper el código existente.** [Lee un poco más aquí](https://2ality.com/2013/10/typeof-null.html)

Por eso, para comprobar si una variable es `null`, se debe usar la comparación estricta **`===`**:

```js
const foo = null
foo === null // true
```

El operador `typeof` es muy útil cuando se usa con operadores de comparación. Por ejemplo, para comprobar si una variable es del tipo que se espera:

```js
const age = 42
typeof age === "number" // true
```

## Comentarios

Los comentarios son una forma de agregar explicaciones al código que **se ignora al ejecutar el programa.**

Los comentarios son útiles para explicar el por qué del código, documentar los cambios realizados en el código y hacer que el código sea más fácil de entender para otros desarrolladores.

Hay **dos tipos de comentarios en JavaScript**: los comentarios de una sola línea y los comentarios de varias líneas.

Los comentarios de una sola línea comienzan con **`//`** y se utilizan para agregar una explicación en una sola línea de código. Por ejemplo:

```js
// Sólo 6 decimales
const PI = 3.141592

// Se incia el radio por 10, pero puede cambiar
let radio = 10
```

También se puede añadir un comentario de una sola línea al final de una línea de código. Por ejemplo:

```js
const PI = 3.141592 // Sólo 6 decimales
```

Los comentarios de varias líneas comienzan con `/*` y terminan con `*/`. Se utilizan para agregar notas explicativas que ocupan varias líneas de código. Por ejemplo:

```js
/*
  Este es un comentario de varias líneas.
  Se utiliza para agregar notas explicativas
  que ocupan varias líneas de código.
*/
```

Es mejor que el código sea lo suficientemente claro como para no necesitar comentarios, pero si es necesario, **se debe** **utilizar comentarios para explicar el por qué del código, no el qué.**

## `console.log()`

Es una **función** integrada en JavaScript que se utiliza para imprimir mensajes en la consola del navegador o del editor de código. Se utiliza principalmente para depurar el código y para **imprimir valores de variables y mensajes para ayudar en el proceso de desarrollo.**

Para poder mostrar estos mensajes en consola, se debe escribir `console.log()` y dentro de los paréntesis, el mensaje que se quiere mostrar.

```js
console.log('Hola, JavaScript')
// -> 'Hola, JavaScript'
```

También puedes averiguar el valor de una variable, escribiendo el nombre de la variable dentro de los paréntesis.

```js
const nombre = 'lucascodev'
console.log(nombre)
// -> 'lucascodev'
```

Se puede concatenar strings, se puede mostrar un mensaje y el valor de una variable en el mismo `console.log()`.

```js
const nombre = 'lucascodev'
console.log('Hola, ' + nombre)
// -> 'Hola, lucascodev'
```

Además, se puede mostrar varios mensajes y valores de variables en el mismo `console.log()` separándolos por comas.

```js
const nombre = 'lucascodev'
const edad = 24
console.log(nombre, edad)
// -> 'lucascodev 24'
```

Además de `console.log()`, existen otros métodos que se utilizan para imprimir mensajes en la consola. Algunos de ellos son:

- `console.error()`: Imprime un mensaje de error en la consola.
- `console.warn()`: Imprime un mensaje de advertencia en la consola.
- `console.info()`: Imprime un mensaje de información en la consola.

La sintaxis es la misma que `console.log()`, sólo cambia el nombre del método.

```js
console.error('Error')
// ❌ Error
console.warn('Advertencia')
// ⚠️ Advertencia
console.info('Información')
// ℹ️ Información
```