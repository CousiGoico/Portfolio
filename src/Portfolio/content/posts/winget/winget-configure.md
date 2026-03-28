---
title: "Configure command"
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

Configura un fichero WinGet para configurar la máquina en un entorno de desarrollo.

> **_NOTE:_** PREVIEW

## Alias

+ configuration

## Uso

            winget configure -f <C:/Users/<username>/winget-configs/config-file-name.dsc.yaml>

## Argumentos u opciones

-f, --file: ruta del fichero de configuración

-?, --help: obtiene información adicional del comando.

--wait: espera a que el usuario pulse una tecla.

--verbose, --verbose-logs: habilita el logado detallado.

--disable-interactivity: desabilita las indicaciones interactivas.

## Ejemplos 

            winget configure show //muestra el detalle del fichero de configuración

            winget configure test // chequea el sistema

            winget configure validate // valida el fichero de configuración

## Referencias

[Microsoft Learn](https://learn.microsoft.com/en-us/windows/package-manager/winget/install)