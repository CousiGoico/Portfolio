# Mi Blog Técnico — Portfolio

Blog técnico personal construido con [Hugo](https://gohugo.io/) y desplegado automáticamente en GitHub Pages.

## 🚀 Tecnologías

| Herramienta | Versión |
|---|---|
| [Hugo](https://gohugo.io/) | latest (extended) |
| Tema | [hugo-theme-dream](https://github.com/g1eny0ung/hugo-theme-dream) |
| Despliegue | GitHub Actions → GitHub Pages |

## 📁 Estructura del proyecto

```
Portfolio/
├── archetypes/        # Plantillas para nuevos contenidos
├── content/
│   └── posts/         # Artículos del blog
├── public/            # Sitio generado (no editar manualmente)
├── themes/
│   └── hugo-theme-dream/  # Tema principal (submódulo Git)
├── hugo.toml          # Configuración de Hugo
└── .github/
    └── workflows/
        └── deploy.yml # Workflow de despliegue automático
```

## ⚙️ Configuración

El archivo `hugo.toml` contiene la configuración principal del sitio:

- **baseURL**: `https://portfolio.github.io/`
- **languageCode**: `es`
- **title**: `Mi Blog Técnico`
- **author**: Fco. Javier Cousiño

## 🛠️ Desarrollo local

### Prerrequisitos

- [Git](https://git-scm.com/)
- [Hugo Extended](https://gohugo.io/installation/) (versión latest recomendada)

### Instalación

```bash
# Clonar el repositorio incluyendo los submódulos
git clone --recurse-submodules https://github.com/CousiGoico/Portfolio.git
cd Portfolio
```

Si ya tienes el repositorio clonado sin submódulos:

```bash
git submodule update --init --recursive
```

### Ejecutar en local

```bash
hugo server -D
```

El sitio estará disponible en `http://localhost:1313`. El flag `-D` incluye los borradores (*drafts*).

### Construir el sitio

```bash
hugo --minify
```

Los archivos generados se guardarán en el directorio `public/`.

## ✍️ Añadir contenido

Para crear un nuevo artículo usa el comando de Hugo:

```bash
hugo new posts/nombre-del-articulo.md
```

Edita el fichero generado en `content/posts/`, rellena el front matter y escribe el contenido en Markdown. Cuando el artículo esté listo, cambia `draft: true` a `draft: false`.

## 🚢 Despliegue

El despliegue es completamente automático. Cada push a la rama `main` dispara el workflow de GitHub Actions (`.github/workflows/deploy.yml`) que:

1. Construye el sitio con `hugo --minify`.
2. Publica el directorio `public/` en la rama `gh-pages` mediante [peaceiris/actions-gh-pages](https://github.com/peaceiris/actions-gh-pages).

## 👤 Autor

**Fco. Javier Cousiño**

## 📄 Licencia

Este proyecto es de uso personal. Todos los derechos reservados.
