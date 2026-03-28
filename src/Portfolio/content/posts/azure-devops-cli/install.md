---
title: "Azure DevOps CLI - Instalación"
date: 2025-10-12T07:30:17+02:00
lastmod: 2025-10-12T07:30:17+02:00
author: Fco. Javier Cousiño
categories:
  - Azure DevOps
tags:
  - Azure
  - DevOps
  - CLI
  - instalacion
draft: false
---

## Indice

1. [Introducción](#Introduccion)
2. [Prerequisitos](#Prerequisitos)
3. [Instalación en Windows](#InstalacionWindows)
4. [Instalación en macOS](#InstalacionMacOS)
5. [Instalación en Linux](#InstalacionLinux)
6. [Configuración inicial](#ConfiguracionInicial)
7. [Comandos básicos](#ComandosBasicos)
8. [Referencias](#Referencias)

### Introducción <a id="Introduccion" href="#Introduccion" class="anchor"></a>

La **CLI de Azure DevOps** es una extensión de la CLI de Azure que permite interactuar con Azure DevOps directamente desde la línea de comandos. Con ella puedes gestionar proyectos, repositorios, pipelines, work items y mucho más sin necesidad de acceder a la interfaz web.

La extensión `azure-devops` se integra completamente con la CLI de Azure (`az`), por lo que una vez instalada puedes usar comandos del tipo:

        az devops project list
        az repos list
        az pipelines run

### Prerequisitos <a id="Prerequisitos" href="#Prerequisitos" class="anchor"></a>

Antes de instalar la CLI de Azure DevOps debes tener instalada la **CLI de Azure** (versión 2.0.69 o superior).

Puedes comprobar la versión instalada ejecutando:

        az --version

Si no la tienes instalada, visita la [documentación oficial de la CLI de Azure](https://learn.microsoft.com/es-es/cli/azure/install-azure-cli).

### Instalación en Windows <a id="InstalacionWindows" href="#InstalacionWindows" class="anchor"></a>

#### Mediante winget

        winget install Microsoft.AzureCLI

#### Mediante MSI

Descarga el instalador MSI desde la [página oficial de la CLI de Azure](https://learn.microsoft.com/es-es/cli/azure/install-azure-cli-windows).

#### Instalación de la extensión azure-devops

Una vez instalada la CLI de Azure, añade la extensión de Azure DevOps:

        az extension add --name azure-devops

Para actualizar la extensión a la última versión:

        az extension update --name azure-devops

### Instalación en macOS <a id="InstalacionMacOS" href="#InstalacionMacOS" class="anchor"></a>

#### Mediante Homebrew

        brew update && brew install azure-cli

#### Instalación de la extensión

        az extension add --name azure-devops

### Instalación en Linux <a id="InstalacionLinux" href="#InstalacionLinux" class="anchor"></a>

#### En distribuciones basadas en Debian/Ubuntu

        curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

#### En distribuciones basadas en RHEL/Fedora/CentOS

        sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
        sudo dnf install azure-cli

#### Instalación de la extensión

        az extension add --name azure-devops

### Configuración inicial <a id="ConfiguracionInicial" href="#ConfiguracionInicial" class="anchor"></a>

#### Iniciar sesión

Una vez instalada la CLI, inicia sesión en tu cuenta de Azure:

        az login

Si trabajas con una cuenta corporativa o necesitas especificar un tenant:

        az login --tenant <tenant-id>

#### Configurar la organización por defecto

Para evitar especificar la organización en cada comando, puedes configurarla como valor por defecto:

        az devops configure --defaults organization=https://dev.azure.com/<tu-organizacion>

#### Configurar el proyecto por defecto

De forma similar, puedes establecer el proyecto por defecto:

        az devops configure --defaults project=<nombre-del-proyecto>

#### Ver la configuración actual

        az devops configure --list

### Comandos básicos <a id="ComandosBasicos" href="#ComandosBasicos" class="anchor"></a>

#### Proyectos

        # Listar proyectos
        az devops project list

        # Mostrar detalles de un proyecto
        az devops project show --project <nombre-proyecto>

        # Crear un nuevo proyecto
        az devops project create --name <nombre-proyecto>

#### Repositorios

        # Listar repositorios
        az repos list

        # Crear un repositorio
        az repos create --name <nombre-repo>

        # Clonar un repositorio
        az repos clone --repository <nombre-repo>

#### Pipelines

        # Listar pipelines
        az pipelines list

        # Ejecutar un pipeline
        az pipelines run --name <nombre-pipeline>

        # Ver el estado de ejecuciones
        az pipelines runs list

#### Work Items

        # Listar work items
        az boards work-item list --project <nombre-proyecto>

        # Crear un work item
        az boards work-item create --title "Mi tarea" --type Task

        # Mostrar un work item
        az boards work-item show --id <id>

### Referencias <a id="Referencias" href="#Referencias" class="anchor"></a>

- [Documentación oficial de la extensión Azure DevOps para la CLI de Azure](https://learn.microsoft.com/es-es/azure/devops/cli/index?view=azure-devops)
- [Referencia de comandos az devops](https://learn.microsoft.com/es-es/cli/azure/devops)
- [Instalar la CLI de Azure](https://learn.microsoft.com/es-es/cli/azure/install-azure-cli)
