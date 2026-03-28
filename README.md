# Portfolio

Personal portfolio and technical blog built with [Hugo](https://gohugo.io/).

## Project Structure

```
/Portfolio
│
├── src/
│   └── Portfolio/          # Hugo site source
│
├── docs/                   # Architecture diagrams, ADRs, notes
│
├── .editorconfig           # Code style consistency
├── .gitignore              # Ignore build artifacts, secrets, etc.
├── README.md               # Project overview
├── LICENSE                 # License
└── Portfolio.sln           # Solution file
```

## Getting Started

### Prerequisites

- [Hugo](https://gohugo.io/installation/) (extended version)

### Running Locally

```bash
cd src/Portfolio
hugo server -D
```

### Building

```bash
cd src/Portfolio
hugo --minify
```

## Deployment

The site is automatically deployed to GitHub Pages via GitHub Actions on every push to the `main` branch.
