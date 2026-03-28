---
title: "GitHub Deploy con GitHub Actions"
date: 2025-10-12T07:30:17+02:00
lastmod: 2025-10-12T07:30:17+02:00
author: Fco. Javier Cousiño
categories:
  - GitHub
tags:
  - GitHub
  - Actions
  - CI/CD
  - deploy
  - DevOps
draft: false
---

## Indice

1. [Introducción](#Introduccion)
2. [Estructura de un workflow](#EstructuraWorkflow)
3. [Eventos de disparo](#EventosDisparo)
4. [Jobs y Steps](#JobsSteps)
5. [Variables de entorno y Secrets](#VariablesSecretos)
6. [Ejemplo: Despliegue en GitHub Pages](#EjemploGitHubPages)
7. [Ejemplo: Despliegue en Azure](#EjemploAzure)
8. [Referencias](#Referencias)

### Introducción <a id="Introduccion" href="#Introduccion" class="anchor"></a>

**GitHub Actions** es una plataforma de integración y entrega continua (CI/CD) integrada directamente en GitHub. Permite automatizar el ciclo de vida del software: compilar, probar y desplegar aplicaciones directamente desde el repositorio.

Los flujos de trabajo (*workflows*) se definen mediante archivos YAML ubicados en el directorio `.github/workflows/` del repositorio. Estos archivos se activan ante determinados eventos del repositorio como un `push`, la apertura de un *pull request*, una publicación, o mediante un disparador manual.

> GitHub Actions está completamente integrado en VS Code a través de la extensión oficial de GitHub Actions.

#### Ventajas

- Integración nativa con GitHub.
- Soporte para múltiples sistemas operativos (Linux, Windows, macOS).
- Gran ecosistema de *actions* reutilizables en el Marketplace.
- Gratuito para repositorios públicos y con minutos gratuitos para los privados.

### Estructura de un workflow <a id="EstructuraWorkflow" href="#EstructuraWorkflow" class="anchor"></a>

Un archivo de workflow tiene la siguiente estructura básica:

        name: Mi Workflow

        on:
          push:
            branches:
              - main

        jobs:
          build:
            runs-on: ubuntu-latest
            steps:
              - name: Checkout del código
                uses: actions/checkout@v4

              - name: Instalar dependencias
                run: npm install

              - name: Ejecutar tests
                run: npm test

              - name: Compilar
                run: npm run build

Las propiedades principales son:

- **`name`**: nombre descriptivo del workflow.
- **`on`**: define los eventos que disparan el workflow.
- **`jobs`**: lista de trabajos a ejecutar.
  - **`runs-on`**: tipo de runner (máquina) en la que se ejecuta el job.
  - **`steps`**: secuencia de pasos dentro del job.
    - **`name`**: nombre del paso.
    - **`uses`**: acción reutilizable del Marketplace.
    - **`run`**: comando de shell a ejecutar.

### Eventos de disparo <a id="EventosDisparo" href="#EventosDisparo" class="anchor"></a>

Los workflows pueden dispararse mediante multitud de eventos:

#### Eventos de repositorio

        on:
          push:                          # Al hacer push
            branches: [main, develop]
          pull_request:                  # Al abrir/actualizar un PR
            branches: [main]
          release:                       # Al publicar una release
            types: [published]

#### Disparo manual

        on:
          workflow_dispatch:             # Permite ejecutarlo manualmente
            inputs:
              environment:
                description: 'Entorno de despliegue'
                required: true
                default: 'staging'

#### Disparo programado (cron)

        on:
          schedule:
            - cron: '0 8 * * 1-5'       # De lunes a viernes a las 8:00 UTC

### Jobs y Steps <a id="JobsSteps" href="#JobsSteps" class="anchor"></a>

#### Jobs en paralelo

Por defecto, todos los jobs de un workflow se ejecutan en paralelo:

        jobs:
          test:
            runs-on: ubuntu-latest
            steps:
              - uses: actions/checkout@v4
              - run: npm test

          lint:
            runs-on: ubuntu-latest
            steps:
              - uses: actions/checkout@v4
              - run: npm run lint

#### Jobs secuenciales (dependencias)

Para ejecutar jobs en orden, usa `needs`:

        jobs:
          test:
            runs-on: ubuntu-latest
            steps:
              - run: npm test

          deploy:
            needs: test              # Solo se ejecuta si 'test' tiene éxito
            runs-on: ubuntu-latest
            steps:
              - run: npm run deploy

#### Matriz de Jobs

Puedes ejecutar un mismo job con diferentes configuraciones usando una matriz:

        jobs:
          test:
            strategy:
              matrix:
                node-version: [18, 20, 22]
                os: [ubuntu-latest, windows-latest]
            runs-on: ${{ matrix.os }}
            steps:
              - uses: actions/setup-node@v4
                with:
                  node-version: ${{ matrix.node-version }}
              - run: npm test

### Variables de entorno y Secrets <a id="VariablesSecretos" href="#VariablesSecretos" class="anchor"></a>

#### Variables de entorno

        env:
          NODE_ENV: production
          API_URL: https://api.example.com

        jobs:
          build:
            runs-on: ubuntu-latest
            env:
              VARIABLE_LOCAL: valor
            steps:
              - name: Usar variable
                run: echo $NODE_ENV

#### Secrets

Los *secrets* se configuran en **Settings > Secrets and variables > Actions** del repositorio y se referencian así:

        steps:
          - name: Desplegar
            env:
              TOKEN: ${{ secrets.MI_TOKEN }}
              DB_PASSWORD: ${{ secrets.DB_PASSWORD }}
            run: ./deploy.sh

### Ejemplo: Despliegue en GitHub Pages <a id="EjemploGitHubPages" href="#EjemploGitHubPages" class="anchor"></a>

        name: Desplegar en GitHub Pages

        on:
          push:
            branches: [main]

        permissions:
          contents: read
          pages: write
          id-token: write

        jobs:
          build:
            runs-on: ubuntu-latest
            steps:
              - uses: actions/checkout@v4

              - name: Instalar Hugo
                uses: peaceiris/actions-hugo@v3
                with:
                  hugo-version: 'latest'

              - name: Compilar sitio
                run: hugo --minify

              - name: Subir artefacto
                uses: actions/upload-pages-artifact@v3
                with:
                  path: './public'

          deploy:
            needs: build
            runs-on: ubuntu-latest
            environment:
              name: github-pages
              url: ${{ steps.deployment.outputs.page_url }}
            steps:
              - name: Desplegar en GitHub Pages
                id: deployment
                uses: actions/deploy-pages@v4

### Ejemplo: Despliegue en Azure <a id="EjemploAzure" href="#EjemploAzure" class="anchor"></a>

        name: Desplegar en Azure App Service

        on:
          push:
            branches: [main]

        jobs:
          build-and-deploy:
            runs-on: ubuntu-latest
            steps:
              - uses: actions/checkout@v4

              - name: Configurar .NET
                uses: actions/setup-dotnet@v4
                with:
                  dotnet-version: '8.0.x'

              - name: Compilar proyecto
                run: dotnet publish -c Release -o ./publish

              - name: Desplegar en Azure Web App
                uses: azure/webapps-deploy@v3
                with:
                  app-name: 'mi-aplicacion'
                  publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
                  package: ./publish

### Referencias <a id="Referencias" href="#Referencias" class="anchor"></a>

- [Documentación oficial de GitHub Actions](https://docs.github.com/es/actions)
- [Marketplace de GitHub Actions](https://github.com/marketplace?type=actions)
- [Sintaxis del workflow](https://docs.github.com/es/actions/writing-workflows/workflow-syntax-for-github-actions)
- [Acción para desplegar en GitHub Pages](https://github.com/actions/deploy-pages)
- [Acción para desplegar en Azure](https://github.com/azure/webapps-deploy)
