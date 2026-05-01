# Setup

## Prerequisites

- **Node.js** >= 18.x (LTS recommended)
- **npm** >= 9.x or **yarn** >= 1.22
- **Angular CLI** installed globally: `npm install -g @angular/cli`

## Getting Started

```bash
# Clone the repository
git clone <repo-url> hola-cafre
cd hola-cafre

# Install dependencies
npm install

# Start development server
ng serve

# Open in browser
open http://localhost:4200
```

## Available Commands

| Command | Description |
|---------|-------------|
| `ng serve` | Start dev server with hot reload |
| `ng serve --open` | Start dev server and open browser |
| `ng build` | Production build (output in `dist/`) |
| `ng test` | Run unit tests |
| `ng lint` | Run ESLint |
| `ng generate component <name>` | Scaffold a new component |

## Environment Configuration

Environment files are located in `src/environments/`:

```
src/environments/
├── environment.ts            # Development
├── environment.staging.ts    # Staging
└── environment.production.ts # Production
```

Key environment variables (TBD):
- API base URL
- CMS endpoint / API key
- Store/payment service credentials
- Analytics tracking ID

## Project Conventions

- File naming: kebab-case (e.g. `gallery-grid.component.ts`)
- Component prefix: `hc-` (Hola Cafre)
- Styles: SCSS with BEM-like naming, design tokens in `src/styles/tokens/`
- Commit messages: Conventional Commits (`feat:`, `fix:`, `docs:`, etc.)
