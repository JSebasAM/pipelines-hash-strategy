# HashMap Pokédex

[![Deploy to GitHub Pages](https://github.com/JSebasAM/pipelines-hash-strategy/actions/workflows/deploy.yml/badge.svg)](https://github.com/JSebasAM/pipelines-hash-strategy/actions/workflows/deploy.yml)

Aplicación Angular con navegación mediante `HashLocationStrategy` y una vista de Pokédex alimentada por [PokéAPI](https://pokeapi.co/). Desplegada automáticamente en GitHub Pages con GitHub Actions.

**Demo:** https://JSebasAM.github.io/pipelines-hash-strategy/

> Captura de pantalla: pendiente de agregar en `docs/screenshot.png` y referenciar aquí (`![Captura](docs/screenshot.png)`).

## Tecnologías

- Angular 20 (componentes standalone)
- `HashLocationStrategy` (`withHashLocation()`), compatible con GitHub Pages sin `404.html`
- PokéAPI y Kitsu API
- Karma + Jasmine (ChromeHeadless)
- ESLint (`angular-eslint`) y Prettier
- GitHub Actions + GitHub Pages

## Instalación

```bash
npm ci
npm start
```

Rutas disponibles: `/#/` (inicio), `/#/pokemon`, `/#/about` y la lista de anime.

## Scripts

| Script                 | Descripción                               |
| ---------------------- | ----------------------------------------- |
| `npm start`            | Servidor de desarrollo                    |
| `npm run build`        | Build de producción                       |
| `npm test`             | Pruebas unitarias (Karma, ChromeHeadless) |
| `npm run lint`         | ESLint                                    |
| `npm run format`       | Prettier (escribe cambios)                |
| `npm run format:check` | Prettier (solo verifica, usado en CI)     |

## Estructura

```
src/app/
├── models/       # Interfaces de datos
├── pages/        # Componentes de página
├── providers/    # Proveedores (router con hash)
└── services/     # Servicios que consumen las APIs
.github/workflows/deploy.yml   # build → deploy → verify
```

## Pipeline

El workflow [`deploy.yml`](.github/workflows/deploy.yml) se ejecuta en cada push a `master` o manualmente:

1. **build**: `npm ci`, lint, formato, pruebas y build con `--base-href "/pipelines-hash-strategy/"`.
2. **deploy**: publica `dist/hash-map-app/browser` en GitHub Pages.
3. **verify**: hace `curl` con reintentos (~2 min) y falla si no hay HTTP 200 o falta `<app-root`.

## Contribuir

Usa [Conventional Commits](CONTRIBUTING.md).
