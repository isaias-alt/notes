# HTML

Son las siglas de **HyperText Markup Language** (Lenguaje de marcado de hipertexto).

Se enfoca como se marca o define el contendido, es decir, como se describe, no se dedica a como se ve el contendo (CSS) ni como se interactua con él (JS).

#### No se ocupa de:
 - La presentación (CSS).
 - La interactividad (JavaScript).
#### Se encarga de:
- Describir el contenido.

Para escribir HTML se debe crear un archivo con la extensión `.html` un ejemplo sería: `index.html`. Se le puede llamar de cualquier manera, pero de forma clásica los navegadores buscaban el archivo `index.html` como punto de entrada.

## Qué son las etiquetas?
Las etiquetas HTML son los componentes básicos que se usan para estructurar y definir el contenido en una página web. El contenido se define a través de elementos.

Un elemento se crea así:
```html
<h1>Hola Mundo!</h1>
```
#### Estas son las partes de un elemento:
- `<h1>`: etiqueta de apertura
- 'Hola Mundo': contenido
- `</h1>`: etiqueta de cierre

No todas las etiquetas permiten contenido y no todas las etiquetas se cierran.

HTML no es case sensitive, pero la recomendación es que que todas las etiquetas se escriban en minúscula.

En HTML se puede anidar los elementos:
```html
<h1>Hola Mundo!</h1>
<p>Esto es un <strong>parrafo</strong>.</p>
```
En este caso parrafo se mostraría en negrita. Se deja el punto fuera para que no se le apique la negrita, quedaría algo como esto: 'Esto es un **parrafo**.'

Los comentarios en HTML se escriben así:
```html
<!-- Esto es un comentario -->
<h1>Hola Mundo!</h1>
<p>Esto es un <strong>parrafo</strong>.</p>
```

El navegador interpreta las etiquetas y aplica ciertos estilos. Más adelante se verá cómo.
#### En HTML existen 3 tipos de elementos:
- Normales.
- Reemplazables (comunmente no tienen etiqueta de cierre).
- Vacios (Saltos de linea, etc.).

A los elementos reemplazables solo hay que indicarles el contenido a reemplazar:
```html
<img src="/images/perrito.png" />
```
 
## Atributos en HTML
La etiquetas en HTML tienen atributos, los atributos proporcionan informacion adicional a los elementos HTML.

#### Existen dos tipos de atributos:
- Globales: se puede usar en todas de etiquetas. 
- Especificos: se pueden usar solo en algunas.

#### Existen dos atributos claves en HTML:
- id: el valor debe ser unico.
- class: puede repetirse el valor.
Ambos atributos son globales sirve para identificar elementos

## Estilos por defecto
Los navegadores tienen unos estilos por defectos llamados user *agent stylesheets* (Hojas de estilo de agente de usuario)

Por ejemplo estos son unos estilos por defecto de la etiqueta `<h1>`:
```css
h1 {
	font-size: 2em;
    font-weight: bold;
    margin-top: 0.67em;
    margin-bottom: 0.67em;
    color: black;
}
```

## HTML semántico
Esto significa usar etiquetas que describan el proposito y el contenido de cada elemento de la página web. 

Es decir que en vez de usar etiquetas genéricas como `<div>`, usar etiquetas especifias como `<header>`, `<article>`, `<section>`, y `<footer>`.

Estas etiquetas le dicen a los navegadores, a los motores de busqueda y a otros desarrolladores que tipo de contenido contiene cada parte de la página.

## Elementos en linea y en bloque
En HTML, los elementos se dividen en dos tipos principales: **elementos en bloque** y **elementos en línea**.

#### Los elementos en bloque:
- Ocupan todo el ancho disponible.
- Siempre comienzan en una nueva linea.
- Ideales para estructurar contenido grande o secciones completas.
- Ejemplos: `<div>`, `<h1>`, `<p>`, `<section>`.

#### Los elementos en linea:
- Ocupan solo el espacio necesario para el contenido que tienen dentro.
- No empiezan en una nueva linea. Pueden colocarse uno al lado del otro.
- Se usan para marcar pequeñas partes del texo o elementos dentro de otras etiquetas sin interrumpir el flujo del contenido.
- Ejemplos: `<span>`, `<a>`, `<img>`, `<strong>`.

## Estructura de Documento
- `<!DOCTYPE>`: Define el tipo de documento y la versión de HTML.
- `<html>`: Elemento raíz de un documento HTML.
- `<head>`: Contiene metadatos sobre el documento (como el título, enlaces a estilos, etc.) esto no se renderiza en el navegador.
- `<title>`: Especifica el título de la página que aparece en la pestaña del navegador.
- `<body>`: Contiene el contenido visible de la página web.

## Secciones de Documento
- `<header>`: Contiene encabezados introductorios o grupos de navegación.
- `<nav>`: Define un conjunto de enlaces de navegación.
- `<section>`: Define una sección temática del contenido.
- `<article>`: Representa una sección de contenido independiente o reutilizable.
- `<aside>`: Contenido relacionado lateralmente con el contenido principal  .
- `<footer>`: Pie de página de la sección o del documento.
- `<main>`: Contenido principal del documento (único por página).

## Texto y Formato
- `<h1>` a `<h6>`: Encabezados, de mayor a menor importancia.
- `<p>`: Párrafo de texto.
- `<br>`: Salto de línea.
- `<hr>`: Separador horizontal (línea).
- `<strong>`: Texto con énfasis fuerte (semántico).
- `<i>`: Texto en cursiva (visual).
- `<em>`: Texto con énfasis (semántico).
- `<small>`: Texto de menor tamaño.
- `<mark>`: Texto resaltado.
- `<del>`: Texto tachado (indica eliminación).
- `<ins>`: Texto subrayado (indica inserción).
- `<sub>`: Subíndice.
- `<sup>`: Superíndice.
- `<blockquote>`: Cita en bloque.
- `<q>`: Cita en línea.
- `<dialog>`: Define un cuadro de diálogo o ventana modal que puede mostrarse y ocultarse mediante JavaScript.

## Listas
- `<ul>`: Lista desordenada.
- `<ol>`: Lista ordenada.
- `<li>`: Elemento de lista.
- `<dl>`: Lista de definiciones.
- `<dt>`: Término en una lista de definiciones.
- `<dd>`: Definición en una lista de definiciones.

## Enlaces y Multimedia
- `<a>`: Enlace a otra página, recurso o sección.
- `<img>`: Imagen.
- `<audio>`: Contenido de audio.
- `<video>`: Contenido de video.
- `<source>`: Fuente alternativa para medios (audio/video).
- `<track>`: Subtítulos o pistas de audio.
- `<iframe>`: Marco embebido (incrusta otro documento).

## Tablas
- `<table>`: Tabla de datos.
- `<thead>`: Cabecera de tabla.
- `<tbody>`: Cuerpo de la tabla.
- `<tfoot>`: Pie de tabla.
- `<tr>`: Fila de tabla.
- `<th>`: Celda de encabezado.
- `<td>`: Celda de datos.

## Formularios
- `<form>`: Formulario para enviar datos.
- `<input>`: Campo de entrada de datos.
- `<textarea>`: Área de texto para entrada larga.
- `<button>`: Botón interactivo.
- `<select>`: Menú desplegable.
- `<option>`: Opción dentro de `<select>`.
- `<label>`: Etiqueta para un control de formulario.
- `<fieldset>`: Agrupa controles de formulario.
- `<legend>`: Título para `<fieldset>`.
- `<datalist>`: Lista de opciones predefinidas para entradas.
- `<output>`: Resultado de una operación de formulario.
- `<progress>`: Barra de progreso.
- `<meter>`: Representa una medida escalar dentro de un rango.

## Contenedores y Layout
- `<div>`: Contenedor genérico para agrupar contenido.
- `<span>`: Contenedor genérico en línea para texto o elementos.
- `<figure>`: Contiene contenido ilustrativo (imágenes, diagramas, etc.).
- `<figcaption>`: Pie de foto o leyenda para un `<figure>`.

## Scripting
- `<script>`: Inserta o enlaza código JavaScript.
- `<noscript>`: Contenido mostrado si el navegador no soporta JavaScript.

## Meta Datos
- `<meta>`: Proporciona metadatos sobre el documento (como el conjunto de caracteres, autor, etc.).
- `<link>`: Vincula recursos externos (como hojas de estilo).
- `<style>`: Define estilos CSS en línea.

## Elementos Obsoletos (Deprecated)
- `<center>`: Centra el contenido. **(Obsoleto)**
- `<font>`: Define estilos de fuente. **(Obsoleto)**
- `<big>`: Texto más grande que el normal. **(Obsoleto)**
- `<basefont>`: Define la fuente predeterminada del documento. **(Obsoleto)**
- `<acronym>`: Define acrónimos. **(Obsoleto, usar `<abbr>` en su lugar)**
- `<applet>`: Embebe una applet de Java. **(Obsoleto)**
- `<bgsound>`: Inserta sonidos de fondo. **(Obsoleto)**
- `<frame>`: Define un marco en un conjunto de marcos. **(Obsoleto)**
- `<frameset>`: Contiene uno o más `<frame>`. **(Obsoleto)**
- `<noframes>`: Contenido alternativo para navegadores sin soporte para `<frameset>`. **(Obsoleto)**
- `<isindex>`: Campo de búsqueda. **(Obsoleto)**
- `<b>`: Texto en negrita. **(Obsoleto)**
