---
title: "Winget export command"
date: 2025-10-12T07:30:17+02:00
lastmod: 2025-10-12T07:30:17+02:00
author: Fco. Javier Cousiño
categories:
  - WinGet
tags:
  - WinGet
  - Windows
draft: false
---

## Definición

Exporta a un fichero JSON un listado de las aplicaciones instaladas en la máquina. 

## Uso

            winget export [-o] <output> [<options>]

## Argumentos u opciones

-o, --output: ruta del fichero JSON a crear.

-s, --source: [opcional] especifica la fuente del fichero a exportar. 

--include-versions: [opcional] incluye la versión de la aplicación instalada.

--accept-source-agreements: usado para aceptar la licencia de acuerdos.

-?, --help: muestra la información del comando.

--wait: indicaciones para presionar una tecla antes de salir.

--logs, --open-logs: abre la localización por defecto de los logs.

--verbose, --verbose-logs: usado para sobreescribir los ajustes y crear detalles de logs.

--disable-interactivity: deshabilita las indicaciones interactivas.

## Esquema JSON 

|Entidad|Descripción|
|-----|-----------|
|Sources|Fuentes de la que proviene la aplicación|
|Packages|Colección de paquetes a instalar|
|PackageIdentifier|El identificador Windows Package Manager usado|
|Version|[Opcional]Version especifica del paquete de la instalación|

## Detalles instaladores

|Valor|Descripción|
|-----|-----------|
|Type|El tipo de instalador|
|Download Url| Url del instalador|
|Locale|Idioma del instalador|
|SHA256|Código SHA256 de la aplicación|

## Ejemplos 

            winget export Test.json

            winget export -o Test.json --include-versions

## Referencias

[Microsoft Learn](https://learn.microsoft.com/en-us/windows/package-manager/winget/export)