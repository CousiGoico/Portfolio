---
title: "Guía de Markdown"
date: 2025-10-12T07:30:17+02:00
lastmod: 2025-10-12T07:30:17+02:00
author: Fco. Javier Cousiño
categories:
  - Markdown
tags:
  - Markdown
  - documentacion
  - escritura
draft: false
---

## Indice

1. [Encabezados](#Encabezados)
2. [Líneas divisorias](#LineasDivisorias)
3. [Énfasis de texto](#EnfasisTexto)
4. [Citas](#Citas)
5. [Listas](#Listas)
6. [Código](#Codigo)
7. [Tablas](#Tablas)
8. [Enlaces](#Enlaces)
9. [Imágenes](#Imagenes)
10. [Emojis](#Emojis)
11. [Superíndice y subíndice](#SuperIndiceSubIndice)
12. [Tabla de contenidos con anclas](#TablaContenidosAnclas)
13. [Alertas de GitHub](#AlertasGitHub)
14. [Referencias](#Referencias)

### Encabezados <a id="Encabezados" href="#Encabezados" class="anchor"></a>

Los encabezados se crean con el símbolo `#` seguido de un espacio y el texto del título. El número de `#` determina el nivel del encabezado (del 1 al 6):

        # H1 - Encabezado nivel 1
        ## H2 - Encabezado nivel 2
        ### H3 - Encabezado nivel 3
        #### H4 - Encabezado nivel 4
        ##### H5 - Encabezado nivel 5
        ###### H6 - Encabezado nivel 6

### Líneas divisorias <a id="LineasDivisorias" href="#LineasDivisorias" class="anchor"></a>

Existen tres formas de crear líneas divisorias:

        ___   (línea continua)
        ---   (línea discontinua)
        ***   (línea de puntos)

### Énfasis de texto <a id="EnfasisTexto" href="#EnfasisTexto" class="anchor"></a>

#### Negrita

        **Este texto está en negrita**
        __Este texto está en negrita__

#### Cursiva

        *Este texto está en cursiva*
        _Este texto está en cursiva_

#### Tachado

        ~~Este texto está tachado~~

#### Combinado

        **_Este texto está en negrita y cursiva_**
        ~~**Este texto está tachado y en negrita**~~

### Citas <a id="Citas" href="#Citas" class="anchor"></a>

Las citas se crean con el símbolo `>`. Pueden anidarse:

        > Texto con un nivel de cita
        >> Texto con dos niveles de cita
        > > > Texto con tres niveles de cita

Se pueden incluir otros elementos Markdown dentro de una cita:

        > **Nota importante:**
        > Esta es una cita con negrita.
        >
        > Y este es un segundo párrafo dentro de la cita.

### Listas <a id="Listas" href="#Listas" class="anchor"></a>

#### Listas no ordenadas

Se pueden crear con `+`, `-` o `*`:

        - Primer elemento
        - Segundo elemento
          - Sub-elemento (indentado con 2 espacios)
          - Otro sub-elemento
            - Sub-sub-elemento
        + También con el símbolo más
        * O con el asterisco

#### Listas ordenadas

        1. Primer elemento
        2. Segundo elemento
        3. Tercer elemento

> También puedes usar el mismo número repetido y Markdown lo numerará automáticamente.

#### Listas de tareas (GitHub Flavored Markdown)

        - [x] Tarea completada
        - [ ] Tarea pendiente
        - [ ] Otra tarea pendiente

### Código <a id="Codigo" href="#Codigo" class="anchor"></a>

#### Código en línea

Rodea el texto con comillas invertidas `` ` ``:

        Usa el comando `npm install` para instalar las dependencias.

#### Bloque de código

Rodea el código con tres comillas invertidas (` ``` `):

        ```
        Este es un bloque de código genérico
        ```

#### Bloque de código con resaltado de sintaxis

Indica el lenguaje después de las tres comillas iniciales:

        ```javascript
        var foo = function(bar) {
            return bar++;
        };
        console.log(foo(5));
        ```

        ```csharp
        public class Saludo {
            public string Mensaje { get; set; } = "Hola, mundo!";
        }
        ```

        ```bash
        #!/bin/bash
        echo "Hola, mundo!"
        ```

### Tablas <a id="Tablas" href="#Tablas" class="anchor"></a>

Las tablas se crean con barras verticales `|` y guiones `-`:

        | Columna 1 | Columna 2 | Columna 3 |
        |-----------|-----------|-----------|
        | Dato 1    | Dato 2    | Dato 3    |
        | Dato 4    | Dato 5    | Dato 6    |

#### Alineación de columnas

        | Izquierda | Centro  | Derecha |
        |:----------|:-------:|--------:|
        | Texto     | Texto   | Texto   |
        | Más texto | Más     | 1234    |

### Enlaces <a id="Enlaces" href="#Enlaces" class="anchor"></a>

#### Enlace básico

        [Texto del enlace](https://www.ejemplo.com)

#### Enlace con título (tooltip)

        [Texto del enlace](https://www.ejemplo.com "Título del enlace")

#### Enlace de referencia

        [Texto del enlace][referencia]

        [referencia]: https://www.ejemplo.com

#### Enlace automático

        <https://www.ejemplo.com>
        <usuario@ejemplo.com>

### Imágenes <a id="Imagenes" href="#Imagenes" class="anchor"></a>

La sintaxis es similar a los enlaces, pero con `!` delante:

        ![Texto alternativo](url-de-la-imagen.png)
        ![Texto alternativo](url-de-la-imagen.png "Título de la imagen")

#### Imagen con enlace

        [![Texto alternativo](url-imagen.png)](url-destino)

### Emojis <a id="Emojis" href="#Emojis" class="anchor"></a>

En GitHub y otras plataformas compatibles puedes usar emojis:

#### Mediante código de emoji

        :smile: :thumbsup: :rocket: :fire: :tada:

#### Mediante caracteres Unicode

        🚀 ✅ ⚠️ 💡 🔧

### Superíndice y subíndice <a id="SuperIndiceSubIndice" href="#SuperIndiceSubIndice" class="anchor"></a>

Algunos renderizadores de Markdown soportan:

        19^th^        → 19ᵗʰ (superíndice)
        H~2~O         → H₂O (subíndice)

### Tabla de contenidos con anclas <a id="TablaContenidosAnclas" href="#TablaContenidosAnclas" class="anchor"></a>

Para crear una tabla de contenidos con anclas en Markdown:

        ## Indice

        1. [Introducción](#introduccion)
        2. [Características](#caracteristicas)
        3. [Conclusión](#conclusion)

        ### Introducción <a id="introduccion" href="#introduccion" class="anchor"></a>

        Contenido de la introducción...

        ### Características <a id="caracteristicas" href="#caracteristicas" class="anchor"></a>

        Contenido de las características...

### Alertas de GitHub <a id="AlertasGitHub" href="#AlertasGitHub" class="anchor"></a>

GitHub Flavored Markdown soporta bloques de alerta especiales:

        > [!NOTE]
        > Información útil que el usuario debe conocer.

        > [!TIP]
        > Consejo para hacer las cosas mejor o más fácilmente.

        > [!IMPORTANT]
        > Información clave necesaria para que los usuarios tengan éxito.

        > [!WARNING]
        > Información urgente que necesita atención inmediata.

        > [!CAUTION]
        > Posibles consecuencias negativas de una acción.

### Referencias <a id="Referencias" href="#Referencias" class="anchor"></a>

- [Guía de Markdown de GitHub](https://docs.github.com/es/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [CommonMark Spec](https://spec.commonmark.org/)
- [markdown-it demo](https://markdown-it.github.io/)
- [Markdown Guide](https://www.markdownguide.org/)
