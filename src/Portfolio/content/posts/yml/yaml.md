---
title: "YAML - Fundamentos y sintaxis"
date: 2025-10-12T07:30:17+02:00
lastmod: 2025-10-12T07:30:17+02:00
author: Fco. Javier Cousiño
categories:
  - DevOps
tags:
  - YAML
  - YML
  - configuracion
  - DevOps
draft: false
---

## Indice

1. [¿Qué es YAML?](#QueEsYAML)
2. [Características básicas](#CaracteristicasBasicas)
3. [Tipos de datos](#TiposDatos)
4. [Estructuras de datos](#EstructurasDatos)
5. [Comentarios](#Comentarios)
6. [Casos de uso](#CasosDeUso)
7. [Buenas prácticas](#BuenasPracticas)
8. [Referencias](#Referencias)

### ¿Qué es YAML? <a id="QueEsYAML" href="#QueEsYAML" class="anchor"></a>

**YAML** (acrónimo recursivo de *YAML Ain't Markup Language*) es un formato de serialización de datos legible por humanos. Se utiliza ampliamente en ficheros de configuración, en pipelines de CI/CD y en herramientas de infraestructura como código.

Los archivos YAML tienen extensión `.yaml` o `.yml` y son ampliamente usados en herramientas como Docker, Kubernetes, GitHub Actions, Azure DevOps, Ansible, entre muchas otras.

### Características básicas <a id="CaracteristicasBasicas" href="#CaracteristicasBasicas" class="anchor"></a>

- La extensión puede ser `.yaml` o `.yml`.
- Los comentarios se añaden con el carácter `#`.
- Las claves y valores se separan con el carácter `:`.
- Los arrays se indican con los caracteres `[` y `]` o con guiones `-`.
- Las cadenas de texto se rodean con comillas dobles `"cadena"`, aunque en muchos casos son opcionales.
- La **indentación** es fundamental: se usan espacios (nunca tabulaciones) para indicar jerarquía.

### Tipos de datos <a id="TiposDatos" href="#TiposDatos" class="anchor"></a>

#### Cadenas de texto (Strings)

        # Sin comillas (válido cuando no hay caracteres especiales)
        nombre: Javier

        # Con comillas dobles
        nombre: "Javier Cousiño"

        # Con comillas simples
        mensaje: 'Hola, mundo!'

        # Cadena multilínea (conserva saltos de línea)
        descripcion: |
          Primera línea.
          Segunda línea.
          Tercera línea.

        # Cadena multilínea (pliega saltos de línea)
        descripcion: >
          Esta es una cadena
          que ocupa varias líneas
          pero se une en una sola.

#### Números

        # Entero
        edad: 30

        # Decimal
        precio: 19.99

        # Notación científica
        grande: 1.5e+6

        # Hexadecimal
        color: 0xFF0000

#### Booleanos

        # Verdadero
        activo: true
        habilitado: yes
        encendido: on

        # Falso
        activo: false
        habilitado: no
        encendido: off

#### Nulos

        valor: null
        otro: ~

### Estructuras de datos <a id="EstructurasDatos" href="#EstructurasDatos" class="anchor"></a>

#### Mapas (objetos/diccionarios)

Un mapa asocia claves con valores:

        persona:
          nombre: Javier
          apellido: Cousiño
          edad: 38
          email: "javier@ejemplo.com"

#### Arrays (listas)

##### Notación de bloque

        lenguajes:
          - C#
          - JavaScript
          - Python
          - Go

##### Notación de flujo (inline)

        lenguajes: [C#, JavaScript, Python, Go]

#### Arrays de objetos

        empleados:
          - nombre: Ana
            puesto: Desarrolladora
            antiguedad: 3
          - nombre: Carlos
            puesto: DevOps
            antiguedad: 5
          - nombre: Marta
            puesto: QA
            antiguedad: 2

#### Mapas anidados

        base_datos:
          servidor:
            host: localhost
            puerto: 5432
          credenciales:
            usuario: admin
            contrasena: "secreto"
          opciones:
            pool_conexiones: 10
            timeout: 30

#### Combinación de mapas y arrays

        microservicios:
          - nombre: api-gateway
            puerto: 8080
            replicas: 3
            variables_entorno:
              - JWT_SECRET: "mi-secreto"
              - LOG_LEVEL: info
          - nombre: user-service
            puerto: 8081
            replicas: 2

### Comentarios <a id="Comentarios" href="#Comentarios" class="anchor"></a>

Los comentarios en YAML comienzan con `#` y pueden aparecer en cualquier línea:

        # Este es un comentario de bloque
        nombre: Javier  # Este es un comentario en línea

        # Configuración de la base de datos
        base_datos:
          host: localhost  # Cambiar en producción
          puerto: 5432

### Casos de uso <a id="CasosDeUso" href="#CasosDeUso" class="anchor"></a>

#### Docker Compose

        version: '3.8'
        services:
          web:
            image: nginx:latest
            ports:
              - "80:80"
            volumes:
              - ./html:/usr/share/nginx/html
          db:
            image: postgres:15
            environment:
              POSTGRES_DB: mibd
              POSTGRES_USER: usuario
              POSTGRES_PASSWORD: contraseña

#### Kubernetes (Deployment)

        apiVersion: apps/v1
        kind: Deployment
        metadata:
          name: mi-aplicacion
        spec:
          replicas: 3
          selector:
            matchLabels:
              app: mi-aplicacion
          template:
            metadata:
              labels:
                app: mi-aplicacion
            spec:
              containers:
                - name: mi-aplicacion
                  image: mi-imagen:1.0
                  ports:
                    - containerPort: 8080

#### GitHub Actions

        name: CI
        on:
          push:
            branches: [main]
        jobs:
          build:
            runs-on: ubuntu-latest
            steps:
              - uses: actions/checkout@v4
              - name: Compilar
                run: dotnet build

### Buenas prácticas <a id="BuenasPracticas" href="#BuenasPracticas" class="anchor"></a>

- Usar siempre **espacios** para la indentación, nunca tabulaciones.
- Mantener una **indentación consistente** (2 o 4 espacios).
- Usar comillas para valores que contengan caracteres especiales (`:`  `,` `[` `]` `{` `}` `#` `&` `*` `?` `|` `-` `<` `>` `=` `!` `%` `@` `` ` ``).
- Añadir comentarios para explicar configuraciones no obvias.
- Validar los archivos YAML con herramientas como [YAML Lint](https://www.yamllint.com/) antes de usarlos en producción.
- Evitar anclas y alias si no son necesarios, ya que pueden dificultar la lectura.

### Referencias <a id="Referencias" href="#Referencias" class="anchor"></a>

- [Especificación oficial de YAML](https://yaml.org/spec/)
- [YAML Lint - Validador online](https://www.yamllint.com/)
- [Documentación de Docker Compose](https://docs.docker.com/compose/)
- [Documentación de Kubernetes](https://kubernetes.io/es/docs/concepts/overview/)
- [Sintaxis de GitHub Actions](https://docs.github.com/es/actions/writing-workflows/workflow-syntax-for-github-actions)
